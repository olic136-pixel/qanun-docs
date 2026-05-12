# C1 — `write_rulebook` extract_citations hook design memo

**Date:** 2026-05-12
**Author:** Overnight sprint Claude (Opus 4.7) per `Authorise overnight-sprint-2026-05-11`
**Status:** Design memo only — DO NOT IMPLEMENT this session per the C1 spec.

---

## Current state

Two pipelines write to the `citations` table; `write_rulebook` does
not touch them. The split is intentional, but inconsistently documented.

### Producers of `citations` rows

1. **`extract_inline_cross_references(text, source_entity, source_rulebook)`**
   in `adgm_corpus/processing/citation_extractor.py:249`. Per-section
   extractor with per-jurisdiction `_CANONICAL_TARGET_MAP` and
   `_SHORTHAND_MAP`. Emits `inline_anchor` + `inline_shorthand` rows.
   Invoked by:
   - `scripts/reextract_citations_for_flipped_versions.py` (run
     post-A1-apply per the orchestrator's "next step" message;
     scope = sections of docs whose is_current=1 was set within
     the last 30 min, or `--all-flipped`).
   - `scripts/rebuild_inline_citations.py` (full rebuild; idempotent
     in --apply mode — deletes existing rows for the rulebooks being
     rebuilt before re-inserting).

2. **`extract_citations(text)`** in
   `adgm_corpus/processing/citation_extractor.py:326`. Legacy
   document-scoped extractor, pattern-based. Emits
   `legacy_intra_rulebook` rows. Invoked by:
   - `scripts/process_all.py:387` (legacy bulk-process flow; not
     used by A1).
   - **Not invoked by anything in the A1 orchestrator path.**

3. **Phase B EAO cross-references** via `extract_eao_er_references`
   (separate path, only on source_doc=2799). Emits `eao_reference` rows.

`write_rulebook(conn, doc, diff)` does NOT call any extractor. After it
returns, the orchestrator emits a `## Next step` line:

```
Run `python scripts/reextract_citations_for_flipped_versions.py --apply`
to refresh inline citations for the just-flipped documents.
```

The operator is expected to run that script as a follow-up step.

---

## The C1 question

Should `write_rulebook` call `extract_inline_cross_references()`
directly during apply, replacing the manual two-step flow? Or should
the separate reextract script remain canonical?

---

## Option A: hook the extractor inside `write_rulebook`

Add to `write_rulebook` (after sections are inserted, before commit):

```python
for section in sections:
    inline = extract_inline_cross_references(
        section.text,
        doc["source_entity"],
        source_rulebook=doc["rulebook_code"],
    )
    for cite in inline:
        conn.execute(
            "INSERT INTO citations (source_doc, target_ref, context, source_section_id, citation_type) VALUES (?,?,?,?,?)",
            (new_doc_id, cite.target_ref, cite.context, section_id, cite.citation_type),
        )
```

### Pros

- **One-step apply.** Operator runs `refresh_rulebooks.py --apply`;
  citations are computed and persisted in the same transaction.
- **No orphan window.** Today, between the orchestrator's commit
  and the operator running the reextract script, the new doc has
  no citations. Quick Lookup synthesis on the new doc during that
  window produces zero "see also" cross-references. The hook
  eliminates the window.
- **One source of truth for invocation.** No more `scripts/reextract…`
  vs `scripts/rebuild…` confusion — `write_rulebook` owns it.
- **Test coverage centralised.** Citation behaviour is testable in
  the same fixtures as the upsert.

### Cons

- **Apply path slower.** Per-section LLM calls or regex matches now
  run inline. Current `extract_inline_cross_references` is pure
  regex (fast), but if it grows LLM-assisted disambiguation later
  (B8), apply becomes a multi-minute operation.
- **Less re-runnable.** Today the operator can re-extract citations
  without re-applying the rulebook (e.g., after adding a new
  `_CANONICAL_TARGET_MAP` entry). With the hook, re-extraction
  requires re-applying (or keeping the rebuild script alongside,
  which defeats the simplification).
- **Risk window narrower but harder to undo.** A bad map entry
  produces bad citations as part of the same transaction as the
  doc write. Today, citation bugs are isolated from doc-state bugs.
- **FSRA behaviour unchanged?** Today's FSRA E1 work uses the
  per-section reextract for all FSRA rulebooks. Switching FSRA to
  the hook needs careful re-testing: does the hook produce the
  same citations as `scripts/rebuild_inline_citations.py` for the
  same input? Regression tests required.

---

## Option B: keep the separate scripts canonical

Status quo. `write_rulebook` writes docs + sections only; the
operator runs `scripts/reextract_citations_for_flipped_versions.py`
after.

### Pros

- **Re-runnable in isolation.** Change `_CANONICAL_TARGET_MAP`, run
  the rebuild script, no rulebook re-apply needed.
- **Apply stays fast.** Doc writes commit quickly; citation
  extraction runs in its own time.
- **Existing test coverage is intact.** No new behavioural surface.

### Cons

- **Operator must remember.** The "Next step" message is a manual
  ceremony. Forgetting it leaves the new doc citation-less.
- **Orphan window during deploy.** Between apply and reextract,
  Quick Lookup on the just-flipped doc shows fewer cross-refs.
  Today's window is minutes; harder to formalise.
- **Two scripts to maintain.** `reextract` and `rebuild` overlap;
  any change to extraction semantics has to land in both.

---

## Option C (recommended) — hook + opt-out + idempotence

Add the hook to `write_rulebook` but make it conditional and idempotent.

```python
def write_rulebook(
    conn, doc, diff=None,
    *,
    extract_inline_citations: bool = True,
):
    # … existing invariant + insert path …
    if extract_inline_citations:
        _extract_and_insert_citations(conn, new_doc_id, sections, doc)
```

Why this works:

- **Default-on** captures Option A's "no orphan window" benefit.
- **`extract_inline_citations=False`** allows the rebuild script
  (and tests) to write docs without computing citations, preserving
  re-runnability.
- **Idempotent** because `_extract_and_insert_citations` deletes
  any prior `inline_anchor` + `inline_shorthand` rows for
  `source_doc = new_doc_id` before inserting (matches the rebuild
  script's invariant).
- **Forward-compatible.** When B8's LLM-assisted DFSA citation maps
  land, the hook can degrade to "fast pass only" by default and
  the LLM-assisted pass runs as the separate rebuild script.

### Recommendation

**Adopt Option C.** Lands incrementally: first the hook with default
True for FSRA, default False for DFSA until B8's DFSA citation maps
are stable. Once DFSA citations stabilise, flip DFSA default to True.

---

## Risk register

- **R1 — Test divergence.** The hook and the rebuild script could
  drift over time. Mitigation: factor the extraction-and-insert
  logic into a single helper (`_extract_and_insert_citations`)
  called by both. The reextract script becomes a "find flipped
  docs, call the helper" loop; the rebuild script becomes a
  "delete by rulebook, call the helper" loop.
- **R2 — FSRA regression.** Switching FSRA to the inline path
  requires verifying citation counts match the current rebuild
  output. Pre-change: dry-run the hook on a sandbox, diff the
  resulting `citations` table against a rebuild of the same docs.
- **R3 — Performance regression.** Per-section regex matches are
  cheap but per-doc (×100 sections) adds up. Profile against the
  largest FSRA rulebook (FUNDS 873k chars, ~150 sections); budget
  ~5 seconds total per refresh as the upper bound.
- **R4 — Tests that mock `write_rulebook`** (today there are
  several) may need updating to expect the new citations rows.
  Audit before landing.

---

## Tests needed (when implementation is authorised)

- `test_write_rulebook_hook_creates_inline_citations`: with default
  hook enabled, applying a fresh FSRA rulebook produces non-empty
  citations.
- `test_write_rulebook_hook_idempotent_on_re_apply`: applying the
  same doc twice does not duplicate citation rows.
- `test_write_rulebook_hook_disabled_skips_extraction`: with the
  kwarg False, no citations created.
- `test_fsra_hook_matches_rebuild_output`: golden test — for a
  representative FSRA rulebook, the hook produces the same
  `citations` rows as `scripts/rebuild_inline_citations.py` does.
- `test_dfsa_hook_default_is_skip_until_b8`: DFSA scraper's
  `upsert_rulebook` passes `extract_inline_citations=False` until
  B8's DFSA maps land.

---

## Out-of-scope tonight

This memo is design only. No code implemented. Authorise C1
implementation in a future session — suggested phrase
`Authorise C1-extract-citations-hook`.

---

## Register

Maps to register item C1.
