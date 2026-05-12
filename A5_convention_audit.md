# A5 — Convention-Dependent Lookups Audit

**Date:** 2026-05-12
**Author:** Overnight sprint Claude (Opus 4.7) per `Authorise overnight-sprint-2026-05-11`
**Scope:** read-only audit of `/Users/oliver/ADGM/adgm-corpus/` + `/Users/oliver/ADGM/qanun-api/`
**Verified data state:** `corpus.db` (2026-05-10 snapshot, sha256 `344305f05d…`)

---

## Why this audit exists

Today's four A1 bugs (A1.b convention drift, A1.f filename filter, A1.g
existence-check, A1.h content_hash drift) shared a shape: code paths
that worked correctly against the pre-A1 corpus state but broke against
the post-A1 state. Each carried an implicit assumption about a
convention encoded in TEXT data, not enforced by schema.

This audit enumerates every code path that touches the six
convention-dependent fields and flags WRITE/READ pairs where the
conventions disagree. Findings drive proposed new register items.

---

## Fields under audit

| Field           | Stated convention                                                |
|-----------------|------------------------------------------------------------------|
| `rulebook_code` | DFSA prefixed (`DFSA-COB`); FSRA bare (`GEN`)                    |
| `section_ref`   | Pre-K7 FSRA `OTHER X.Y`; post-K7 `<CODE> X.Y[.Z]`; DFSA `<CODE> X.Y[.Z]` (bare) |
| `source_url`    | Non-empty for `is_current=1` rows                                |
| `content_hash`  | `sha256(full_text)` (A1.h) — NOT `sha256(raw_response_bytes)`    |
| `version_str`   | FSRA `VER<digits>.<digits>`; DFSA `VER<digits>-<digits>`         |
| `source_key`    | UNIQUE; lowercase snake_case + version stamp                     |

---

## 1. `rulebook_code`

**WRITE sites (no validation enforces convention):**
- `adgm_corpus/storage/db.py::insert_document` — accepts `rulebook_code` kwarg, no check.
- `adgm_corpus/storage/db.py::update_document` — FTS sync re-indexes without normalising.
- All ingestion paths (orchestrator + per-scraper `upsert_rulebook`).

**Actual data convention (verified):**

| source_entity | rulebook_code pattern        | examples                       |
|---------------|------------------------------|--------------------------------|
| FSRA          | bare                         | `GEN`, `COBS`, `PRU`, `MKT`    |
| DFSA          | prefixed                     | `DFSA-COB`, `DFSA-GEN`, etc.   |
| ADGM          | mixed prefixed / pseudo      | `ADGM-ER`, `ADGM-ER-2024-EAO`  |
| ADGM_RA       | bare                         | `RA-12`, `RA-15` (TBC)         |

**READ sites:**
- `adgm_corpus/storage/db.py::get_current_rulebook(conn, entity, code)` — exact-string SQL equality.
  Caller must supply the correct convention. No fallback / no alias.
- `adgm_corpus/processing/structure_parser.py:58` — `bare_code = rulebook_code.split("-")[-1] if "-" in rulebook_code else rulebook_code` — tolerates both, derives bare for regex prefix matching.
- `adgm_corpus/mcp/server.py` (6 sites: 353/424/632/670/786/862) — pass-through to Pinecone metadata; no normalisation.
- `qanun-api/routers/quicklookup.py:227` — `r.get("rulebook_code") == "ADGM-ER-2024-EAO"` — hardcoded exact match (single special case).
- `qanun-api/routers/corpus.py:310` — same hardcoded ADGM-ER-2024-EAO match.

**Validation sites:** None. No regex, assertion, or schema constraint.

**Cross-jurisdiction risk:** A caller that supplies the wrong convention
to `get_current_rulebook` (e.g., asking for `DFSA-COB` against
source_entity `FSRA`, or `COB` against `DFSA`) gets `None` back —
indistinguishable from "no rulebook exists". This is the exact failure
mode A1.g surfaced. The A1.g fix patched the orchestrator to use the
scraper's emitted `rulebook_code`; nothing prevents the next caller
from making the same mistake.

→ Proposed register item **A5.A**.

---

## 2. `section_ref`

**WRITE sites:**
- `adgm_corpus/storage/db.py::insert_section` — no validation.
- `adgm_corpus/processing/structure_parser.py` (lines 82, 84, 131, 137, 145, 161, 175, 213) — builds `section_ref` by concatenating `rulebook_code` with numeric ref. Inherits the rulebook_code convention; so DFSA section_refs look like `DFSA-COB 5.2.1` (prefixed code + space + numeric).

**Actual data convention (verified):**

| source_entity      | section_ref pattern                | sample              |
|--------------------|-----------------------------------|---------------------|
| FSRA (post-K7)     | `<BARE_CODE> X.Y[.Z][.lettered]`  | `GEN 3.5`, `COBS 7.2.1` |
| FSRA (pre-K7)      | `OTHER X.Y[.Z]`                   | `OTHER 3.5.1`       |
| DFSA               | `<PREFIXED-CODE> X.Y[.Z]`         | `DFSA-COB 5.2.1`    |
| ADGM legislation   | `<CODE> Sec.NN` or `<CODE> X.Y`   | `ADGM-ER-2024 Sec.55` |
| FSMR / IFR         | `FSMR Sch1 art3` (varies)         |                     |

**READ sites:**
- `qanun-api/services/change_detection_service.py:54, 200` — `a.section_ref.split()[0]` to derive the rulebook code. Works for `GEN 3.5` → `GEN` and `DFSA-COB 5.2.1` → `DFSA-COB`. Fragile if numeric segment ever begins with whitespace or a hyphen.
- `adgm_corpus/mcp/server.py::_get_section_outbound_refs` — exact-string match against `section_ref`. Caller must know exact format.
- `intelligence_pkg/agents/twin_monitor.py:151` — exact equality.
- Many test fixtures assert exact strings.

**Validation sites:** None.

**Cross-jurisdiction risk:** The portability map (B7) will need to bridge
between `GEN 3.5.1` (FSRA) and `DFSA-COB 5.2.1` (DFSA) for equivalent
rules. Today's code has no canonical decomposition function; every
consumer reinvents `split()[0]` or hand-rolled regex. Each reinvention
is a future convention-drift bug.

The pre-K7 `OTHER X.Y` artefacts on doc 206 (and likely other legacy
FSRA docs) are dead references unless A3 retags them. Any consumer that
follows historical-version queries through is_current=0 docs will hit
`OTHER X.Y` and either silently return nothing or misroute.

→ Proposed register item **A5.B**.

---

## 3. `source_url`

**WRITE sites:**
- Schema: `source_url TEXT NOT NULL` in `documents` table.
- Pre-A1 FSRA scraper (`adgm_corpus/collection/scrapers/adgm_rulebooks.py`) sets `source_url=""` on the doc dict before the recent A1.a refactor unless the PDF URL was captured.
- DFSA scraper (A1.b) sets `source_url=module_url` — populated.

**Actual data convention (VERIFIED, the schema NOT NULL is satisfied by empty strings):**

| source_entity | empty source_url, is_current=1 |
|---------------|--------------------------------|
| DIFC_COURTS   | 1,066                          |
| FSRA          | 627                            |
| ADGM_COURTS   | 263                            |
| UNKNOWN       | 57                             |
| BVI_FSC       | 27                             |
| DFSA          | 22                             |
| EL_SALVADOR   | 16                             |
| ADGM_RA       | 8                              |
| PANAMA_SMV    | 5                              |
| DIFC          | 5                              |
| MONDAQ        | 2                              |
| PANAMA        | 1                              |
| **Total**     | **2,099**                      |

DFSA's 22 empty is the post-A1 bulk's full set of is_current=1 modules
— suggesting the A1.b scraper isn't actually populating `source_url`
on its output (or the upsert path is dropping it). Surface immediately.

**READ sites:**
- `adgm_corpus/storage/db.py::get_section_by_ref` — selects `d.source_url`; returns empty string to callers without distinguishing from null.
- `intelligence_pkg/exporters/provenance_trace.py:59` — renders blank in the memo when empty.
- `qanun-api/routers/quicklookup.py:67-70` — returns empty to API consumers.

**Validation sites:** None at runtime (the schema's NOT NULL is satisfied by `""`).

→ Proposed register item **A5.C** (and a discovery — the DFSA empty
source_url is a fresh bug from today's A1 bulk; bumps A4 priority).

---

## 4. `content_hash`

**WRITE sites:**
- `adgm_corpus/collection/scrapers/adgm_rulebooks.py:378-395` — FSRA scraper computes `sha256(full_text)` after A1.h fix. ✓
- `adgm_corpus/collection/scrapers/dfsa_rulebooks.py:_doc_dict_from_html` — DFSA scraper computes `sha256(full_text)` after A1.h fix. ✓
- Older ingestion paths (`scripts/phase_a_*`, legacy court scrapers) may not pre-compute.

**Actual data convention (VERIFIED):**

| content_hash kind | is_current=1 count |
|-------------------|--------------------|
| sha256 hex (64 chars) | 2,176          |
| empty or NULL     | 122                |

94% pre-computed. The 122 empty rows are pre-A1.h ingestion artefacts
or non-rulebook docs (consultations, circulars, judgments) where the
ingestion path doesn't run the same scraper.

**READ sites:**
- `intelligence_pkg/agents/retriever.py:66` — **regenerates** content_hash from section text on the fly for deduplication: `hashlib.sha256((row["text"] or "").encode()).hexdigest()`. This is for section-level dedup, not document-level. Distinct from document.content_hash.
- `adgm_corpus/storage/db.py` queries return content_hash unchanged.

**Validation sites:**
- A1.h's regression test `test_content_hash_ignores_drupal_form_selectors` asserts the invariant for DFSA.
- No assertion-at-INSERT that content_hash matches sha256(full_text).

**Cross-jurisdiction risk:** Low for current ingestion (A1 scrapers do
the right thing) but the 122 empty rows on is_current=1 mean any
"are these two docs identical?" check across all jurisdictions can't
short-circuit on content_hash alone. Inserting via a code path that
doesn't compute the hash silently bypasses the A1.h regression.

→ Proposed register item **A5.D** (modest priority — A1.h's coverage is
already good; this just plugs the remaining gap).

---

## 5. `version_str`

**WRITE sites:**
- FSRA scraper: format `VER<digits>.<digits>` extracted from filename via `VERSION_PATTERN = re.compile(r"VER(\w+?)(?:\.(\d+))?\.pdf", re.IGNORECASE)`.
- DFSA scraper: format `VER<digits>-<digits>` extracted from URL slug via `_parse_slug_version`.

**Actual data convention (verified — small samples):**

| source_entity | sample version_str values        |
|---------------|----------------------------------|
| FSRA          | `VER07.310325`, `VER12.311025`, `VER13.270426` |
| DFSA          | `VER5101-26`, `VER7101-26`, `VER10/01-26` (note the `/` variant) |
| Some legacy   | `"Feb 2025"` (one row — human-readable) |

**READ sites:**
- `_parse_version_num` and `_parse_version_str` in `adgm_corpus/collection/scrapers/adgm_rulebooks.py` — assume `VER<digits>.<digits>` pattern.
- DFSA's parser is hyphen-tolerant.
- `intelligence_pkg/exporters/provenance_trace.py:59` — renders verbatim.
- `qanun-api/routers/corpus.py:145` — passes verbatim to client.

**Validation sites:** None.

**Cross-jurisdiction risk:** Tools that try to **compare** versions
across jurisdictions (e.g., "is this rulebook out of date by how
many bumps?") would hit the separator difference and the occasional
oddball value. No comparison logic exists today; the format is a
display string. Risk is forward-looking, not current.

→ Proposed register item **A5.E**.

---

## 6. `source_key`

**WRITE sites:**
- Schema: `source_key TEXT NOT NULL UNIQUE`.
- Pattern: lowercase, snake_case, version-stamped. Examples observed in commits and tests: `fsra_gen_v7`, `dfsa_cob_prefixed_existing`, `fsra_gen_ver07.310325`.

**Actual data convention (verified):** UNIQUE constraint holds — 2,595
distinct source_keys for 2,595 documents. No two rows share a key.

**READ sites:**
- `adgm_corpus/storage/db.py::get_document_by_key`
- `adgm_corpus/storage/db.py::get_manifest_entry`
- MCP server / retriever — exact-string match.

**Validation sites:** UNIQUE constraint at DB only; no regex enforcement.

**Cross-jurisdiction risk:** Today's UNIQUE constraint catches duplicates,
which is the only correctness property the field really needs. Naming
convention drift exists (`fsra_gen_v7` vs `fsra_gen_ver07.310325`) but
doesn't break anything as long as keys remain distinct per version.

→ Filed as **A5.F** but with low priority — naming convention without a
correctness impact.

---

## Proposed new register items

### A5.A — Normalise `rulebook_code` lookups (Half-day)

**Status:** Open. Dependencies: none. Source: A5 audit, 2026-05-12.

**Description.** Build a `normalize_rulebook_code(source_entity, code)`
helper that converts between bare (`COB`) and prefixed (`DFSA-COB`)
forms. Apply it in `get_current_rulebook`, in MCP search paths, and at
any other site that uses `rulebook_code` as a lookup key. Today A1.g
fixed one symptom (the orchestrator); the next caller has the same
trap. The hardcoded `ADGM-ER-2024-EAO` matches in
`quanun-api/routers/quicklookup.py:227` and `routers/corpus.py:310`
are red flags for the same convention pattern.

**Acceptance.** Lookups succeed under either input form for a given
jurisdiction. Regression tests cover both directions. The hardcoded
`ADGM-ER-2024-EAO` matches are replaced with normalised checks.

---

### A5.B — Canonical `section_ref` decomposition + portability prep (Half-day)

**Status:** Open. Dependencies: prerequisite for B7 (portability map seeding).
Source: A5 audit, 2026-05-12.

**Description.** Define a `decompose_section_ref(ref)` function returning
`(rulebook_code, numeric_part)`. Replace every `split()[0]` site
(change_detection_service:54, change_detection_service:200, and any
others surfaced by grep) with the canonical helper. Add a regression
test fixture covering all five known section_ref shapes (FSRA post-K7,
FSRA pre-K7 OTHER, DFSA prefixed, ADGM legislation with `Sec.NN`,
FSMR Schedule references).

**Acceptance.** No more `split()[0]` on `section_ref` outside the
canonical helper. Helper handles all five known shapes. B7 portability
map can rely on this for cross-jurisdiction equivalence.

---

### A5.C — `source_url` backfill (Multi-day)

**Status:** Open. Dependencies: A4 already in register; this updates A4 with new data.
Source: A5 audit, 2026-05-12.

**Description.** The register's existing A4 sized "Multi-day" with
~200 affected docs. The actual count is **2,099 is_current=1 rows
with empty source_url across 12 source_entities**. The 22 empty DFSA
rows are post-A1 — fresh from today's bulk — and should be the first
fix because they affect a corpus segment with otherwise-clean A1
captures. Court decisions (1,066 DIFC_COURTS + 263 ADGM_COURTS)
likely lack URLs by nature and may need a different treatment (e.g.,
nullable column or whitelist).

**Acceptance.** Per the existing A4 acceptance + (a) every DFSA
is_current=1 doc has a non-empty source_url; (b) consultations,
circulars, guidance have URLs backfilled or are explicitly flagged
as "no public URL"; (c) court decisions either get URLs or move to a
schema with nullable source_url.

---

### A5.D — Pre-compute `content_hash` for every is_current=1 doc at INSERT (Half-day)

**Status:** Open. Dependencies: A1.h already landed.
Source: A5 audit, 2026-05-12.

**Description.** A1.h fixed the DFSA + FSRA scrapers to compute
`sha256(full_text)` during ingestion. 2,176 is_current=1 docs now
have correct hashes. 122 don't (pre-A1.h ingestion paths — consultations,
circulars, judgments, etc.). Backfill: `content_hash = sha256(full_text)`
for the 122 docs in a single SQL transaction. Then add an INSERT-time
assertion that content_hash, when non-empty, matches sha256(full_text);
raise `ContentHashConventionError` if not.

**Acceptance.** Every is_current=1 doc with a non-empty `full_text`
has a 64-character hex `content_hash`. Assertion catches future
drift.

---

### A5.E — `version_str` canonical type (Multi-day, low priority)

**Status:** Open. Dependencies: none. Source: A5 audit, 2026-05-12.

**Description.** Define a `VersionStr` value type with regex
`^VER\d+[.-]\d+$`. Add an INSERT validator. Backfill the one stray
`"Feb 2025"` row to either a real version or an explicit
`"VER-LEGACY-2025-02"` placeholder. Future version-comparison logic
(e.g., "did this rulebook bump between two corpus snapshots?") can
rely on the canonical type.

**Acceptance.** Validator on INSERT; one stray row resolved.
Comparison helper `compare_versions(a, b) → -1|0|+1` available.

---

### A5.F — `source_key` naming convention enforcement (≤1 hour, lowest priority)

**Status:** Open. Dependencies: none. Source: A5 audit, 2026-05-12.

**Description.** Document the canonical `source_key` shape
(`<entity_lower>_<rulebook_lower>_ver<numeric>` or similar) and add a
regex check on INSERT. Backfill any non-conforming rows. No
correctness impact today; this is hygiene.

**Acceptance.** Documented convention; regex enforcement; non-
conforming rows resolved.

---

## Out-of-scope discovery

While auditing, encountered references to `adgm_corpus/agents/*` and
`adgm_corpus/ingestion/*` (out-of-band Hetzner code per user memory
`project_qanun_out_of_band_code.md` and `feedback_qanun_no_touch_agents_ingestion.md`).
These were NOT inspected per the no-touch policy. If A5.A/A5.B helpers
need to be referenced from those packages, surface for authorisation
before any change.

---

## Register

Maps to register item A5. Each A5.A–F is a candidate new item.
