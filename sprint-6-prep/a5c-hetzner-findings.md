# A5.C — Hetzner Production corpus.db source_url State Findings

**Block L — Sprint 6 prep overnight (15-16 May 2026)**

## Investigation

A5.C is the long-standing "documents missing source_url" register item.
Sprint 3 Cleanup's A5.C audit memo recommended **probing Hetzner production
first** (Option 3) before any backfill, on the chance production already
has source_url populated. This block ran that probe.

**Correction (Memory #18/#23):** the Sprint-6-prep brief's L2 step queried
`/home/qanun/ADGM/qanun-api/qanun_demo.db` — that database has **no
`documents` table**. The `documents` table (and its `source_url` column)
lives in the adgm-corpus `corpus.db`, not the qanun-api app DB. The query
below targets the correct file: `/home/qanun/ADGM/adgm-corpus/corpus.db`.

## Hetzner production corpus.db — source_url state (is_current=1)

```
Total is_current=1 documents:  2,298
Missing source_url:            2,083
Has source_url:                  215
```

Missing by source_entity:

| source_entity | missing |
|---|---:|
| DIFC_COURTS | 1066 |
| FSRA | 626 |
| ADGM_COURTS | 264 |
| UNKNOWN | 57 |
| BVI_FSC | 27 |
| EL_SALVADOR | 16 |
| ADGM_RA | 8 |
| DFSA | 6 |
| PANAMA_SMV | 5 |
| DIFC | 5 |
| MONDAQ | 2 |
| PANAMA | 1 |

## Verdict

**Option 3 (copy-from-prod) is NOT viable.** Hetzner production has the
*same* source_url gap as local — 2,083 of 2,298 is_current=1 documents are
missing source_url on production too. There is no populated production copy
to backfill from.

The gap profile is near-identical to the local audit (Sprint 3 Cleanup
Block D4 found ~2,030 locally; production shows 2,083). The small delta is
just per-session drift — both environments share the same backfill debt.

## Recommended path (revises the Sprint 3 Cleanup A5.C memo)

Option 3 eliminated. The remaining options collapse to a **category-split
re-derivation** (Option 4):

1. **Court documents — DIFC_COURTS (1066) + ADGM_COURTS (264) = 1,330, 64%
   of the gap.** These are judgments. Their URLs live on the court portals
   (difccourts.ae judgment registry, adgm.com judgments). Backfill needs a
   court-portal scrape keyed on case citation — a dedicated case-law-URL
   session, distinct from rulebook scraping.

2. **FSRA (626) — mostly historical rulebook versions.** The
   `adgm_rulebooks` scraper's `MODULE_URLS` only knows the *current*
   version URL per module. Writing the current URL onto a historical-
   version row would be factually wrong. Needs version-aware URL
   reconstruction (the `net_file_store` path encodes the version — e.g.
   `ADGM1547_7584_VER13270426.pdf` — so the URL is derivable from
   `version_str` IF the file-store ID per module is known; that mapping
   would need building).

3. **UNKNOWN (57) — needs source_entity classification first**, then
   falls into one of the above buckets.

4. **Small tail (BVI/EL_SALVADOR/DFSA/PANAMA/DIFC/MONDAQ ≈ 62 rows)** —
   ad-hoc; manual title→URL mapping is cheapest.

No backfill applied this session — surfacing the verdict is the
deliverable. A5.C remains a discrete register item; the next concrete
step is the court-portal scrape for the 1,330 court documents (the
largest, most tractable single chunk).
