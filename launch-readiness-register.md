# Qanun — Launch-Readiness Register

**Version:** 1.3
**Date:** 13 May 2026 (morning, post-Bundle-1 merge session)
**Owner:** Oliver Cook KC (CLO)
**Status:** Living document — updated as items land or new items surface

**v1.3 changes from v1.2:**
- **Bundle 1 merge session complete.** Four sprint branches from the 12-13 May overnight merged across two repos (adgm-corpus: 3 merges — A7-diag, flake-perf, A5C1; qanun-api: 1 merge — F2-TRADEDAR). First-parent topology preserved; sprint branches retained on origin; no force-pushes; 8 gate test counts (4 on-branch + 4 post-merge) all matched projection exactly.
- **F2.TRADEDAR moved Open → Done** (merge `805f50f` on qanun-api main). Fixture redesigned as autouse session-scoped seed; xfail-strict flipped to passing.
- **A5.C.1 partial progress** — script + tests committed (merge `ccfa1c0` on adgm-corpus master); backfill APPLY against corpus.db remains Open, pending explicit interactive authorisation per HG1.
- **C11 partial progress** — near-term threshold-raise mitigation committed (merge `059ad05` on adgm-corpus master); proper C11.A redesign remains Open. Diagnostic refuted the order-dependency hypothesis: root cause is cold-start network variance.
- **A7 diagnostic infrastructure committed** (merge `9b77f69` on adgm-corpus master) — audit script + 10 strict xfails. Per-rulebook reconciliation applies (A2 + A7.B-A7.I) remain Open and constitute Bundle 2.
- **Status-at-a-glance table refreshed** (F2.TRADEDAR moves to Done; F open 2 → 1, Done 2 → 3; totals Open 49 → 48, Done 13 → 14).
- **Test count baselines updated:** adgm-corpus master 676P/1S/22XF; qanun-api main 42P/1S/3XF; qanun main unchanged at 5 vitest.
- **Register canonical relocation:** at Bundle 1 kickoff, the v1.2 working canonical was synced from `/tmp/qanun-overnight/launch-readiness-register-v1.2.md` into the tracked location `~/qanun-docs/launch-readiness-register.md` (qanun-docs main commit `f3d036f`). From this version forward, `~/qanun-docs/launch-readiness-register.md` is the canonical.
- **New 'Today's Achievements (13 May 2026 — Bundle 1 Merge Session)' section appended.**

**v1.2 changes from v1.1:**
- **D10 master integration session complete.** Ten sprint branches merged across three repos (adgm-corpus: 8 merges including foundation; qanun-api: 1 merge; qanun: 1 merge). First-parent topology preserved; sprint branches retained on origin; no force-pushes.
- **9 items moved fully Done** that were previously "Done — awaiting master integration": A1, A6, C2, C3, C4, C5, C7, F1, F2. Merge commit SHAs recorded inline.
- **2 new items added** from meta-findings during the integration session:
  - **C11 — TestPerformanceQuickSearch flake investigation.** Fired on 3 of 7 on-branch runs (C5, C2, C4) during integration; all cleared on retry. Pre-existing, not caused by sprint work. Order-dependency hypothesis filed.
  - **C12 — Prompt-drafting discipline for verification commands.** Three caught prompt-vs-reality mismatches during integration (smoke-check import path, sprint-branch arithmetic, diff inspection target). All caught by halt-and-surface. Memory entries #18 and #19 added; phase-2-backlog tracked in qanun-docs main.
- **Status-at-a-glance table refreshed** (counts move slightly: D10 → Done; +2 from C11/C12).
- **Sequencing recommendation advanced** — first wave can now proceed; D10 dependency removed from all blocked items.
- **Backup chain extended** — sha256 of canonical corpus.db verified unchanged at master integration close.
- **Test count baselines updated:** adgm-corpus 675P/1S/5XF; qanun-api 41P/1S/4XF/0F; qanun 5 vitest smoke tests passing.

**v1.1 changes from v1.0 (carried forward for reference):**
- 19 items marked Done from the overnight sprint of 12 May 2026 (with date, branch, commit references)
- 16 new items integrated into the register with proper IDs continuing the v1.0 numbering scheme
- **B1 resized from "Multi-day" to "Week"** — overnight verification refuted the regex-hypothesis; B1 is now a parser redesign, not a regex tweak
- **A4 superseded by A5.C** — overnight A5 audit found 2,099 rows with empty source_url, not the ~200 originally estimated; the scope expansion is captured in A5.C
- Sequencing recommendation revised to reflect new dependencies (master integration session before further sprint work; B1 reframing affects B4)

---

## Principle

Nothing knowingly broken, incomplete, or sub-optimal reaches a tester. The value of testers is finding what we missed; their value collapses if half of what they find is what we already knew. Every item in this register must be Open → Done before any beta or demo cohort sees the product.

This principle applies regardless of tester-visibility. Items invisible to a casual test session (audit-trail provenance, internal data conventions, latent test-coverage gaps) are launch-blocking if they're known-to-be-wrong. Items where we don't yet know whether anything is wrong (the unknown unknowns) are what the testers are for.

---

## How to Use This Register

- **Items are identified by category prefix + number** (e.g. B1, C3). IDs are stable once assigned; new items get the next available number, never recycled.
- **Status:** Open / Blocked (waiting on a dependency) / In Progress / Done. Updated as work progresses, with date and commit/PR reference noted on Done items.
- **Sizing convention:**
  - **Half-day:** ≤4 hours of focused work, including testing and deploy
  - **Day:** ~1 working day (5-8 hours)
  - **Multi-day:** 2-5 working days
  - **Week:** 5-10 working days
  - **Multi-week:** 10+ working days
- **Dependencies** are forward references — Item X depends on Item Y means Y must land before X can start.
- **Source** records where the item was surfaced (today's diagnostic, SOW phase, audit document, conversation date).
- **Acceptance** is the concrete test for "done" — what would convince a careful reviewer the item is genuinely complete.

---

## Status at a Glance

| Category | Open | Blocked | Done | Total |
|---|---|---|---|---|
| A — Data Integrity | 17 | 1 | 10 | 28 |
| B — Content Coverage | 5 | 4 | 1 | 10 |
| C — Code Quality | 6 | 0 | 6 | 12 |
| D — Feature Completion | 10 | 1 | 1 | 12 |
| E — Operational Hygiene | 9 | 0 | 1 | 10 |
| F — Test Coverage | 1 | 1 | 3 | 5 |
| **Total** | **48** | **7** | **22** | **77** |

**Done since v1.1 (12 May 2026 master integration session):** D10 (master integration); plus the 9 items that were "Done [awaiting integration]" now fully Done on master/main: A1, A6, C2, C3, C4, C5, C7, F1, F2.

**Done since v1.2 (13 May 2026 Bundle 1 merge session):** F2.TRADEDAR (merge `805f50f` on qanun-api main).

**Done in Bundle 2 (13 May 2026 A7-cluster reconciliation session — all 8 known A7 cases applied):** A7.E (FSRA MIR); A7.D (FSRA PRU); A2 (FSRA GEN, Path 2 with A3 K7 evidence); A7.G (BVI_FSC BVI-BCA); A7.B (FSRA COBS); A7.F (FSRA GLO); A7.H (BVI-REGS, Path (b) inverted); A7.C (FSRA FUNDS, Path A — memo §4 size-drop hypothesis invalidated; doc-199 PRU/FUNDS mislabel carved out). 8 of 8 known A7 reconciliations applied. Each flip-only; doc-level metadata + section cleanup deferred per item.

**New register items opened in Bundle 2:** A7.B.SECTIONS, A7.F.SECTIONS (COBS + GLO archived-section cleanup); A7-FUNDS-doc-199-mislabel (PRU content in FUNDS row); A7-FSRA-pipeline-size-sanity (size-floor scraper guard); **A7-GLOBAL-INVARIANT-FINDINGS** (3 new multi-current cases surfaced by defence-in-depth test — FSRA OTHER 65 rows, ADGM FSRA ADGM-FSRA-F 37 rows, ADGM_RA ADGM-RA-F 32 rows).

**Net change since v1.1:**
- 67 items → 69 items (+1 Done from D10; +2 new C11/C12)
- 9 items' status descriptions updated to drop "awaiting master integration" qualifier
- Phase-2-backlog.md now tracked in qanun-docs main (commit `a351ea7` + follow-ups)

**Revised launch timeline estimate: 5-7 weeks** (unchanged from v1.1). The master integration session was the foundation step — most subsequent first-wave items have lost their D10 dependency and can now proceed in parallel, which should pull the timeline toward the lower end of the range if discipline holds.

---

# Category A — Data Integrity

Corpus-correctness items. Without these, every downstream feature is built on shaky data.

---

### A1 — Upsert pre-flight invariant in `write_rulebook` — **DONE [2026-05-12]**

- **Status:** Done — `sprint/A1-invariant-2026-05-11-overnight` (adgm-corpus, commit `964b8fd`); merged to master in commit `2863b79`
- **Size:** Half-day
- **Source:** A1.b bug discovery, 11 May 2026
- **Description:** Pre-flight invariant added to `write_rulebook`: `COUNT(*) WHERE source_entity=? AND rulebook_code=? AND is_current=1` must be 0 or 1. If > 1, raises `MultiCurrentInvariantError` with offending source_entity, rulebook_code, and IDs. No half-written transaction on failure.
- **Acceptance:** ✓ 3 regression tests pass (multi/single/zero current rows). Verified halt before insert when invariant fails. Importable from `adgm_corpus.collection.scrapers.adgm_rulebooks` on master (note: integration prompt initially specified `adgm_corpus.storage.db`; mismatch caught and resolved during merge — see C12).
- **Notes:** Foundational item that unblocked A7-cluster's "dependency: A1 on master" entries. Master integration commit `2863b79` sits on top of foundation merge `913f93a` (which carried the A1.a–A1.h overnight scraper work).

---

### A2 — FSRA GEN orphan reconciliation — **DONE [2026-05-13]**

- **Status:** Done — interactive apply 2026-05-13 (Bundle 2; Path 2). Flip-only; 2790 metadata backfill deferred to A5.C / A5.E.
- **Size:** Half-day
- **Dependencies:** None (A1 now on master at `2863b79` — will catch any new orphans during reconciliation)
- **Source:** Pre-A1 audit + A1.h diagnostic, 11 May 2026 (confirmed scope in A7 audit, 12 May) + `/tmp/qanun-overnight/a7/A7-GEN.md`
- **Description:** Pre-apply state showed 3 is_current=1 rows on local canonical (sha `344305f0…` = 10 May Hetzner snapshot, predating the 11 May A1.h flip of 2768 on Hetzner). Hetzner had 2 currents (2768 already flipped, but `superseded_by` left NULL). Per memo §5's idempotent two-flip prescription (Path 2), local reconciliation: doc 206 (VER12.311025, 260 KB, **130 sections all `OTHER` prefix**) and doc 2768 (4.8 KB stub, 4 sections) both flipped to `is_current=0, superseded_by=2790`; doc 2790 (264.7 KB, 131 sections all `GEN` prefix) retained as canonical current. Local now slightly improves on Hetzner: 2768 has `superseded_by=2790` (vs Hetzner's NULL); the improvement propagates back at next local→Hetzner deploy.
- **Acceptance:** ✓ Rows-affected = 2; post-COMMIT invariant query `COUNT(*) WHERE source_entity='FSRA' AND rulebook_code='GEN' AND is_current=1` = 1 (doc 2790). `GEN 1.1` resolves to doc 2790 on the is_current=1 join. PRAGMA integrity_check ok. Test `test_single_current_invariant_per_rulebook[FSRA-GEN]` flipped from xfail-strict to passing. Full-suite delta: 678P/1S/20XF → 679P/1S/19XF.
- **Backup:** `/Users/oliver/ADGM/adgm-corpus/backups/corpus_pre_A7_GEN_20260513_081400.db` (sha256 `75ef39f2…`, integrity ok).
- **A3 K7 finding:** Doc 206 has 130 sections with prefix breakdown of **100% `OTHER`** (zero GEN). This is the primary A3 retag target — strongest evidence in Bundle 2 (MIR/PRU/COBS/GLO siblings showed no OTHER-prefix carry-forward). A3 retag scope now has a concrete first-item: 130 rows on doc 206 to be re-prefixed from `OTHER` to `GEN` (per A3 register entry's K7 carry-forward plan).
- **Deferred follow-ups:** (a) Doc 2790 metadata gaps (version_str / version_num / source_url) — A5.C and A5.E. (b) Hetzner 2768 row has `superseded_by=NULL`; local has `superseded_by=2790`. Reconciles at next local→Hetzner deploy; not blocking.

---

### A3 — K7 retag carry-forward for OTHER X.Y section_refs

- **Status:** Open
- **Size:** Day
- **Dependencies:** None
- **Source:** Pre-A1 audit, 11 May 2026
- **Description:** Doc 206 (and likely other pre-K7 FSRA docs) use section_refs with prefix `OTHER X.Y` instead of `GEN X.Y` / `PRU X.Y` / etc. K7 retag pass didn't carry forward to legacy is_current=0 rows. Affects historical-version queries and cross-reference resolution.
- **Acceptance:** Audit script identifies all OTHER-prefix section_refs. For each, determine correct rulebook code from parent doc's `rulebook_code`. Retag in place. Re-run citation cross-reference check.
- **Notes:** Intertwined with A2 (doc 206 becomes is_current=0 in A2; OTHER refs become historical-only).

---

### A4 — Source-URL provenance backfill — **SUPERSEDED BY A5.C**

- **Status:** Folded into A5.C (renamed and resized)
- **Reason for fold:** A5 audit on 12 May found 2,099 rows with empty source_url, not the ~200 originally estimated. The scope is an order of magnitude larger and warrants a re-scoped item.
- **See:** A5.C below

---

### A5 — Convention-dependent lookups audit — **DONE [2026-05-12]**

- **Status:** Done — memo at `~/qanun-docs/A5_convention_audit.md` (commit `95ce8b4`)
- **Size:** Day (sized at half-day; actual delivery shorter)
- **Source:** Meta-finding from today's four A1 bugs, 11 May 2026
- **Description:** Audited every code path in adgm-corpus + qanun-api that reads or writes `rulebook_code`, `section_ref`, `source_url`, `content_hash`, `version_str`, `source_key`.
- **Findings:** Surfaced 6 follow-up items (A5.A–A5.F). Two surprises: (1) 2,099 is_current=1 rows have empty source_url, not the ~200 previously estimated; (2) 22 post-A1 DFSA docs from today's bulk are also missing source_url — the new DFSA scraper isn't populating it.
- **Notes:** Verified against actual corpus.db. Each finding has a sized follow-up below.

---

### A5.A — Normalise rulebook_code lookups across the codebase

- **Status:** Open
- **Size:** Day
- **Dependencies:** None
- **Source:** A5 audit memo, 12 May 2026
- **Description:** Multiple code paths construct or query rulebook_code differently — some use bare codes (`GEN`), some prefixed (`DFSA-GEN`), some inconsistently. Establish a canonical helper `normalise_rulebook_code(source_entity, code)` and route all reads/writes through it. Eliminates the class of bug that bit A1.g.
- **Acceptance:** Helper function in `adgm_corpus/storage/db.py` or similar. All call-sites refactored. Unit tests for the helper. Convention-drift bugs cannot recur because the helper is the single source of truth.

---

### A5.B — Canonical section_ref decomposition

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** None
- **Source:** A5 audit memo, 12 May 2026
- **Description:** `section_ref` is parsed inconsistently across the codebase (some treat as opaque string, some split on space, some on dot). Build canonical decomposition: rulebook code, chapter, rule, sub-rule, paragraph. Route all section_ref parsing through it.
- **Acceptance:** Decomposition utility in `adgm_corpus/storage/db.py`. All parsing call-sites refactored. Unit tests cover the various section_ref shapes found in production data.

---

### A5.C — Source-URL backfill scale (2,099 rows, not ~200)

- **Status:** Open
- **Size:** Multi-day
- **Dependencies:** None
- **Source:** A5 audit memo, 12 May 2026 (supersedes v1.0's A4)
- **Description:** 2,099 is_current=1 rows have empty source_url. Recovery strategy varies by source_entity: (a) from local_path filename if URL is encoded, (b) by re-fetching the document during a future bulk refresh, (c) by cross-referencing against the regulator's portal. Of these 2,099, 22 are post-A1 DFSA docs from today's bulk — those need a scraper fix (A5.C.1) plus backfill, not just backfill.
- **Acceptance:** Per source_entity: every is_current=1 row has non-empty source_url. Recovery method documented per row category. Audit script verifies completeness.
- **Notes:** This is the regulatory-credibility item — a tool whose differentiator is grounded citations cannot ship with empty provenance.

---

### A5.C.1 — DFSA scraper source_url population fix

- **Status:** Open — script + tests landed; backfill APPLY pending
- **Size:** Half-day
- **Dependencies:** None
- **Source:** A5 audit memo finding 12 May 2026
- **Description:** Today's A1 DFSA bulk produced 22 new is_current=1 docs that lack source_url. The DFSA scraper isn't populating the `source_url` field in the `new_doc` dict returned by `fetch_rulebook`. Fix the scraper, re-run a small backfill for the 22 affected docs only.
- **Acceptance:** DFSA scraper test confirms `new_doc['source_url']` is populated with the leaf-page URL. 22 affected docs backfilled. Regression test ensures all future scrapes include source_url.
- **Bundle 1 progress [2026-05-13]:** Script + tests committed to master via `sprint/A5C1-dfsa-source-url-2026-05-12-overnight` (merge commit `ccfa1c0` on adgm-corpus master). `scripts/backfill_dfsa_source_url.py` is dry-run-by-default; derives source_url from `MODULE_URLS` registry (21/22) plus guidance-index fallback (1/22). `tests/acceptance/test_source_url_invariant.py` adds 1 passing diagnostic + 7 strict xfails (one per source_entity class). Backfill APPLY against corpus.db remains pending — requires explicit interactive authorisation per HG1 discipline.
- **See:** `/tmp/qanun-overnight/a5/A5C1.md`
- **Notes:** Same pattern likely affects FSRA scraper (A1.a refactor); audit A1.a after this lands.

---

### A5.D — content_hash pre-compute on INSERT

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** None
- **Source:** A5 audit memo, 12 May 2026
- **Description:** content_hash is computed in some scraper paths but written via plain INSERT in others, creating opportunities for hash drift. Move hash computation into write_rulebook so every insert produces a consistent hash from the canonical full_text. Reduces surface area for the next A1.h-equivalent bug.
- **Acceptance:** write_rulebook computes content_hash from full_text consistently. Scraper callers can pass through but write_rulebook validates or recomputes. Unit test for the consistency property.

---

### A5.E — version_str canonical type + validator

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** None (low priority per A5 memo)
- **Source:** A5 audit memo, 12 May 2026
- **Description:** version_str format varies across source_entities: FSRA uses `VER12.311025`, DFSA uses `VER7101-26`, El Salvador uses none. Establish per-source_entity expected pattern with validators; reject inserts that don't match.
- **Acceptance:** Validator per source_entity. Existing data audited; any malformed strings surfaced and either fixed or normalised.

---

### A5.F — source_key naming convention enforcement

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** None (lowest priority per A5 memo)
- **Source:** A5 audit memo, 12 May 2026
- **Description:** source_key is constructed inconsistently — some use `{source}_{rulebook}_{slug}`, some use different patterns. Establish canonical construction pattern in the scraper base class.
- **Acceptance:** Canonical helper. All scrapers refactored.

---

### A6 — A1 idempotence test infrastructure — **DONE [2026-05-12]**

- **Status:** Done — `sprint/A6-idempotence-test-2026-05-11-overnight` (adgm-corpus, commit `93dfd30`); merged to master in commit `f443dbb`
- **Size:** Half-day
- **Source:** A1.h investigation memo, 11 May 2026
- **Description:** Two test classes added. `TestIdempotenceMocked` runs against synthetic corpus.db and passes. `TestIdempotenceLive` scaffold gated on `QANUN_RUN_LIVE_IDEMPOTENCE=1` environment variable via `@pytest.mark.skipif`.
- **Acceptance:** ✓ Mocked tests pass on master (2P + 1S verified post-merge). Skipped-test verification confirmed: `pytest -v tests/test_idempotence_refresh.py` shows 2 PASSED + 1 SKIPPED + 0 FAILED + 0 XFAIL.
- **Notes:** Polluted `/tmp/qanun-overnight/idempotence-sandbox/corpus.db` (298MB, written 12 May 17:40 by the inadvertent overnight live run) **deleted as part of A6 merge housekeeping**. Sandbox is clean for A6.LIVE re-exercise.

---

### A6.LIVE — Live idempotence exercise

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** A6 (Done)
- **Source:** A6 deferred sub-item, 12 May 2026
- **Description:** Run the live idempotence exercise: refresh DFSA bulk three times in succession against a fresh sandbox (snapshotted from Hetzner). Assert first run produces non-trivial changes; second and third runs produce 100% unchanged, zero INSERTs.
- **Acceptance:** Live test passes. Result captured in `/tmp/qanun-overnight/A6-idempotence-live-result.md`. Polluted sandbox deleted first.
- **Notes:** Authorise as `Authorise A6-live-idempotence-exercise-<date>`.

---

### A7 — Cross-jurisdiction single-current invariant audit — **DONE [2026-05-12]**

- **Status:** Done — memo at `~/qanun-docs/A7_cross_jurisdiction_invariant_audit.md` (commit `8fc15d9`)
- **Size:** Half-day
- **Source:** Pattern from today's FSRA GEN orphan and DFSA pre-flight, 11 May 2026
- **Description:** Ran the audit across every source_entity. Found 31 orphan rows across 10 rulebooks (vs v1.0's assumption of 1 rulebook with 3 rows).
- **Findings:** Six FSRA rulebooks (GEN, COBS, FUNDS, PRU, MIR, GLO) with 2-5 is_current=1 rows each. Two BVI_FSC rulebooks (BCA, REGS) with duplicate identical captures. UNKNOWN has 11 docs sharing truncated rulebook codes. Each filed as a sub-item below.
- **Cross-cutting finding:** The ingestion path that produced these orphans (28 April stub + 2 May duplicate) deserves its own investigation (filed as A7.ROOT below).

---

### A7.B — FSRA COBS orphan reconciliation — **DONE [2026-05-13]**

- **Status:** Done — interactive apply 2026-05-13 (Bundle 2). Flip-only; section + citation cleanup tracked as A7.B.SECTIONS.
- **Size:** Half-day
- **Dependencies:** None (A1 now on master at `2863b79`)
- **Source:** A7 audit memo + `/tmp/qanun-overnight/a7/A7-COBS.md`
- **Description:** Worst case in the FSRA cluster pre-apply: 5 is_current=1 rows. State: 184 (VER21.010126 legitimate prior, 426 KB, 1871 sections), 2767 (28-Apr stub, 21 KB, 90 sections), 2783 (2-May stub, 7.8 KB, 27 sections), 2787 (2-May duplicate-A, 438 KB, 1906 sections), 2788 (2-May duplicate-B, 444 KB, 1928 sections). Memo §5 prescription applied per-doc; 184 + 2767 + 2783 + 2787 → `is_current=0, superseded_by=2788`; 2788 retained canonical. Note 2787 and 2788 have **different content_hashes** (`b0b4b9c1…` vs `77fbe1fe…`) — picking by size per memo §5 heuristic; memo §9 portal verification deferred to follow-up.
- **Acceptance:** ✓ Rows-affected = 4; invariant count = 1 (doc 2788). `COBS 1.1` resolves to doc 2788 on the is_current=1 join. PRAGMA integrity_check ok. Test `test_single_current_invariant_per_rulebook[FSRA-COBS]` flipped from xfail-strict to passing. Full-suite delta: 680P/1S/18XF → 681P/1S/17XF.
- **Backup:** `/Users/oliver/ADGM/adgm-corpus/backups/corpus_pre_A7_COBS_20260513_082429.db` (sha256 `d199e146…`, integrity ok).
- **Deferred follow-ups:** doc 2788 metadata (A5.C/E); section + citation cleanup (A7.B.SECTIONS below); content_hash vs portal verification (memo §9).

---

### A7.B.SECTIONS — FSRA COBS section + citation cleanup post-flip

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** B1 parser redesign (so cleanup runs against a corrected parser; section-parser non-determinism observed across multiple Bundle 2 rulebooks)
- **Source:** A7-COBS memo §6 deferred from Bundle 2 apply 2026-05-13
- **Description:** Delete archived sections from doc 2787 (1906 rows) and stub sections from docs 2767 (90 rows) and 2783 (27 rows) — total ~2023 rows. Preserve sections for doc 184 (1871 rows, legitimate VER21 historical). Plus citation re-pointing: any `citations` rows with `source_doc_id=2787` or `target_doc_id=2787` need either deletion (if duplicate of existing 2788-anchored citation) or re-anchoring to 2788.
- **Acceptance:** `sections` table contains no rows for COBS doc_ids in {2787, 2767, 2783}; contains rows for {184, 2788}. `citations` table contains no rows referencing 2787 (or those rows have been re-anchored to 2788 with documented per-row decision). PRAGMA integrity_check ok. Full-suite green.
- **Notes:** Deferred from Bundle 2 due to multi-statement shape (memo §6 conditional DELETE) and parallel concern that B1 parser redesign may rationalise what should be parsed in the first place. Cross-reference `/tmp/qanun-overnight/a7/A7-COBS.md` §6 for the precise decision tree on which doc_ids to delete vs preserve.

---

### A7.C — FSRA FUNDS orphan reconciliation — **DONE [2026-05-13, Path A]**

- **Status:** Done — interactive apply 2026-05-13 (Bundle 2; Path A flip-only). Mislabel-of-doc-199 carved out as separate item.
- **Size:** Half-day
- **Dependencies:** None (A1 now on master)
- **Source:** A7 audit memo + `/tmp/qanun-overnight/a7/A7-FUNDS.md` + Bundle 2 in-session forensic
- **Description:** Pre-apply state: 3 is_current=1 rows. Memo §4 framed the case as a 67% size-drop investigation (199 at 873 KB vs 2789 at 283 KB) requiring portal verification. **In-session investigation overturned the framing entirely:** first-300-chars of doc 199's body reads "Prudential – Investment, Insurance Intermediation and Banking Rulebook (PRU) (VER19.010126)" — doc 199 is PRU content mislabeled as FUNDS in the documents.rulebook_code column. Its `VER19.010126` value doesn't fit FUNDS's actual version chain (VER10 / VER11 / VER12); it fits a hypothetical PRU VER19 (also not present in PRU's chain VER02→VER13). Doc 2789's body reads "Fund Rulebook (FUNDS) (VER12.290426)" — legitimate 29 April 2026 re-issuance of FUNDS VER12. The memo's size-drop premise was comparing two unrelated regulations. Path A applied: 199 + 2784 (340-byte stub) → `is_current=0, superseded_by=2789`; 2789 retained canonical FUNDS. Doc 199's `rulebook_code='FUNDS'` mislabel persists on the is_current=0 row — carved out to A7-FUNDS-doc-199-mislabel below.
- **Acceptance:** ✓ Rows-affected = 2; invariant count = 1 (doc 2789). `FUNDS 1.1.1` resolves to doc 2789. PRAGMA integrity_check ok. Test `test_single_current_invariant_per_rulebook[FSRA-FUNDS]` flipped from xfail-strict to passing. Full-suite delta: 683P/1S/15XF → 684P/1S/14XF.
- **Backup:** `/Users/oliver/ADGM/adgm-corpus/backups/corpus_pre_A7_FUNDS_20260513_091106.db` (sha256 `0be275a0…`, integrity ok).
- **Memo §4 outcome:** Hypothesis invalidated. The 67% size-drop reading was apples-vs-oranges. No actual content reduction in FUNDS; current 2789 (283 KB) is the genuine current state, no missing larger doc.
- **Deferred follow-ups:** A7-FUNDS-doc-199-mislabel (correct rulebook_code on doc 199); A7-FSRA-pipeline-size-sanity (memo §9 — fail-loud on <50% size fetches); doc 2789 metadata (A5.C/E).

---

### A7-FUNDS-doc-199-mislabel — Correct PRU-content-in-FUNDS-row mislabel (4 affected docs)

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** Forensic decision on the superseded_by chain for PRU VER19 (which isn't in PRU's canonical chain doc 15 → 2795)
- **Source:** Bundle 2 A7-FUNDS investigation + post-apply protocol-review forensic, 2026-05-13
- **Description:** Systematic PRU-content-in-FUNDS-tagged-row mislabel affecting four docs (64, 121, 189, 199) — all share `Adgm1547_11092_VerNN<date>` slug pattern and contain Prudential Rulebook (PRU) body text. Scraper-side routing bug, not isolated. Per-doc bodies confirm:
  - Doc 64 → `Prudential – Investment, Insurance Intermediation and Banking Rules (PRU) (VER10.250521)`
  - Doc 121 → `Prudential ... (PRU) (VER11.270422)`
  - Doc 189 → `Prudential ... (PRU) (VER12.301122)`
  - Doc 199 → `Prudential ... Rulebook (PRU) (VER19.010126)` (is_current=0 since A7.C Bundle 2 apply)
  All four also have `Adgm1547 11092 VerNN…` title slugs in the documents table, consistent with a single misrouted scraper source. Doc 2789 (the only is_current=1 FUNDS row post-Bundle-2) is the first genuine FUNDS body content in the corpus.
- **Acceptance:** `rulebook_code` corrected to PRU on all four docs (64, 121, 189, 199); `superseded_by` chain decided in a focused follow-up (PRU canonical chain doc 15 → 2795 doesn't include a VER19 entry — doc 199's PRU VER19 may be an off-chain capture; 64/121/189 may slot into a parallel pre-K7 PRU historical chain). Section_refs on these four (currently 100% `OTHER` prefix via K7 carry-forward gap) re-prefixed to `PRU` if A3 carry-forward is in scope at the same time, or annotated as deferred. Forward-looking body-vs-label integrity-check added to prevent recurrence.
- **Notes:** A1 invariant counts is_current=1 per rulebook_code and doesn't catch content-vs-label mismatch. Cross-reference `/tmp/qanun-overnight/a7/A7-FUNDS.md` for the original A7 audit framing (which assumed 199 was a FUNDS capture). Cross-reference **A7-FSRA-pipeline-size-sanity** for the broader pipeline guard against the family of silent-mis-ingest issues. The bundled four-doc correction may also affect any get_rule history queries that currently surface 64/121/189 under FUNDS — they should surface under PRU after this lands (PRU's get_rule history doesn't currently include VER10/VER11/VER12 captures because they're filed elsewhere).

---

### A7-FSRA-pipeline-size-sanity — Fail-loud size-floor for FSRA ingestion

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** None
- **Source:** A7-FUNDS memo §9, 2026-05-13
- **Description:** When the FSRA scraper fetches a rulebook whose full_text length is < 50% of the prior is_current=1 row's full_text length, the pipeline should fail-loud (raise + abort the write), not silent-commit. The 28-April + 2-May FSRA pipeline's stub-shaped captures (340-byte FUNDS, 4.7-KB GEN, 1.5-KB MIR, etc.) all passed unconditionally because no size-sanity floor existed. A1 invariant covers the count side; this addition covers the size side.
- **Acceptance:** FSRA scraper raises `SizeFloorError` (or equivalent) when fetched full_text < 0.5 × prior_full_text. Test covers both the floor-trigger and the floor-pass cases. Register entry A1.h.SIZE-FLOOR or similar.
- **Notes:** Pairs with the existing A1 pre-flight invariant. Defence-in-depth: A1 catches multi-current count; A7-FSRA-pipeline-size-sanity catches partial-fetch silent-commits.

---

### A7-GLOBAL-INVARIANT-FINDINGS — Three multi-current cases beyond the A7 audit

- **Status:** Open
- **Size:** Half-day (investigation) + tbd (remediation, depending on outcome)
- **Dependencies:** None
- **Source:** Bundle 2 close-out, 2026-05-13 — `test_global_single_current_invariant` defence-in-depth test surfaced these
- **Description:** After all 8 known A7 reconciliations applied (MIR, PRU, GEN, BVI-BCA, COBS, GLO, BVI-REGS, FUNDS), the `test_global_single_current_invariant` test still xfails because the defence-in-depth query returns 3 multi-current cases the A7 audit did not catch:
  - `FSRA` + `OTHER` — **65 is_current=1 rows**
  - `ADGM FSRA` + `ADGM-FSRA-F` — **37 is_current=1 rows**
  - `ADGM_RA` + `ADGM-RA-F` — **32 is_current=1 rows**
- **Hypotheses:**
  1. **Legitimate category-bucket cases.** `rulebook_code` here is being used as a *category* (OTHER catch-all; ADGM-FSRA-F = "FSRA Forms"; ADGM-RA-F = "RA Forms") rather than a canonical-rulebook identifier. If so, each row is a distinct document (different form / different consultation paper) that's correctly is_current=1 in its own right, and the A1 single-current invariant doesn't apply. Remediation: refine the global query to exclude category buckets; document the bucket pattern in a new schema-conventions memo.
  2. **Genuine multi-current violations.** Like the A7 cluster but missed by the audit because the audit might have been scoped to "canonical rulebook codes" only. Each bucket would need its own A7-like reconciliation.
  3. **Mix.** Some rows in each bucket are genuine duplicates, others are distinct documents.
- **Acceptance:** First, the investigation that resolves which hypothesis holds (likely Hypothesis 1 based on the bucket naming). Then either query refinement + bucket-pattern memo (if H1), or per-bucket reconciliation items A7.J / A7.K / A7.L (if H2/H3).
- **Notes:** Surfaced via the highest-value regression test working exactly as the A7 cluster overview §6 anticipated ("catches **any** new violation, not just the 8 known ones"). This is the test paying for itself on its first full pass.

---

### A7.D — FSRA PRU orphan reconciliation — **DONE [2026-05-13]**

- **Status:** Done — interactive apply 2026-05-13 (Bundle 2). Flip-only; 2795 metadata backfill deferred to A5.C / A5.E.
- **Size:** Half-day
- **Dependencies:** None (A1 now on master)
- **Source:** A7 audit memo + `/tmp/qanun-overnight/a7/A7-PRU.md`
- **Description:** Three is_current=1 rows reconciled: 15 (legitimate VER13.181223 prior, 864 KB, 1279 sections) and 2772 (28-April ingestion stub, 4.9 KB, 4 sections) flipped to `is_current=0, superseded_by=2795`; 2795 (May 2026 VER14 candidate, 875 KB, 1296 sections — +1.3% section delta from 15) retained as canonical current. Doc 15 section-ref convention is 100% `PRU` prefix (zero `OTHER` — A3 K7 carry-forward concern from memo §10 verified not-applicable).
- **Acceptance:** ✓ Invariant query `COUNT(*) WHERE source_entity='FSRA' AND rulebook_code='PRU' AND is_current=1` = 1 (doc 2795). `PRU 1.1.1` resolves to doc 2795 on the is_current=1 join. PRAGMA integrity_check ok post-COMMIT. Test `test_single_current_invariant_per_rulebook[FSRA-PRU]` flipped from xfail-strict to passing. Full-suite delta: 677P/1S/21XF → 678P/1S/20XF.
- **Backup:** `/Users/oliver/ADGM/adgm-corpus/backups/corpus_pre_A7_PRU_20260513_080421.db` (sha256 `3bfb2dbc…`, integrity ok).
- **Deferred follow-up:** doc 2795 `version_str` / `version_num` / `source_url` remain empty — tracked under A5.C and A5.E. Memo §6 portal lookup for VER14.<minor> + URL is input for that follow-up.

---

### A7.E — FSRA MIR orphan reconciliation — **DONE [2026-05-13]**

- **Status:** Done — interactive apply 2026-05-13 (Bundle 2). Flip-only; 2793 metadata backfill deferred to A5.C / A5.E.
- **Size:** Half-day
- **Dependencies:** None (A1 now on master)
- **Source:** A7 audit memo + `/tmp/qanun-overnight/a7/A7-MIR.md`
- **Description:** Three is_current=1 rows reconciled: 326 (legitimate VER08.110724 prior, 247 KB) and 2770 (28-April ingestion stub, 1.5 KB) flipped to `is_current=0, superseded_by=2793`; 2793 (May 2026 VER09 candidate, 249 KB) retained as canonical current. Section-ref convention identical between 326 and 2793 (both `MIR x.y.z`); A3 K7 OTHER-prefix concern from memo §10.2 verified not-applicable.
- **Acceptance:** ✓ Invariant query `COUNT(*) WHERE source_entity='FSRA' AND rulebook_code='MIR' AND is_current=1` = 1 (doc 2793). `MIR 1.1.1` resolves to doc 2793 on the is_current=1 join. PRAGMA integrity_check ok post-COMMIT. Test `test_single_current_invariant_per_rulebook[FSRA-MIR]` flipped from xfail-strict to passing. Full-suite delta: 676P/1S/22XF → 677P/1S/21XF.
- **Backup:** `/Users/oliver/ADGM/adgm-corpus/backups/corpus_pre_A7_MIR_20260513_075740.db` (sha256 `08f02382…`, integrity ok).
- **Deferred follow-up:** doc 2793 `version_str` and `source_url` remain empty — tracked under A5.C (provenance backfill at 2,099-row scale) and A5.E (version_str validator). Memo §10.1 portal lookup (correct VER number for May 2026 MIR) is the input for this follow-up.

---

### A7.F — FSRA GLO orphan reconciliation — **DONE [2026-05-13]**

- **Status:** Done — interactive apply 2026-05-13 (Bundle 2). Flip-only; section + citation cleanup tracked as A7.F.SECTIONS.
- **Size:** Half-day
- **Dependencies:** None (A1 now on master)
- **Source:** A7 audit memo + `/tmp/qanun-overnight/a7/A7-GLO.md`
- **Description:** Tied-worst case in FSRA cluster (5 currents, same shape as COBS). State: 169 (VER25.010126 legitimate prior, 159 KB, 79 sections), 2769 (28-Apr stub, 1.4 KB, 4 sections), 2785 (2-May stub, 2 KB, 9 sections), 2791 (2-May duplicate-A, 160 KB, 76 sections), 2792 (2-May duplicate-B, 161 KB, 76 sections). Memo §5 prescription applied; 169 + 2769 + 2785 + 2791 → `is_current=0, superseded_by=2792`; 2792 retained canonical. 2791 and 2792 have **different content_hashes** (`7b0595aa…` vs `dfa39e83…`) despite same parser run; size-heuristic pick per memo.
- **Acceptance:** ✓ Rows-affected = 4; invariant count = 1 (doc 2792). GLO-prefixed sections on is_current=1 GLO docs resolve to doc 2792 only. `GLO 1.1.1` is present at rule level on 2792 (glossary parser worked). PRAGMA integrity_check ok. Test `test_single_current_invariant_per_rulebook[FSRA-GLO]` flipped from xfail-strict to passing. Full-suite delta: 681P/1S/17XF → 682P/1S/16XF.
- **Backup:** `/Users/oliver/ADGM/adgm-corpus/backups/corpus_pre_A7_GLO_20260513_082626.db` (sha256 `0fd479cd…`, integrity ok).
- **Glossary-specific note (memo §10):** Pre-apply diagnostic of distinct term entries across competing currents not performed — judged out of scope for the flip-only apply; tracked as part of A7.F.SECTIONS investigation when archived sections are cleaned up.
- **Deferred follow-ups:** doc 2792 metadata (A5.C/E); section + citation cleanup (A7.F.SECTIONS below); content_hash vs portal verification (memo §9).

---

### A7.F.SECTIONS — FSRA GLO section + citation cleanup post-flip

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** B1 parser redesign (so cleanup runs against a corrected parser)
- **Source:** A7-GLO memo §6 deferred from Bundle 2 apply 2026-05-13
- **Description:** Delete archived sections from doc 2791 (76 rows) and stub sections from docs 2769 (4 rows) and 2785 (9 rows) — total 89 rows. Preserve sections for doc 169 (79 rows, legitimate VER25 historical). Plus citation re-pointing for any `citations` rows with `source_doc_id=2791` or `target_doc_id=2791` — either delete (if duplicate of 2792-anchored equivalent) or re-anchor to 2792. Glossary-specific: pre-cleanup, verify 2791 and 2792 term-entry sets are near-identical (memo §10 concern); divergence > 1% flag for review.
- **Acceptance:** `sections` table contains no rows for GLO doc_ids in {2791, 2769, 2785}; contains rows for {169, 2792}. `citations` table re-anchored or cleared for 2791. PRAGMA integrity_check ok. Full-suite green. Glossary determinism check passed.
- **Notes:** Smaller scale than A7.B.SECTIONS (~89 rows vs ~2023). Can likely be applied together with A7.B.SECTIONS in a single follow-up session. Cross-reference `/tmp/qanun-overnight/a7/A7-GLO.md` §6.

---

### A7.G — BVI_FSC BCA duplicate reconciliation — **DONE [2026-05-13]**

- **Status:** Done — interactive apply 2026-05-13 (Bundle 2). Conservative shape: archive (flip) the duplicate; preserve archived row's sections.
- **Size:** Half-day
- **Dependencies:** None (A1 now on master)
- **Source:** A7 audit memo + `/tmp/qanun-overnight/a7/A7-BVI-BCA.md`
- **Description:** Three rows for BVI_FSC BVI-BCA, all sharing identical content_hash `f9af6baf…` and identical 472,544-byte full_text. Pre-apply state: 2573 (Mar 31, already is_current=0, 135 sections), 2662 (Apr 3, is_current=1, 0 sections), 2756 (Apr 15, is_current=1, 18 sections). Memo §5 prescription applied: 2662 → `is_current=0, superseded_by=2756`; 2756 retained as canonical current; 2573's optional `superseded_by` backfill skipped (kept truly-flip-only consistent with the bundle pattern).
- **Acceptance:** ✓ Rows-affected = 1; invariant count = 1 (doc 2756). `BVI-BCA Part I` resolves to doc 2756 on the is_current=1 join. PRAGMA integrity_check ok. Test `test_single_current_invariant_per_rulebook[BVI_FSC-BVI-BCA]` flipped from xfail-strict to passing. Full-suite delta: 679P/1S/19XF → 680P/1S/18XF.
- **Backup:** `/Users/oliver/ADGM/adgm-corpus/backups/corpus_pre_A7_BVI_BCA_20260513_081903.db` (sha256 `9efbc4c3…`, integrity ok).
- **B-cluster observation captured:** Canonical 2756 has only 18 sections while archived 2573 has 135 (same content_hash). Section-parser produced different output across runs of byte-identical content. Not blocking A7-invariant — a determinism concern that belongs with B-cluster (parser-redesign B1). Worth a follow-up register item if patterns persist.
- **Deferred follow-up:** doc 2756's metadata gaps (version_str/source_url) — A5.C. Hetzner-side `A7-BVI-content-hash-dedup` register item from memo §9 still Open (BVI scraper currently lacks the dedup that would prevent this recurring).

---

### A7.G.SECTIONS — BVI_FSC BVI-BCA section + citation cleanup post-flip

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** B1 parser redesign (so cleanup runs against a corrected parser; the parser non-determinism that produced 135 vs 18 vs 0 sections on byte-identical content is the underlying B-cluster concern)
- **Source:** Bundle 2 A7-BVI-BCA close-out, 2026-05-13 (retroactively opened alongside A7.B.SECTIONS / A7.F.SECTIONS)
- **Description:** Doc 2573 (BVI_FSC BVI-BCA, is_current=0 since pre-Bundle-2) has 135 archived sections while canonical current 2756 has only 18, despite both rows sharing content_hash `f9af6baf…` (byte-identical full_text). The 135-vs-18 asymmetry indicates section-parser non-determinism across runs, not real content divergence. Cleanup decision tree: (a) delete 2573's 135 archived sections (safest — they're orphaned from is_current=1 joins anyway, and the canonical 2756 has its own 18 sections); (b) preserve them with annotation explaining they're parser-output-from-the-same-content (informational only); (c) re-parse the canonical 2756 with the post-B1 parser and compare against 2573 + 2662 to understand which run was correct, then standardize. Plus citation re-pointing on 2662's archived row (also flipped in Bundle 2).
- **Acceptance:** Either `sections` table has consistent per-doc counts for the BVI-BCA chain (probably via deletion of archived sections), or there's a documented annotation explaining the asymmetry and the section-parser determinism concern is filed as a B-cluster item with its own remediation. PRAGMA integrity_check ok. Full-suite green.
- **Notes:** Cross-reference `/tmp/qanun-overnight/a7/A7-BVI-BCA.md` and the matching B-cluster determinism concern. Bundle 2 close-out captured this finding alongside the COBS/GLO ones (A7.B.SECTIONS / A7.F.SECTIONS) since they share the parser-determinism root cause.

---

### A7.H — BVI_FSC REGS duplicate reconciliation — **DONE [2026-05-13, Path (b) inverted]**

- **Status:** Done — interactive apply 2026-05-13 (Bundle 2). **Path (b) inverted** from memo §5 prescription.
- **Size:** Half-day
- **Dependencies:** None (A1 now on master)
- **Source:** A7 audit memo + `/tmp/qanun-overnight/a7/A7-BVI-REGS.md` + Bundle 2 in-session investigation
- **Description:** Pre-apply state: 2 is_current=1 rows (2589 from 1 Apr, 25,931 bytes, 18 sections, source_url populated, formal S.I. title; 2664 from 3 Apr, 25,944 bytes, 0 sections, empty source_url, malformed-normalised title). Memo §5 prescribed flipping 2589 (the "older convention"), but in-session investigation showed: (a) first 500 chars byte-identical between the two — 13-byte delta is whitespace/footer noise, not a regulatory update; (b) 2589 carries source_url provenance while 2664 has empty source_url; (c) 2589 has 18 parsed `BVI-REGS Reg.N` sections while 2664 has zero — flipping per memo would have left BVI-REGS with zero queryable sections; (d) 2589's title is the formal "Investment Business (Approved Managers) Regulations 2012 (S.I. 2012 No. 54)" while 2664's is the malformed "Bvi Investment Business Approved Managers Regs". Memo §3's "newer convention is better" rationale was based on title-cleanliness alone; deeper evidence inverted the call. **Apply: flip 2664, retain 2589 as canonical.**
- **Acceptance:** ✓ Rows-affected = 1; invariant count = 1 (doc 2589). `BVI-REGS Reg.1` (one of 18) resolves to doc 2589 on the is_current=1 join. PRAGMA integrity_check ok. Test `test_single_current_invariant_per_rulebook[BVI_FSC-BVI-REGS]` flipped from xfail-strict to passing. Full-suite delta: 682P/1S/16XF → 683P/1S/15XF.
- **Backup:** `/Users/oliver/ADGM/adgm-corpus/backups/corpus_pre_A7_BVI_REGS_20260513_090242.db` (sha256 `d39135ae…`, integrity ok).
- **Why memo was wrong here:** Memo §3 evaluated "newer scraper run = better" on title-convention surface only. The actual scraper-run-quality evidence (provenance + sections) points the other way: 2664 looks like a partial re-ingestion that lost source path and parser output. The title-cleanliness preference is a separate concern from canonical-version selection.
- **Deferred follow-ups:** Title hygiene — the malformed "Bvi Investment Business…" pattern is the seed for the **A7-BVI-title-extraction-audit** register item (proposed by memo §9 and now opened below). NULL `updated_at` on 2589 from memo §6 — superseded by Bundle 2 setting `updated_at = datetime('now')` on the touched docs (2664), so 2589 still has its empty `updated_at`; tracked as part of A5.E hygiene scope.

---

### A7-BVI-title-extraction-audit — Audit BVI title normalisation across all BVI_FSC docs

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** None
- **Source:** A7-BVI-REGS memo §9 + Bundle 2 in-session investigation, 2026-05-13
- **Description:** Doc 2664's title `Bvi Investment Business Approved Managers Regs` is a malformed title-case normalisation — "Bvi" should be "BVI" (acronym), "Regs" is a truncated "Regulations", and the full S.I. citation `(S.I. 2012 No. 54)` was dropped during normalisation (compare to doc 2589's preserved full title). The BVI scraper's title-extraction logic appears to apply lossy normalisation between runs. Audit: enumerate all `BVI_FSC` docs, categorise titles into well-formed / malformed-normalised / other, identify the offending scraper rev. Tighten the normalisation: preserve acronyms (BVI), preserve canonical regulation names, preserve citation suffixes.
- **Acceptance:** Audit report in `~/qanun-docs/A7_bvi_title_audit.md`. Recommended fix landed in BVI scraper or a normalisation utility. Regression test ensures titles like "Bvi" → "BVI" and S.I. citations are preserved. Re-run titles audit; zero malformed survivors.
- **Notes:** Cross-reference A5.A (`rulebook_code` normalisation) — same family of convention-drift concern but for title. A7-BVI-content-hash-dedup (proposed in A7-BVI-BCA memo §9) is the upstream fix that would prevent the duplicate-with-different-title problem from happening in the first place.

---

### A7.I — UNKNOWN source_entity truncated rulebook code reconciliation

- **Status:** Open
- **Size:** Day
- **Dependencies:** None (A1 now on master)
- **Source:** A7 audit memo
- **Description:** 11 docs in source_entity='UNKNOWN' share truncated rulebook_code values. These were ingested with insufficient metadata to classify properly. Investigation: identify the real source entity per doc, reclassify or remove.
- **Acceptance:** All UNKNOWN docs either reclassified to a real source_entity or removed with documented reason. UNKNOWN source_entity count drops to whatever's truly unclassifiable (ideally zero).

---

### A7.ROOT — Ingestion path root-cause investigation

- **Status:** Open
- **Size:** Day
- **Dependencies:** A7 (Done) provides starting evidence
- **Source:** A7 audit cross-cutting finding, 12 May 2026
- **Description:** The orphan pattern clusters around two dates: 28 April (stub-shaped captures) and 2 May (duplicate captures). Investigate what ingestion process ran on those dates, why the existing safeguards didn't catch the duplicates, what changed. Document so it doesn't recur once the A1 invariant is in place.
- **Acceptance:** Memo in `~/qanun-docs/` identifying the offending ingestion path(s), confirming the A1 invariant would have prevented recurrence (or proposing additional safeguards if not).

---

# Category B — Content Coverage

What the corpus actually contains.

---

### B1 — Structure parser rule-level extraction redesign (Problem 2) — **REFRAMED**

- **Status:** Open — superseded sizing from "Multi-day depending on hypothesis verification" to "Week"
- **Size:** Week (revised from v1.0 Multi-day)
- **Dependencies:** None
- **Source:** Quick Lookup screenshots, morning of 11 May 2026; B1 PDF inspection memo at `~/qanun-docs/B1_parser_hypothesis_verification.md` (12 May)
- **Description:** **HYPOTHESIS REFUTED.** The CCD-suggested "parser only promotes rule numbers when lettered sub-clauses follow" hypothesis turned out to be wrong. The four GEN 3.5.X sub-rules that appeared "captured" were spurious matches against body-text Guidance-paragraph references, not real captures. The real rules in FSRA PDFs use TITLE+(1)(2)(3) format **without inline rule numbers as line prefixes**. The current SUB_RULE_RE regex literally cannot find them because they don't appear in the form the regex looks for. This is a parser redesign, not a regex tweak.
- **Acceptance:** New parser correctly identifies rule numbers in TITLE+(1)(2)(3) format. Test case: `get_rule('GEN 3.5.1')` returns rule text including the outsourcing/appointed-representative rule. Comprehensive test against FSRA GEN with full chapter 3 expected section_refs. Re-run FSRA GEN canary after parser fix and B4 bulk refresh.
- **Notes:** This is the single largest reframed item in v1.1. The launch timeline grows by ~week as a result. Need a focused session to (a) characterise the actual rule-format structure in FSRA PDFs, (b) design the new parser strategy, (c) implement, (d) test against multiple rulebooks. Until B1 lands, FSRA Quick Lookup quality remains compromised — Problem 2 is unsolved.

---

### B2 — DFSA sourcebook handling

- **Status:** Open (design memo Done; implementation Open)
- **Size:** Multi-day (5-6 days per B2 design memo)
- **Dependencies:** B3 (Done — inventory reconciliation complete)
- **Source:** A1 bulk regression, 11 May 2026; design memo at `~/qanun-docs/B2_sourcebook_handler_design.md` (commit `db6ee7c`)
- **Description:** Design memo recommends strategy pattern with three parser variants: (1) standard X.Y.Z dots for FPR/PRS/RAR, (2) hyphenated X-Y-Z for RPP, (3) chapter-only with inline content for CMC. PRU's entiresection URL returns empty body and needs alternative URL discovery.
- **Acceptance:** All six DFSA sourcebooks (PRU, CMC, RPP, FPR, PRS, RAR) refresh cleanly. Each produces non-trivial section count. Prior is_current=1 docs flipped appropriately. Single-current invariant preserved.
- **Notes:** Strategy pattern design lets each sourcebook have its own parser without contaminating the rulebook scraper.

---

### B3 — DFSA inventory reconciliation — **DONE [2026-05-12]**

- **Status:** Done — `~/qanun-docs/dfsa_inventory_authoritative.md` (commit `d2f4413`)
- **Size:** Day
- **Source:** A1 bulk regression + A1 design notes, 11 May 2026
- **Findings:** All 22 MODULE_URLS entries return HTTP 200. Master TR index lists 21 module-shaped paths; PRU is the lone "hidden sourcebook" (URL works, master index doesn't list). No new modules to add. Six sourcebooks identified: CMC, FPR, PRS, PRU, RAR, RPP. RPP's slug uses `-edition` instead of `-verN-NN` (B2 handler input).

---

### B4 — FSRA full bulk refresh

- **Status:** Blocked
- **Size:** Half-day
- **Dependencies:** **B1 (now sized at week)**, A1 (on master), A2 + A7.B-A7.F (FSRA orphan reconciliations)
- **Source:** Sprint A section, 11 May 2026; revised in v1.1 to depend on B1 not just need-B1
- **Description:** Apply corrected A1 scraper to all FSRA rulebooks. Under the no-knowingly-broken principle, this cannot proceed until B1's parser redesign lands — otherwise the refresh propagates the current rule-level extraction gap to fresh docs.
- **Acceptance:** Same shape as today's DFSA mini-canary + bulk: 6-step per-module verification, invariant query empty, corpus state summary written. GEN 3.5.1 retrievable via `get_rule` after refresh (confirming B1's parser fix landed).
- **Notes:** B1 reframing makes this item the longest blocked item in the register.

---

### B5 — A2: DIFC primary legislation ingestion

- **Status:** Open
- **Size:** Week
- **Dependencies:** None
- **Source:** SOW Section A2, 11 May 2026 sprint state
- **Description:** Unchanged from v1.0. Ingest DIFC Companies Law, Personal Property Law, Insolvency Law, etc. Requires scraper design, parser handling for legislation-shaped content, embedding, MCP registration.
- **Acceptance:** DIFC primary legislation queryable via search_corpus and get_rule with Tier 1 classification.

---

### B6 — A3: Voyage re-embedding

- **Status:** Blocked
- **Size:** Day
- **Dependencies:** B4 (Blocked), B2, B5
- **Source:** SOW Section A3
- **Description:** Re-embed all docs in Pinecone using Voyage Law-2. Must run locally (Voyage IP-blocks Hetzner — see E9.PROXY for the proxy-mode alternative). Critical: K16 FSRA→ADGM_RA metadata migration on 18 docs / 248 vectors must NOT be re-flipped.
- **Acceptance:** All is_current=1 docs have current vectors in Pinecone. K16 metadata preserved. Vector count matches sections count.
- **Notes:** E9.PROXY (the Cloudflare proxy mode recovered from the lowercase clone) may unblock running this from Hetzner directly, which would simplify the runtime.

---

### B7 — A4: Portability map seeding

- **Status:** Blocked
- **Size:** Day
- **Dependencies:** B6
- **Source:** SOW Section A4
- **Description:** Unchanged from v1.0. Populate section_portability_maps via Anthropic LLM + corpus search; human review before activation.

---

### B8 — DFSA inline citation maps

- **Status:** Open
- **Size:** Multi-day
- **Dependencies:** None
- **Source:** A1 mini-canary observation, 11 May 2026
- **Description:** Build `_CANONICAL_TARGET_MAP` and `_SHORTHAND_MAP` in citation_extractor.py for each of the 21 DFSA modules. Affects "see also" cross-reference UX in Quick Lookup and Studio's citation map output for DFSA content.
- **Acceptance:** Inline citation maps populated for all 21 DFSA modules. Re-run citation extraction; verify non-trivial citation count per doc.
- **Notes:** C1 (Done — design memo) recommends Option C: hook in write_rulebook with extract_inline_citations=True default. Phased: FSRA first, DFSA after B8 lands. So B8 unblocks the C1 implementation for DFSA.

---

### B9 — Doc 2790 metadata recovery — **DONE [2026-05-11]**

- **Status:** Done — folded into A2's scope, as noted in v1.0
- **Source:** A1-FSRA-GEN-diagnostic, 11 May 2026

---

# Category C — Code Quality

Known-to-be-wrong code.

---

### C1 — `write_rulebook` hook for legacy `extract_citations` — DESIGN DONE

- **Status:** Open (design memo Done; implementation Open)
- **Size:** Half-day (implementation only, per memo)
- **Dependencies:** None for FSRA; B8 for DFSA
- **Source:** A1 mini-canary observation, 11 May 2026; design memo at `~/qanun-docs/C1_extract_citations_hook_design.md` (commit `e997553`)
- **Description:** Memo recommends Option C: write_rulebook calls extract_inline_citations(extract_inline_citations=True) by default with opt-out kwarg. Idempotent helper. Phased: FSRA first; DFSA after B8 lands inline maps.
- **Acceptance:** Hook implemented per Option C. FSRA citation extraction during apply produces same results as the current separate-script path. Regression test verifies count parity.

---

### C2 — Orchestrator NEW vs AMENDED label fix — **DONE [2026-05-12]**

- **Status:** Done — `sprint/C2-label-2026-05-11-overnight` (adgm-corpus, commit `d0fd7b9`); merged to master in commit `6a2ae1a`
- **Acceptance:** ✓ NEW/AMENDED/unchanged labels under prefixed convention covered by 2 new regression tests. Post-merge full suite: 664P/5XF/0F clean.

---

### C3 — "just-flipped FSRA documents" typo — **DONE [2026-05-12]**

- **Status:** Done — `sprint/C3-typo-2026-05-11-overnight` (adgm-corpus, commit `d6c57dc`); merged to master in commit `7d01968`
- **Acceptance:** ✓ Investigation showed the hardcoded "FSRA" string didn't actually exist in current code — orchestrator already interpolates jurisdiction correctly. Deliverable pivoted to `TestJurisdictionLabelling` regression class (3 tests) locking in the correct behaviour. Post-merge full suite: 667P/5XF/0F clean (first try, no flake).
- **Notes per Self-Assessment:** This was the right pivot — closing an item by "we found it doesn't apply" leaves no protection against future regression. Regression tests provide structural protection.

---

### C4 — Reextract WAL-checkpoint crash — **DONE [2026-05-12]**

- **Status:** Done — `sprint/C4-wal-checkpoint-2026-05-11-overnight` (adgm-corpus, commit `74b7923`); merged to master in commit `95d925d`; memo `~/qanun-docs/C4_wal_checkpoint_investigation.md` (commit `f7ef5d3`)
- **Acceptance:** ✓ Fix: reorder (commit() first, checkpoint after) + try/except suppression with log warning. 1 new regression test passes. Post-merge full suite: 675P/1S/5XF/0F clean.

---

### C5 — `--rulebook` filter ergonomics — **DONE [2026-05-12]**

- **Status:** Done — `sprint/C5-rulebook-filter-2026-05-11-overnight` (adgm-corpus, commit `03f55b4`); merged to master in commit `53e0f87`
- **Acceptance:** ✓ `--rulebook AUT` and `--rulebook AUD` both match. Friendly warning for unknown codes. 4 new tests pass. Post-merge behaviour smoke check: `_normalised_rulebooks(('AUT',), 'AUD')` returns `('AUT',)` — alias-aware bidirectional match confirmed on master.

---

### C6 — DFSA `MODULE_URLS` refresh script

- **Status:** Open
- **Size:** Day
- **Dependencies:** None
- **Source:** A1.b design memo, 11 May 2026
- **Description:** Unchanged from v1.0. Maintenance script that re-crawls DFSA master index and updates hardcoded URLs when DFSA bumps version segments.

---

### C7 — DFSA Drupal selector robustness — **DONE [2026-05-12]**

- **Status:** Done — `sprint/C7-drupal-robust-2026-05-11-overnight` (adgm-corpus, commit `b7c9135`); merged to master in commit `6d9328b`
- **Acceptance:** ✓ New `_find_main_container` cascades through `<main>`, `[role=main]`, `#main-content`, `[id^="main-"]`. 5 layout-variant tests pass. Post-merge behaviour smoke check verified cascade across all 4 locator shapes plus negative case. No DFSA-test regressions.

---

### C8 — SOW v3 schema-drift reconciliation — **DONE [2026-05-12]**

- **Status:** Done — memo `~/qanun-docs/schema_canonical_vs_sow.md` (commit `4799751`)
- **Findings:** Authoritative map of 8 known SOW → production renames. Memo recommends adding a "production schema reference appendix" for the next SOW reissue.
- **See:** C8.APPENDIX below for the follow-up

---

### C8.APPENDIX — SOW schema reference appendix

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** None
- **Source:** C8 memo recommendation, 12 May 2026
- **Description:** Add a "Production Schema Reference" appendix to the next SOW reissue. Documents the canonical production schema names (per `~/qanun-docs/schema_canonical_vs_sow.md`) so future SOW work references the live names rather than guessed ones.
- **Acceptance:** Appendix drafted and ready for inclusion in the next SOW version.

---

### C9 — Convention check pattern for scraper pre-flight — **DONE [2026-05-12]**

- **Status:** Done — memo `~/qanun-docs/scraper_authoring_guide.md` (commit `e875f0e`)
- **Deliverable:** Canonical pre-flight convention-check pattern (using A1 invariant as reference) + 6-section author's checklist + anti-pattern enumeration from today's bugs.

---

### C10 — Pipefail standardisation — **DONE [2026-05-12]**

- **Status:** Done — `~/qanun-docs/deploy_command_patterns.md` (qanun-docs main `39141ee`)
- **Notes:** Audit showed no untrapped `| tee` patterns currently exist in any of the three repos. Existing patterns are protected. Deliverable is the doc; no code change needed.

---

### C11 — TestPerformanceQuickSearch flake investigation

- **Status:** Open
- **Size:** Half-day (diagnostic) + Half-day (fix, depending on root cause)
- **Dependencies:** None
- **Source:** Master integration session, 12 May 2026 — fired on 3 of 7 on-branch runs (C5, C2, C4)
- **Description:** `tests/acceptance/test_section_17.py::TestPerformanceQuickSearch::test_performance_quick_search` is order-dependent: passes in isolation (~3.5s), fails when full suite runs (timing/threshold assertion fails). Fired during today's integration on C5, C2, and C4 on-branch runs; all cleared on retry. C3, C7, A6 on-branch runs silent. Post-merge runs all clean first-try. The on-branch vs post-merge split is itself diagnostic: when run after a slightly different test set (sprint branch's pre-master baseline), the trigger fires; when run against the full post-merge master, it doesn't.
- **Acceptance:** Diagnostic phase: identify the trigger test (the test or fixture that immediately precedes test_performance_quick_search when it fires vs when it doesn't). Run `pytest --collect-only --quiet` to see run order; run `pytest --durations=20` over multiple iterations to identify timing patterns; bisect the test set to find the minimal pre-context that triggers. Fix phase: either (a) per-test fixture cleanup that resets the state the trigger leaves dirty, (b) explicit test ordering directive (`pytest-order` plugin), (c) timing-tolerance adjustment if the test's threshold is too tight for the contaminated state, or (d) xfail-strict with documented unxfail condition if root cause is unfixable.
- **Bundle 1 progress [2026-05-13]:** Near-term mitigation landed via `sprint/flake-perf-test-2026-05-12-overnight` (merge commit `059ad05` on adgm-corpus master): threshold raised from 5s to 10s in `tests/acceptance/test_section_17.py`. Per overnight diagnostic, the flake is cold-start network variance (first Voyage embed + first Pinecone TLS/gRPC handshake) rather than order-dependency — original hypothesis refuted. The 10s threshold should suppress the fire rate substantially while preserving genuine perf-regression coverage. Proper C11.A redesign (mock the network calls; split into unit + e2e integration-marker) remains Open.
- **See:** `/tmp/qanun-overnight/flake/flake-diagnostic.md`
- **Notes:** Contaminates every full-suite run including future integration sessions. Not blocking specific feature work but erodes trust in green/red signal during sessions. Listed in phase-2-backlog.md (qanun-docs main).

---

### C12 — Prompt-drafting discipline for verification commands

- **Status:** Open (initial discipline already in memory; codification + checklist pending)
- **Size:** Half-day
- **Dependencies:** None
- **Source:** Master integration session, 12 May 2026 — three caught prompt-vs-reality mismatches
- **Description:** Three meta-findings caught during the master integration session via halt-and-surface:
  1. **Smoke-check import path**: A1-invariant smoke check used `from adgm_corpus.storage.db import MultiCurrentInvariantError`; actual location is `adgm_corpus.collection.scrapers.adgm_rulebooks`. Drafted by conceptual placement, not by inspecting actual code.
  2. **Sprint-branch arithmetic**: C5 verification expected on-branch count of 662, but on-branch count is `base-baseline + own-delta = 659`. The 662 number is `current-master + own-delta` post-merge. Conflation of two distinct numbers.
  3. **Diff inspection target**: C3 pre-merge check used `git diff master..origin/sprint/C3` to verify "no production files modified"; the symmetric diff includes foundation-cut artefacts (master commits the branch was cut before). Correct check is `git show <branch-sha> --stat --name-only` for commit-contribution inspection.
- **Mitigation already landed in memory (#18, #19):** Draft verification commands against actual code on a representative checkout, never by analogy. Use `git show <sha>` for commit contribution, not `git diff master..branch`. On-branch vs post-merge arithmetic both belong in verification matrices.
- **Remaining work:** (a) Formalise a one-page integration-prompt-drafting checklist in `~/qanun-docs/integration_prompt_checklist.md` covering the above mistake shapes plus any further patterns that surface. (b) Apply the checklist as a pre-flight step before every future integration prompt is sent to CCD. (c) Track new mistake shapes as they're caught (each instance is a free lesson and worth recording).
- **Acceptance:** Checklist exists in `~/qanun-docs/`. Referenced in any future integration prompt's preamble. Phase-2-backlog updated when new mistake shapes are caught.
- **Notes:** Three caught mismatches in one session is enough signal to make this a structural priority. The pattern: prompt-author drafts verification commands by projecting expected outcomes rather than inspecting actual state. Halt-and-surface catches it; checklist makes it harder to draft poorly in the first place.

---

# Category D — Feature Completion

Sprint sections not yet landed.

---

### D1 — M-section completion

- **Status:** Open (M2-M5 deployed; M1 staged; M3/M4/M6 deploys pending)
- **Size:** Day
- **Source:** Overnight sprint state, 10-11 May 2026
- **Description:** Unchanged from v1.0.

---

### D2 — Q1-Q5 deploy

- **Status:** Open
- **Size:** Half-day
- **Source:** Overnight sprint state, 10-11 May 2026
- **Description:** Unchanged from v1.0.

---

### D3 — C-section synthesis completion

- **Status:** Open
- **Size:** Day
- **Dependencies:** D2
- **Description:** Unchanged from v1.0.

---

### D4 — B1 parser + B2 dry-run deployment

- **Status:** Open
- **Size:** Half-day
- **Description:** Unchanged from v1.0.

---

### D5 — E1 deployment + E2 scaffold completion

- **Status:** Open
- **Size:** Half-day
- **Description:** Unchanged from v1.0.

---

### D6 — F1 + F4 deployment

- **Status:** Open
- **Size:** Half-day
- **Description:** Unchanged from v1.0.

---

### D7 — F2 templates

- **Status:** Open
- **Size:** Day
- **Description:** Unchanged from v1.0. (Note: not to be confused with F2 the test-failure item, which is Done.)

---

### D8 — F3 build + deploy

- **Status:** Blocked
- **Size:** Day
- **Dependencies:** D1 (M1)
- **Description:** Unchanged from v1.0.

---

### D9 — D-section frontend work (8 tasks)

- **Status:** Open
- **Size:** Multi-day
- **Description:** Unchanged from v1.0.

---

### D10 — Master integration session — **DONE [2026-05-12]**

- **Status:** Done — 10 sprint branches merged across 3 repos
- **Size:** Day (actual: interactive session, several hours, with per-merge gate discipline)
- **Source:** Sprint state across multiple sessions
- **Merge SHAs:**
  - adgm-corpus master @ `95d925d` (final HEAD)
    - `913f93a` — foundation merge (sprint/A1-scrapers-2026-05-11 carrying A1.a–A1.h overnight work)
    - `2863b79` — A1-invariant merge
    - `53e0f87` — C5 merge
    - `6a2ae1a` — C2 merge
    - `7d01968` — C3 merge
    - `6d9328b` — C7 merge
    - `f443dbb` — A6 merge
    - `95d925d` — C4 merge
  - qanun-api main @ `b179bd2` (F2 merge)
  - qanun main @ [F1 merge SHA — see integration progress log]
- **Acceptance:** ✓ All 10 sprint branches merged with `--no-ff`. First-parent topology preserved on each repo. Sprint branches retained on origin (no deletion). No force-pushes. Test counts: adgm-corpus 675P/1S/5XF, qanun-api 41P/1S/4XF/0F, qanun 5 vitest smoke tests passing. Three caught prompt-vs-reality mismatches via halt-and-surface (filed as C12).
- **Notes:** Foundation merge (913f93a) was added during the session — sprint branches were cut from `sprint/A1-scrapers-2026-05-11 @ 70f3cc1`, not from master, so a foundation merge was needed to preserve the per-item audit story. The integration session caught and resolved three meta-findings about prompt drafting that are now in memory (#18, #19) and filed as C12.

---

### D11 — G1 smoke run against api.qanun.io

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** D10
- **Description:** Unchanged from v1.0.

---

### D12 — Tester onboarding

- **Status:** Blocked
- **Size:** Half-day
- **Dependencies:** All of A, B, C, D, E, F categories
- **Description:** Unchanged from v1.0.

---

# Category E — Operational Hygiene

---

### E1 — API key rotation

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** None
- **Description:** Unchanged from v1.0 (overdue since 12 May per the 48-hour Section 0 spec).

---

### E2 — Tier 0 wip-branch triage

- **Status:** Open
- **Size:** Day
- **Description:** Unchanged from v1.0.

---

### E3 — Empty ~/LLM-Legal-Council repo cleanup

- **Status:** Open
- **Size:** ≤1 hour
- **Description:** Unchanged from v1.0.

---

### E4 — Oliver OS git remote PAT removal

- **Status:** Open
- **Size:** ≤1 hour
- **Description:** Unchanged from v1.0.

---

### E5 — Three-way vault drift

- **Status:** Open
- **Size:** Day
- **Description:** Unchanged from v1.0.

---

### E6 — b5a5fcc orphan branch investigation

- **Status:** Open
- **Size:** Half-day
- **Description:** Unchanged from v1.0.

---

### E7 — MKT section-parsing regression

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** Possibly B2 or related parser work
- **Description:** Unchanged from v1.0. May have been resolved by DFSA bulk (MKT got 690 sections in the bulk); verify before treating as separate work.

---

### E8 — `~/qanun-api` lowercase duplicate cleanup — **INVESTIGATION DONE**

- **Status:** Open — investigation Done, deletion still pending authorisation
- **Size:** Half-day (delete; investigation Done)
- **Dependencies:** None
- **Source:** QANUN_STATE_2026-05-10 audit; investigation memo `~/qanun-docs/E8_E9_lowercase_repo_cleanup_plan.md` (commit `376b2ea`)
- **Description:** Investigation confirms safe to delete — 7 worktrees, all with zero unique commits vs origin/main. No legitimate work at risk.
- **Acceptance pending:** Explicit Authorise E8-delete-lowercase-qanun-api authorisation before deletion (HG6 prohibits autonomous deletes).

---

### E9 — `~/adgm-corpus` lowercase duplicate cleanup — **INVESTIGATION REVEALED UNIQUE WORK**

- **Status:** Open — **investigation showed cleanup CANNOT proceed yet**
- **Size:** Day (preservation work) + Half-day (delete, after preservation)
- **Dependencies:** E9.PROXY must land first
- **Source:** QANUN_STATE_2026-05-10 audit; investigation memo `~/qanun-docs/E8_E9_lowercase_repo_cleanup_plan.md` (commit `376b2ea`)
- **Description:** Investigation surfaced **HIGH-PRIORITY** finding: the lowercase clone contains a working Cloudflare Worker proxy for Pinecone (addressing GCP IP blocking) that's NOT in the canonical clone. `pinecone_client.py` is 300 lines vs canonical's 134, plus an entire `infrastructure/cloudflare-worker/` directory. Three recovery blocks defined in the memo.
- **Acceptance:** Cannot delete until E9.PROXY recovery lands.
- **Notes:** This was framed as "cleanup of redundant duplicate" in v1.0. Investigation revealed it's recovery of unique work that exists ONLY in the lowercase clone. Major reframing.

---

### E9.PROXY — Cloudflare proxy mode preservation

- **Status:** Open — **HIGH PRIORITY**
- **Size:** Day
- **Dependencies:** None
- **Source:** E9 investigation memo, 12 May 2026
- **Description:** Extract the Cloudflare Worker proxy code from `~/adgm-corpus/` (lowercase) to a preservation branch on canonical `~/ADGM/adgm-corpus/`. The proxy addresses GCP IP blocking that affects Voyage embedding from Hetzner — a real problem currently unsolved on canonical. Three blocks per memo: (a) `pinecone_client.py` proxy-mode additions (~166 net lines), (b) `infrastructure/cloudflare-worker/` directory contents, (c) any related config/docs.
- **Acceptance:** Preservation branch `recovery/cloudflare-proxy-2026-05-XX` on canonical adgm-corpus. All three blocks present. Tests added covering proxy-mode behaviour. Branch pushed to origin. Then (and only then) E9 deletion can be authorised.
- **Notes:** The proxy may also unblock B6 (Voyage re-embedding) by allowing it to run from Hetzner instead of requiring local-only execution. That's a secondary benefit worth confirming.

---

### E10 — Playwright Chromium update cadence on Hetzner

- **Status:** Open
- **Size:** ≤1 hour
- **Description:** Unchanged from v1.0.

---

# Category F — Test Coverage

---

### F1 — Frontend vitest configuration — **DONE [2026-05-12]**

- **Status:** Done — `sprint/F1-frontend-vitest-2026-05-11-overnight` (qanun, commit `1b9d965`); merged to qanun main, 12 May 2026
- **Acceptance:** ✓ vitest 4 configured with jsdom; 5 smoke tests pass (sign-in, dashboard, query, projects, settings). `npm test` runs cleanly on main.

---

### F2 — qanun-api pre-existing test failures — **DONE [2026-05-12]**

- **Status:** Done — `sprint/F2-test-failures-2026-05-11-overnight` (qanun-api, commit `8ffee13`); merged to qanun-api main in commit `b179bd2`; memo `~/qanun-docs/F2_qanun_api_test_failures.md` (commit `101c7c4`)
- **Findings:** 7 failures categorised. 2 fixed (1 test bug, 1 stale assertion). 1 properly skipped (was un-guarded integration test). 4 xfailed-strict with documented unxfail conditions.
- **Delta:** 39P/7F → 41P/4XF/1S/0F (test count preserved). Post-merge verification: 41P/1S/4XF/0F clean first try on qanun-api main.
- **Follow-ups:** F2.TRADEDAR and F2.CONTENT below.

---

### F2.TRADEDAR — TradeDar fixture for entity-model tests — **DONE [2026-05-13]**

- **Status:** Done — `sprint/F2-TRADEDAR-fixture-2026-05-12-overnight` (qanun-api, commit `8cdb79b`); merged to main in commit `805f50f` (Bundle 1 Merge 2, 13 May 2026)
- **Size:** Half-day
- **Source:** F2 memo, 12 May 2026
- **Description:** Autouse session-scoped fixture added to `tests/conftest.py` that calls `init_db()` and idempotently seeds the TradeDar demo entity. Fixture values mirror the hardcoded fallback in `services/drafting_service.py:234-252` so DB-backed row and fallback path agree. `xfail(strict=True)` marker removed from `test_tradedar_seeded`.
- **Acceptance:** ✓ Fixture in place; previously-xfailed test passes. Delta: 41P/1S/4XF → 42P/1S/3XF. Post-merge full suite: 42P/1S/3XF clean first try.
- **See:** `/tmp/qanun-overnight/f2/F2-TRADEDAR.md`

---

### F2.CONTENT — Section content-authoring for 3 xfail-strict template tests

- **Status:** Open
- **Size:** Day
- **Dependencies:** None (content work, not code)
- **Source:** F2 memo, 12 May 2026
- **Description:** Three template tests xfail-strict pending section content authoring. Author the missing content; unxfail.
- **Acceptance:** Content authored per template requirements; previously-xfailed tests pass.

---

### F3 — A1 regression test pass (audit completion)

- **Status:** Open
- **Size:** Half-day
- **Dependencies:** A6.LIVE
- **Description:** Unchanged from v1.0 (renumbered from v1.0's F3).

---

### F4 — DFSA sourcebook regression tests

- **Status:** Blocked
- **Size:** Half-day
- **Dependencies:** B2
- **Description:** Unchanged from v1.0.

---

### F5 — G1 smoke test suite expansion

- **Status:** Blocked
- **Size:** Day
- **Dependencies:** D11
- **Description:** Unchanged from v1.0.

---

# Beyond Launch — Post-Launch Roadmap

Unchanged from v1.0. Not in the register; forward product work explicitly post-launch:

- Phases 10-18 Vanta layer
- Qanun Monitor (compliance calendar add-on)
- Law firm account type
- Progressive automation thresholds
- DFSA/DIFC coverage expansion
- Seed fundraise (technical narrative in SOW v4.0)
- UCIE v2.0 El Salvador work (Phases 8-10)
- Qanun governance suite Tier 1-5 model

---

# Today's Achievements (12 May 2026 — Master Integration Session)

**Wall-clock: late afternoon → evening, interactive gated session.**

**10 sprint branches merged across 3 repos:**

- adgm-corpus master @ `95d925d`:
  - `913f93a` foundation merge (carrying A1.a–A1.h overnight scraper work)
  - `2863b79` A1-invariant
  - `53e0f87` C5 rulebook-filter
  - `6a2ae1a` C2 label
  - `7d01968` C3 typo (regression tests)
  - `6d9328b` C7 Drupal-robust
  - `f443dbb` A6 idempotence-test
  - `95d925d` C4 WAL-checkpoint
- qanun-api main @ `b179bd2`: F2 test-failures merge
- qanun main: F1 frontend-vitest merge

**Structural achievements:**

- First-parent topology preserved on each repo (8 first-parent steps on adgm-corpus alone)
- All 7 adgm-corpus + 1 qanun-api + 1 qanun sprint branches retained on origin
- No force-pushes
- Test counts at each gate were exact: 658 → 662 → 664 → 667 → 672 → 674+1S → 675+1S on adgm-corpus; 41+1S on qanun-api; 5 on qanun
- 298MB of polluted A6 sandbox cleaned up during A6 merge housekeeping
- Phase-2-backlog.md tracked in qanun-docs main (commit `a351ea7` + follow-ups)

**Three caught prompt-vs-reality mismatches via halt-and-surface:**

1. Smoke-check import path (A1-invariant): conceptual placement vs actual location
2. Sprint-branch arithmetic (C5): on-branch vs post-merge count conflation
3. Diff inspection target (C3): symmetric diff vs commit-contribution

All caught, all resolved on the spot, all filed as C12. Memory entries #18 and #19 added so future integration prompts inherit the discipline.

**One pre-existing flake characterised:**

`TestPerformanceQuickSearch::test_performance_quick_search` fired on 3 of 7 on-branch runs (C5, C2, C4). All cleared on retry. Post-merge runs all clean first-try. Filed as C11 with order-dependency hypothesis.

---

# Today's Achievements (13 May 2026 — Bundle 1 Merge Session)

**Wall-clock: ~3-4 hours interactive (per runbook estimate).**

**4 sprint branches merged across 2 repos:**

- adgm-corpus master @ `ccfa1c0` (final):
  - `9b77f69` — Merge 1: `sprint/A7-diagnostic-tools-2026-05-12-overnight` (audit script + 10 strict xfails)
  - `059ad05` — Merge 3: `sprint/flake-perf-test-2026-05-12-overnight` (C11 threshold raise 5s → 10s)
  - `ccfa1c0` — Merge 4: `sprint/A5C1-dfsa-source-url-2026-05-12-overnight` (backfill script + 7 strict xfails + 1 passing diagnostic)
- qanun-api main @ `805f50f` (final):
  - `805f50f` — Merge 2: `sprint/F2-TRADEDAR-fixture-2026-05-12-overnight` (xfail-strict flipped to passing)

**Test count baselines at session close:**

- adgm-corpus master: **676P / 1S / 22XF** (up from 675P/1S/5XF; +1P from A5C1 diagnostic; +17XF across A7-diag (10) and A5C1 (7))
- qanun-api main: **42P / 1S / 3XF** (up from 41P/1S/4XF; +1P from F2-TRADEDAR unxfail)
- qanun main: unchanged at 5 vitest passing (not touched by Bundle 1)

**Structural achievements:**

- First-parent topology preserved on each repo (3 merges on adgm-corpus master in stack: 9b77f69 → 059ad05 → ccfa1c0)
- All 4 sprint branches retained on origin (no deletion)
- No force-pushes; all four pushes were fast-forward updates, verified via reflog
- Test counts exact at each gate (8 gates total: 4 on-branch + 4 post-merge)
- C11 flake fired only on Merge 1 on-branch (sprint branch was cut from pre-flake-fix baseline at 95d925d); cleared on C11 retry-once protocol; protected by 10s threshold after Merge 3 landed
- Sprint-branch arithmetic from memory #19 verified across all 4 merges (each branch cut from 95d925d; both on-branch and post-merge counts spelled out per merge in the kickoff prompt, and all six explicit projections matched reality)
- Register synced from `/tmp/qanun-overnight/launch-readiness-register-v1.2.md` working canonical to `~/qanun-docs/launch-readiness-register.md` tracked canonical at session start (per kickoff correction 2; commit `f3d036f` on qanun-docs main)
- corpus.db sha256 unchanged across the session at `344305f05d…` (no merge touched corpus.db)

**Net register movement:**

- F2.TRADEDAR: Open → Done (merge `805f50f`)
- A5.C.1: Open → Open + Bundle 1 note (script + tests committed; backfill APPLY still pending)
- C11: Open → Open + Bundle 1 note (10s threshold mitigation committed; C11.A redesign still pending)
- A7 cluster items (A2, A7.B-A7.I): all Open — diagnostic + xfail-strict scaffolding committed on adgm-corpus, reconciliation SQL applies still pending per-rulebook interactive sessions (Bundle 2)

---

# Today's Achievements (12 May 2026 — Overnight Sprint)

Wall-clock: 17:18 → 18:15 Dubai +04, ~57 minutes for 19 items.

**12 items moved Open → Done:**
C2, C3, C4, C5, C7, C10, A1, A6, B3, C8, C9, E8 (investigation), E9 (investigation), F1, F2.

(Note: more items above are listed Done because in v1.0 they were Open at register-creation time; tonight's actual delta is C2/C3/C4/C5/C7/C10 + A1/A6 + B3/C8/C9 + E8-inv/E9-inv + F1/F2 = 14 register entries newly Done, plus the 2 already-Done from v1.0 carried forward.)

**12 audit/design memos in `~/qanun-docs/`:**
B1, A5, A7, B3, C8, C9, B2, C1, C4, F2, E8/E9, deploy_command_patterns.

**10 sprint branches on origin, awaiting master integration:**
- adgm-corpus: A1-invariant, A6, C2, C3, C4, C5, C7
- qanun-api: F2
- qanun: F1

**16 new register items folded into v1.1:**
A5.A, A5.B, A5.C (supersedes A4), A5.C.1, A5.D, A5.E, A5.F, A6.LIVE, A7.B, A7.C, A7.D, A7.E, A7.F, A7.G, A7.H, A7.I, A7.ROOT, C8.APPENDIX, E9.PROXY, F2.TRADEDAR, F2.CONTENT (~21 entries; some were sub-items consolidated).

---

# Backup Chain (Current State, 12 May 2026)

Six layers from yesterday's session, all preserved. Plus tonight's overnight ran read-only against the canonical corpus.db (sha256 unchanged at `344305f05d…`). Master integration session also ran read-only against corpus.db — sha256 verified unchanged at session close.

1. `corpus_pre_a1_apply_retry_20260511_0639.db` — pre-A1 baseline
2. `corpus_pre_2768_flip_20260511_1242.db` — pre-2768 flip
3. `corpus_pre_bulk_20260511_1413.db` — pre-bulk-v2 crash baseline
4. `corpus_pre_a1h_rebaseline_20260511_1529.db` — pre-rebaseline
5. `corpus_pre_bulk_v3_20260511_1534.db` — pre-bulk-resumed
6. `corpus_pre_surgical_rollback_20260511_1541.db` — pre-surgical-rollback

**Current canonical corpus.db state (post-master-integration, 12 May 2026 evening):**
- sha256 `344305f05d…` (unchanged from pre-overnight) — verified by master integration session
- Hetzner production corpus.db state: identical to canonical local at session close

Plus working artefacts:
- `/tmp/qanun-overnight/idempotence-sandbox/corpus.db` — **DELETED** during A6 merge housekeeping (was 298MB polluted by the A6 live test that ran inadvertently during overnight build). A6.LIVE can now stage a fresh sandbox.
- `/tmp/qanun-overnight/pre-overnight-uncommitted-backup/` — backup of legitimate uncommitted work from pre-overnight (rebaseline_content_hash.py, adgm_corpus/agents/, etc.).
- `/tmp/qanun-overnight/integration-progress.md` — internal log of the master integration session (per-merge gate dialogues, caught mismatches, surfaced surprises). Working artefact, not repo-tracked.

---

# Sequencing Recommendation (Revised in v1.2)

Significantly revised from v1.1 to reflect that D10 master integration is complete. Most first-wave items have lost their "A1 on master" or "D10" dependency and can now proceed in parallel.

**Status of canonical branches (12 May 2026 evening):**
- adgm-corpus master @ `95d925d` — 675P / 1S / 5XF
- qanun-api main @ `b179bd2` — 41P / 1S / 4XF / 0F
- qanun main @ post-F1 — 5 vitest smoke tests passing

**First wave — current (independent items, ≤half-day each, parallelisable across CCD sessions and overnight):**
- **A7-cluster** (9 half-day reconciliation items — A2 + A7.B–A7.I) — all now unblocked. Ideal overnight workload due to structural similarity and parallelism.
- **A5.C.1** — DFSA scraper source_url population fix (half-day, scoped).
- **E1** — API key rotation (overdue, half-day).
- **E3** — LLM-Legal-Council cleanup (≤1 hour).
- **E4** — Oliver OS PAT removal from git remote (≤1 hour).
- **F2.TRADEDAR** — TradeDar fixture rebuild (half-day).
- **C11** — Flake investigation diagnostic phase (half-day).
- **C12** — Integration prompt-drafting checklist drafting (half-day).

**Second wave — foundational + investigations (day-scale work):**
- **E9.PROXY** — high priority, preserve unique Cloudflare proxy work before any deletion (day, own session).
- **A5.A, A5.B** — refactor convention-dependent lookups (day + half-day).
- **A5.D** — content_hash pre-compute on INSERT (half-day).
- **C8.APPENDIX** — SOW schema reference appendix (half-day).
- **A7.ROOT** — ingestion-path root-cause investigation (day, depends on A7 cluster reconciliations giving fuller evidence).
- **A6.LIVE** — live idempotence exercise (half-day, own authorisation; sandbox already clean).
- **A3** — K7 retag carry-forward for OTHER X.Y section_refs (day, can run alongside A2).
- **F2.CONTENT** — Section content authoring for 3 xfail-strict template tests (day).

**Third wave — multi-day work (each is its own focused session or multi-session sprint):**
- **B1** — Parser redesign (week, biggest single item).
- **B2** — DFSA sourcebook handler implementation (5-6 days per memo).
- **A5.C** — Source-URL backfill at 2,099-row scale (multi-day).
- **B8** — DFSA inline citation maps (multi-day).
- **B5** — DIFC primary legislation ingestion (week).
- **D9** — D-section frontend (multi-day).

**Fourth wave — integration + after-bulk (depends on third wave landing):**
- **B4** — FSRA bulk refresh (after B1 lands).
- **A5.C completion** — using fresh fetches from B4.
- **B6** — Voyage re-embedding (after B2 + B4 + B5; E9.PROXY may simplify by allowing Hetzner-side execution).
- **B7** — Portability seeding (after B6).
- **C1** — extract_citations hook implementation (FSRA first, then DFSA after B8).
- **D1-D8** — Sprint section completion.
- **E8** — Lowercase qanun-api deletion (after authorisation).
- **E9** — Lowercase adgm-corpus deletion (after E9.PROXY recovery).

**Final wave — launch:**
- Master integration sessions for later branches (analogous to D10's discipline)
- **D11** — G1 smoke run against api.qanun.io.
- **F3, F4, F5** — Test coverage completion.
- F1 expansion (frontend test coverage beyond smoke).
- **D12** — Tester onboarding.

**Revised total estimate: 5-7 weeks** at ~1 CCD session/day pace (unchanged from v1.1). Master integration session was the foundation step that unblocked the first wave; subsequent waves should compress slightly with more parallelism available. Could compress further with parallel CCD sessions across different repos (different worktrees per Operational Hygiene rule 7) — first-wave items in particular benefit from this.

**Next-session recommendation:** Phase 2 prioritisation session itself (~half-day interactive) to walk the 67 + audit-surfaced entries and confirm the sequencing above is right. Or, if confidence is high in the sequencing, go directly to attacking first-wave items via overnight sprint (most are well-scoped enough to be overnight-suitable).

---

*End of register v1.3. Next update: when Bundle 2 (A7-cluster reconciliation apply) lands, when overnight produces new findings, or when next major batch moves Open → Done.*
