# A7 — Cross-Jurisdiction Single-Current Invariant Audit

**Date:** 2026-05-12
**Author:** Overnight sprint Claude (Opus 4.7) per `Authorise overnight-sprint-2026-05-11`
**Scope:** read-only audit of `/Users/oliver/ADGM/adgm-corpus/corpus.db`
**Snapshot:** 2026-05-10 (sha256 `344305f05d1177c3`)

> Note on snapshot date. The canonical local corpus.db is the 10 May
> Hetzner snapshot; today's A1.h work (doc 2768 flip, DFSA bulk) ran
> against the 11 May Hetzner state. So findings here reflect the
> pre-A1.h baseline. The single-current orphan situation has likely
> changed for `FSRA GEN` on Hetzner (doc 2768 → is_current=0); the
> other findings below are not affected by today's A1.h work and
> remain live.

---

## Method

Single-current invariant: for every `(source_entity, rulebook_code)`
pair where rulebook_code is non-empty, there must be ≤ 1
`is_current=1` row.

```sql
SELECT source_entity, rulebook_code, COUNT(*) AS current_count, GROUP_CONCAT(id) AS ids
FROM documents
WHERE is_current = 1
GROUP BY source_entity, rulebook_code
HAVING current_count > 1
```

Then per-violation deep-dive: `length(full_text)`, `version_str`,
`updated_at` to classify each orphan row.

---

## Results — by source_entity

| source_entity | violating rulebook_codes               | total orphan rows |
|---------------|---------------------------------------|-------------------|
| FSRA          | GEN, COBS, FUNDS, PRU, MIR, GLO       | 22                |
| BVI_FSC       | BVI-BCA, BVI-REGS                     | 4                 |
| UNKNOWN       | COMP-LAW-FOUNDATI, COMP-LAW-PRIVATE_  | 5                 |
| (placeholder rulebook_code buckets — not real rulebook orphans) |                       |                   |
| FSRA          | empty / OTHER                         | 636 + 65          |
| ADGM_RA       | empty / ADGM-RA-F                     | 5 + 32            |
| ADGM FSRA     | ADGM-FSRA-F                           | 37                |
| ADGM_COURTS   | NULL                                  | 263               |
| DIFC_COURTS   | NULL                                  | 1066              |
| (others with empty/NULL rulebook_code) | — | varies |

The "placeholder rulebook_code" buckets reflect documents (consultations,
judgments, guidance papers, registration forms) where rulebook_code is
empty or set to a category label (`OTHER`, `ADGM-RA-F`, `COMP-LAW-…`).
They are *not* the same rulebook with multiple current rows. The SQL
GROUP BY happens to collapse them into one bucket because they share
the placeholder value.

The **real** rulebook orphans (where the same rulebook_code legitimately
designates a single rulebook) are FSRA's 6 rulebooks, BVI_FSC's 2, and
UNKNOWN's 2 truncated codes.

---

## Detail — FSRA real orphans

All six follow the same shape: one legitimate March 2026 row with a
populated `version_str` and substantial `full_text`, plus a 28-April
"stub" with tiny `full_text` and empty `version_str` (a botched scrape),
plus one or more 2-May rows of varying size.

### FSRA GEN (3 currents)

Already documented in today's A1.h diagnostic. Reproduced for completeness.

| id   | version_str   | full_text len | updated_at        | classification               |
|------|---------------|---------------|-------------------|------------------------------|
| 206  | VER12.311025  | 260,078       | 2026-03-15 16:31  | legitimate prior version (K7-era OTHER X.Y refs) |
| 2768 | (empty)       | 4,790         | 2026-04-28 05:23  | ingestion artefact (stub)    |
| 2790 | (empty)       | 264,747       | 2026-05-02 05:20  | current VER13 (metadata gaps — A2) |

Per the prompt, doc 2768 was flipped on Hetzner on 11 May. The local
snapshot is from 10 May so still shows it is_current=1. **Hetzner state
verification pending.**

### FSRA COBS (5 currents) — **NEW finding**

| id   | version_str   | full_text len | updated_at        | classification |
|------|---------------|---------------|-------------------|----------------|
| 184  | VER21.010126  | 426,433       | 2026-03-15 16:29  | legitimate prior version |
| 2767 | (empty)       | 21,400        | 2026-04-28 05:23  | ingestion artefact (stub) |
| 2783 | (empty)       | 7,828         | 2026-05-02 05:20  | second stub (incomplete fetch) |
| 2787 | (empty)       | 438,313       | 2026-05-02 05:20  | duplicate of 2788 — both look like full captures from the same 2-May run |
| 2788 | (empty)       | 444,434       | 2026-05-02 05:20  | duplicate of 2787 |

The 2787 ↔ 2788 duplication is the worst case — two full captures from
the same ingestion run, both is_current=1. Even after a clean flip of
the older rows, one of 2787/2788 needs to be flipped to 0 and the other
must populate `version_str`.

### FSRA FUNDS (3 currents)

| id   | version_str   | full_text len | updated_at        | classification |
|------|---------------|---------------|-------------------|----------------|
| 199  | VER19.010126  | 873,340       | 2026-03-15 16:31  | legitimate prior |
| 2784 | (empty)       | 340           | 2026-05-02 05:20  | ingestion artefact (340 bytes — failed fetch) |
| 2789 | (empty)       | 283,107       | 2026-05-02 05:20  | current capture — but smaller than the prior 873k, suggests partial extraction |

The 873k → 283k size drop between March prior and May capture is
suspicious. Either a real content reduction or the parser missed
content. Worth verifying before flipping the older row.

### FSRA PRU (3 currents)

| id   | version_str   | full_text len | updated_at        | classification |
|------|---------------|---------------|-------------------|----------------|
| 15   | VER13.181223  | 863,831       | 2026-03-15 16:22  | legitimate prior |
| 2772 | (empty)       | 4,857         | 2026-04-28 05:23  | ingestion stub |
| 2795 | (empty)       | 875,628       | 2026-05-02 05:21  | current capture |

Cleaner — 875k vs 863k prior is a believable +12k delta.

### FSRA MIR (3 currents)

| id   | version_str   | full_text len | updated_at        | classification |
|------|---------------|---------------|-------------------|----------------|
| 326  | VER08.110724  | 246,859       | 2026-03-15 16:34  | legitimate prior |
| 2770 | (empty)       | 1,491         | 2026-04-28 05:23  | ingestion stub |
| 2793 | (empty)       | 248,524       | 2026-05-02 05:20  | current capture |

### FSRA GLO (5 currents) — also notable

| id   | version_str   | full_text len | updated_at        | classification |
|------|---------------|---------------|-------------------|----------------|
| 169  | VER25.010126  | 158,802       | 2026-03-15 16:28  | legitimate prior |
| 2769 | (empty)       | 1,442         | 2026-04-28 05:23  | ingestion stub |
| 2785 | (empty)       | 1,970         | 2026-05-02 05:20  | second stub |
| 2791 | (empty)       | 159,741       | 2026-05-02 05:20  | current capture A |
| 2792 | (empty)       | 161,232       | 2026-05-02 05:20  | current capture B (duplicate of 2791) |

Same shape as COBS — two stubs (one from each ingestion attempt) plus
two duplicate full captures from the same 2-May run.

---

## Detail — BVI_FSC orphans

### BVI_FSC BVI-BCA (2 currents)

| id   | full_text len | updated_at        | classification |
|------|---------------|-------------------|----------------|
| 2662 | 472,544       | 2026-04-03 07:31  | first capture |
| 2756 | 472,544       | 2026-04-15 07:01  | second capture, byte-identical |

Two identical captures 12 days apart. Either pipeline re-ran without
detecting unchanged content, or the second capture was supposed to
flip the first to is_current=0 but didn't. Flip 2662 to is_current=0,
set superseded_by=2756 (or vice versa — they're identical).

### BVI_FSC BVI-REGS (2 currents)

| id   | full_text len | updated_at        | classification |
|------|---------------|-------------------|----------------|
| 2589 | 25,931        | (NULL)            | unknown vintage |
| 2664 | 25,944        | 2026-04-03 07:31  | April 3 capture |

13-byte size delta, no detectable content drift. Flip the older
(2589) to is_current=0.

---

## Detail — UNKNOWN COMP-LAW orphans

The UNKNOWN source_entity bucket has 11 docs with truncated
`rulebook_code` values like `COMP-LAW-FOUNDATI`, `COMP-LAW-PRIVATE_`,
`COMP-LAW-BRANCH_F` (note 17-character truncation). These are ADGM
Companies Regulations 2015 templates and forms:

- 2 rows under `COMP-LAW-FOUNDATI` (Foundation Registration + Foundation
  Continuance — distinct docs, same truncated code)
- 3 rows under `COMP-LAW-PRIVATE_` (Private Ltd Non Financial, Private
  Ltd Rsc Non Financial, Private Ltd Retail — three distinct docs)

The invariant is "violated" only because the rulebook_code field was
truncated during ingestion, causing distinct documents to share a
code. They are not the same rulebook with multiple currents. **Fix is
at the rulebook_code field, not the is_current flag.**

---

## Categorisation summary

| Pattern                                  | Affected            | Treatment                              |
|------------------------------------------|---------------------|----------------------------------------|
| Legitimate prior + stub + current dup    | FSRA COBS, GLO      | Flip older + dedup one of the dups     |
| Legitimate prior + stub + clean current  | FSRA GEN, FUNDS, PRU, MIR | Flip older + flip stub + verify current metadata |
| Two identical captures, no flip          | BVI-BCA, BVI-REGS   | Flip the earlier to is_current=0       |
| Truncated rulebook_code conflating docs  | UNKNOWN COMP-LAW    | Fix rulebook_code on each doc — not a flip issue |
| Placeholder rulebook_code (OTHER/empty)  | FSRA (701 rows), ADGM_RA, ADGM_COURTS, DIFC_COURTS, ADGM FSRA | Not a rulebook orphan — categorisation noise; surfaces in A5.B section_ref work |

---

## Proposed new register items

Per the audit, each FSRA orphan rulebook gets its own A2-shaped item.

### A7-FSRA-COBS (Day)
Reconcile 5 is_current=1 rows for FSRA COBS. Flip 184 (prior),
2767 + 2783 (stubs), keep one of 2787/2788 (full capture). Pick the
larger (2788 at 444k). Backfill version_str on 2788. Same audit-trail
shape as today's A2 work on GEN.

### A7-FSRA-GLO (Day)
Same as COBS — flip prior + 2 stubs, dedup 2791/2792.

### A7-FSRA-FUNDS (Half-day)
Verify the 873k → 283k size drop (real content reduction or parser
miss?). Flip 199 + 2784 (stub).

### A7-FSRA-PRU (Half-day)
Flip 15 + 2772 (stub); keep 2795. Backfill metadata on 2795.

### A7-FSRA-MIR (Half-day)
Same as PRU.

### A7-FSRA-GEN (Half-day)
Already covered by existing register item **A2**.

### A7-BVI-BCA (Half-day)
Flip 2662; keep 2756.

### A7-BVI-REGS (Half-day)
Flip 2589; keep 2664.

### A7-UNKNOWN-COMP-LAW-TRUNCATE (Half-day)
Investigate why `rulebook_code` was truncated at 17 chars (column
type? scraper bug?). Re-derive rulebook_code from title for each of
the 11 affected docs. Add an INSERT-time check that rulebook_code
length matches expected ranges.

---

## Cross-cutting findings

1. **The 28-April + 2-May FSRA stub pattern repeats across 6 rulebooks.**
   It looks like the same pipeline ran twice and BOTH runs failed
   mid-fetch on a non-trivial subset of rulebooks, committing
   nearly-empty rows. Worth investigating the ingestion path's
   error handling — small full_text (under 25KB for a real rulebook)
   should be a hard failure, not a silent commit.

2. **The 2-May FSRA duplications (COBS 2787/2788, GLO 2791/2792)**
   appear to be the same ingestion run committing two captures of the
   same module. A1 invariant (landed in `sprint/A1-invariant-2026-05-11-overnight`)
   would have caught the second of each pair at write time.

3. **BVI_FSC's 12-day re-capture with byte-identical content** suggests
   the BVI scraper doesn't check content_hash before INSERT — does the
   full upsert cycle every run. Worth confirming and aligning with
   FSRA/DFSA's content_hash-aware upsert.

4. **The placeholder rulebook_code buckets are wide:** FSRA has 636 rows
   with empty rulebook_code and 65 with `OTHER`. These are
   consultations, circulars, and pre-K7 docs. Surfaces in A5.B
   (section_ref normalisation) but not a real "multi-current rulebook"
   problem.

---

## Register

Maps to register item A7. Each A7-* sub-item is a candidate new item.
The A1 invariant landed tonight prevents NEW occurrences of this
pattern; the existing rows need explicit reconciliation per A2-shape.
