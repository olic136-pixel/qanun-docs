# TICKET: section_ref vector-metadata refresh (K16 pattern) — "46,558" park-list item

**Status:** Ready to build · **Gate:** EMBED (vector-store writes — requires explicit `Authorise` per studio protocol) · **Repo:** adgm-corpus
**Origin:** MAX-3 park list ("46,558 section_ref vector-metadata refresh (K16 pattern)", LAUNCH_VERDICT_20260610 / MAX3_MASTER_LOG §3) · **Written:** 2026-06-10 (MAX-4 V6)

## Headline number vs. real vector scope — probed 2026-06-10 (read-only)

The park-list figure 46,558 counts **corpus.db section-row renames** from M21 Stage-2
(`scripts/m21_stage2_remediate.py`):

- **P1** `--dfsa-prefix-sections`: 9,198 current DFSA section_refs renamed bare → `DFSA-`-prefixed (`GEN 3.3` → `DFSA-GEN 3.3`).
- **P2** `--other-reprefix`: 37,360 rows **incl. history** renamed `OTHER x.y` → `{rulebook_code} x.y` (FSRA IFR/FEES/PIN/CIB/BRR/WAIVERS parser-prefix bug).

Vectors only exist for a fraction of those rows (history rows and retired docs were
purged from the index in MAX-2/3 EMBED). **Actual stale-vector population found by
sample probe: ≈ 9,778, not 46,558.**

### Probe evidence (read-only `fetch`/`list`, index `describe_index_stats`, 2026-06-10)

Namespaces (total 66,018 + panama_smv 903): `default` 45,690 · `dfsa` 9,198 · `adgm` 4,744 · `el_salvador` 2,385 · `vara` 2,112 · `bvi_fsc` 986 · `panama_smv` 903.

| Scope | Namespace | Id scheme | Sampled | Stale | Evidence |
|---|---|---|---|---|---|
| P1 DFSA | `dfsa` (9,198 vectors — exactly the P1 count) | `dfsa_{slug}_{section_id}` (e.g. `dfsa_cmc_k_112143`) | 5/5 | **5/5 STALE** | meta `'CMC 1'` vs db `'DFSA-CMC 1'`, `'CMC 1.2'` vs `'DFSA-CMC 1.2'`, … |
| P2 FSRA | `default` | `doc_{doc_id}_chunk_{i}` | 11/11 | **11/11 STALE** | doc 62 (CIB) meta `'OTHER 1.2.2'`; doc 87 (FEES) `'OTHER 1.2.1'`…; doc 78 also has stale `rulebook_code='OTHER'` (db: WAIVERS) |
| DFSA-PRU 2431 hold-back | `default` (334 vectors) | `doc_2431_chunk_*` | 1 | **already correct** (`'DFSA-PRU 1.1'`, entity DFSA) | no action; slated for purge after the 2828 re-scrape anyway |
| FSRA keepers (non-P2), `adgm`, `vara`, `el_salvador`, `bvi_fsc`, `panama_smv` | — | — | — | unaffected | P1 touched only DFSA-entity sections; P2 only the 6 OTHER-prefixed FSRA rulebooks |

### Exhaustive P2 sizing (full chunk enumeration of the 7 current FSRA P2 docs)

| doc | rulebook | default-ns vectors | stale `OTHER *` |
|---|---|---|---|
| 62 | CIB | 114 | 114 |
| 78 | WAIVERS | 1 | 1 |
| 87 | FEES | 58 | 58 |
| 91 | PIN | 256 | 256 |
| 102 | WAIVERS | 3 | 0 (already non-OTHER refs) |
| 116 | BRR | 31 | 31 |
| 117 | IFR | 120 | 120 |
| **total** | | **583** | **580** |

**Refresh scope: 9,198 (`dfsa` ns, assume all stale per sample) + 580 (`default` ns) = 9,778 metadata-only updates.** No re-embedding — text unchanged, only `section_ref` (and for P2 docs, `rulebook_code`) metadata is stale. Chroma is out of scope (it was re-keyed/synced separately in MAX-2/3; verify with one sample if paranoid).

## Implementation — `scripts/refresh_section_ref_metadata.py` (K16 pattern)

Follow `scripts/k16_refresh_pinecone_metadata.py` exactly: dry-run default, `--apply`
gated, idempotent (skip already-correct), per-doc/per-page progress lines, grand totals.

### Pass A — `dfsa` namespace (9,198)
1. Enumerate ids: `index.list(namespace="dfsa")` (paginated; confirmed working in probe).
2. Parse trailing integer = `sections.id`. Source of truth:
   `SELECT section_ref FROM sections WHERE id = ?` against the canonical local
   corpus.db (read-only URI, per CLAUDE.md).
3. `fetch` in batches of 100 (fetch cap); compare `metadata.section_ref`.
4. Stale ⇒ `index.update(id=vid, set_metadata={"section_ref": db_ref}, namespace="dfsa")`.
5. Edge: section_id no longer in db ⇒ log + count as `orphan-vector` (purge candidate,
   do NOT update); db_ref not `DFSA-`-prefixed ⇒ log + skip (invariant breach).

### Pass B — `default` namespace P2 docs (580 of 583)
1. Doc set from corpus.db: current FSRA docs with `rulebook_code IN
   ('IFR','FEES','PIN','CIB','BRR','WAIVERS')` → ids 62, 78, 87, 91, 102, 116, 117
   (assert exactly 7; warn-and-list on drift, K16 style).
2. Enumerate `doc_{id}_chunk_{i}` with the K16 probe loop — raise `MAX_CHUNK_PROBE`
   to **300** (doc 91 has 256 chunks; K16's 100 is too small here).
3. New ref: prefix swap `new = f"{rulebook_code} " + old[len("OTHER "):]` **validated
   against db**: require `new` ∈ that doc's current `section_ref` set; if not (chunk
   sub-refs like `'OTHER 1.2.2(i)'` should still match since P2 renamed them
   identically), log + skip rather than guess.
4. Update both stale fields in one call:
   `set_metadata={"section_ref": new, "rulebook_code": code}` (fixes doc 78's
   `rulebook_code='OTHER'` too).
5. Leave `doc_2431_chunk_*` alone (already correct; hold-back owned by the 2828
   re-scrape ticket).

### Runtime estimate
Pinecone has no bulk metadata-update — 1 `update` call per vector.
- Reads: ~98 list pages + ~98 fetch batches (dfsa) + ~10 fetch batches (default) ≈ 2–3 min.
- Writes: 9,778 updates. Serial @ ~5–10 req/s ⇒ **~16–33 min**; with 8 concurrent
  workers (safe for metadata updates) ⇒ **~4–8 min**. Budget **≤ 45 min** end-to-end
  serial, **≤ 15 min** parallel. $0 (no embedding calls).

### Verification (post-apply)
1. Re-run script without `--apply` ⇒ `would-update: 0` both passes (idempotence proof).
2. Re-run the V6 probe queries: `dfsa_cmc_k_112143..7` show `DFSA-CMC *`;
   `doc_62/87/91/116/117_chunk_0..4` show `{code} *`, zero `OTHER *`.
3. `describe_index_stats` namespace counts **unchanged** (metadata-only:
   default 45,690 / dfsa 9,198 / adgm 4,744 / vara 2,112 / el_salvador 2,385 /
   bvi_fsc 986 / panama_smv 903).
4. Functional spot-check: scoped retrieval with metadata filter
   `{"section_ref": {"$eq": "DFSA-CMC 1.2"}}` in `dfsa` ns returns the vector;
   the bare `"CMC 1.2"` filter returns nothing.
5. Register flip: close the "46,558 section_ref vector-metadata refresh" park-list
   line with the true number (9,778 updated; 37k+ history rows had no vectors).

### Risks / notes
- **EMBED-gated**: although metadata-only, these are production vector-store writes —
  hold for explicit authorisation, run from local Mac (Voyage not needed, but keep the
  same operational discipline).
- Interruptible/resumable by design (idempotent skip of already-correct vectors).
- If the orphan-vector count in Pass A is > 0, file the list against the next EMBED
  purge — do not purge in this script.
