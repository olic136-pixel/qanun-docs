# TICKET: qanun-api entity-threading for `get_rule` scoping

**Status:** Ready to build · **Size:** S (≤ half day incl. tests) · **Repo:** qanun-api
**Origin:** MAX-3 J1 park-list item ("qanun-api client-side entity threading flagged as follow-up ticket", MAX3_MASTER_LOG §Phase 0) · **Written:** 2026-06-10 (MAX-4 V6)

## Background

MAX-3 J1 (sprint/max3-citations) added an optional `source_entity` parameter to the
adgm-corpus MCP `get_rule` tool to disambiguate the 7 colliding FSRA↔DFSA module codes
(AML, GEN, GLO, IFR, MKT, PIN, REP). The MCP server side is live:

```
adgm-corpus/adgm_corpus/mcp/server.py (tool schema, master):
  get_rule(citation, include_history=True, source_entity=None)
  "source_entity": "Optional entity scope (e.g. FSRA, DFSA, VARA). Disambiguates
   colliding module codes such as FSRA 'GEN 3.3' vs DFSA 'GEN 3.3'.
   Omit for the legacy unscoped lookup."
```

qanun-api never threads it. Every `get_rule` call from qanun-api is unscoped, so a
bare citation like `GEN 3.3` resolves by legacy precedence and can return the wrong
regulator's rule. Post-M21-P1 the DFSA sections are `DFSA-`-prefixed in corpus.db, which
removes most ambiguity for *prefixed* refs — but unscoped lookups of *bare* refs emitted
by older data paths, and any future entity with overlapping codes, remain mis-resolution
risks. Threading the scope is cheap and makes intent explicit.

## Call sites (qanun-api `main` @ c53f351)

`get_rule` is called through `mcp_client/client.py::mcp_manager.corpus("get_rule", args)`
from exactly **3 sites**:

### 1. `routers/corpus.py:95` — `GET /corpus/passage` (`corpus_passage`)
- Endpoint **already accepts** `source_entity: Optional[str]` (line 89) and already
  threads it into the `search_corpus` *fallback* (lines 106–107) — but the primary
  `get_rule` attempt at line 95 drops it:
  ```python
  rule_result = await mcp_manager.corpus("get_rule", {
      "citation": section_ref,
      "include_history": False,
  })
  ```
- **Entity context available:** the endpoint's own `source_entity` query param
  (frontend corpus page sends it since the K12 filter fix — param vocabulary
  `source_entity`, values FSRA / ADGM_RA / DFSA / VARA / EL_SALVADOR / BVI_FSC /
  PANAMA_SMV).
- **Change:** when `source_entity` is truthy, include it in the `get_rule` args.

### 2. `routers/corpus.py:400–403` — `_enrich_with_tier1_refs` (Tier-1 enrichment)
- Fetches outbound targets of ADGM_RA `ADGM-ER-2024-EAO` sections via
  `get_section_outbound_refs`, then `get_rule({"citation": target_ref,
  "include_history": False})` per target.
- **Entity context available:** targets are by construction Tier-1 ADGM_RA
  instruments — `_ENRICHMENT_TARGET_ENTITY_MAP = {"ADGM-ER-2024": "ADGM_RA",
  "ADGM-ER-2024-EAO": "ADGM_RA", "ADGM-WB-2024": "ADGM_RA"}` already encodes this
  (and the synthesizer *discards* payloads whose rulebook_code is unmapped).
- **Change:** pass `"source_entity": "ADGM_RA"` (constant).

### 3. `routers/quicklookup.py:285–288` — duplicated `_enrich_with_tier1_refs`
- Verbatim duplicate of site 2 (K10 deferral: helpers intentionally duplicated in
  `routers/corpus.py` and `routers/quicklookup.py` rather than extracted — see comment
  at quicklookup.py:144).
- **Change:** identical — `"source_entity": "ADGM_RA"`. Keep both copies in sync;
  extracting a shared `services/tier1_enrichment.py` is an optional refactor, NOT
  required for this ticket.

### Secondary (no `get_rule`, noted for completeness — separate decision)
- `services/corpus_ingest.py:783` — citation validation via
  `search_corpus {"query": rule_ref, "max_results": 1}` with **no entity filter**.
  When the calling template's jurisdiction is known, thread
  `source_entity` here too (same collision class, search-ranked instead of
  exact-lookup). Lower risk, but same one-line shape if picked up.
- All other corpus lookups (`quicklookup` search paths, `entity_setup`,
  `corpus.py` search/list endpoints) already thread `source_entity` via
  `ENTITY_MAP` (quicklookup.py:452) / explicit params. No change.

## Change shape

```python
# site 1 (corpus_passage)
args = {"citation": section_ref, "include_history": False}
if source_entity:
    args["source_entity"] = source_entity
rule_result = await mcp_manager.corpus("get_rule", args)

# sites 2+3 (tier1 enrichment, both copies)
rule_payload = await mcp_manager.corpus(
    "get_rule",
    {"citation": target_ref, "include_history": False,
     "source_entity": "ADGM_RA"},
)
```

Backwards compatibility: `source_entity` is optional server-side; omitting it preserves
legacy behaviour, so no MCP version coupling. If qanun-api ever runs against a pre-MAX-3
corpus MCP, the unknown kwarg would raise inside `_get_rule(**arguments)` — production
Hetzner deployed the MAX-3 server, so this is a non-issue; do not add fallback logic.

## Tests (new file `tests/test_entity_threading.py`, mock `mcp_manager`)

1. **corpus_passage threads the param** — call `GET /corpus/passage?section_ref=GEN+3.3&source_entity=DFSA`;
   assert the mocked `mcp_manager.corpus` saw `("get_rule", {... "source_entity": "DFSA"})`.
2. **corpus_passage omits when absent** — no `source_entity` query param ⇒ `get_rule`
   args contain **no** `source_entity` key (legacy unscoped contract preserved).
3. **tier1 enrichment scoped (both routers)** — drive `_enrich_with_tier1_refs` with a
   seeded ADGM_RA/EAO result + mocked `get_section_outbound_refs` payload; assert every
   `get_rule` call carries `source_entity="ADGM_RA"`. Parameterise over the
   `routers/corpus.py` and `routers/quicklookup.py` copies to enforce K10 sync.
4. **Collision regression (integration-ish, optional if a live corpus.db fixture is
   available):** `get_rule("GEN 3.3", source_entity="DFSA")` must NOT return the FSRA
   GEN section (post-P1 it resolves to `DFSA-GEN 3.3` or not-found, never cross-entity).

## Acceptance
- 3 call sites threaded; suite green (baseline 1,026/0 per MAX-3, plus new tests).
- Verify the qanun frontend corpus page actually sends `source_entity` on the passage
  fetch for non-default tabs (it does for `/corpus/search` since K12; confirm passage).
- No behaviour change for unscoped callers.
