# Manifest Schema Expansion + VARA Worked Example

**Generated:** 2026-05-15
**Schema file:** `~/ADGM/adgm-corpus/adgm_corpus/manifests/MANIFEST_SCHEMA.json` (v1.0 → v1.1)
**VARA migration:** `~/ADGM/adgm-corpus/adgm_corpus/manifests/VARA.json` (12 docs → 13 docs + 8 material categories)

---

## Why expand the schema

Overnight MCR generation (14-15 May 2026) reconciled `corpus.db` against each jurisdiction's `expected_documents` list and reported full presence — but the **VARA Quick Lookup gap (Marketing Regulations 2024) never surfaced** because `expected_documents` only enumerated the 12 rulebooks. Standalone regulations, guidance, circulars, enforcement decisions, FAQs, and forms had no place in the schema.

A manifest that omits a category cannot detect missing material in that category. The MCR's "12/12 PRESENT" verdict for VARA was technically correct against the manifest, but the manifest itself was the gap.

## Schema change (additive, back-compat)

Two changes to `MANIFEST_SCHEMA.json`:

1. **`material` becomes a new optional top-level field** — an object with 8 named arrays, one per category:
   - `primary_legislation` — foundational law (decrees, acts establishing the regulator)
   - `implementing_regulations` — standalone regulations like VARA-MR2024
   - `rulebooks` — the existing rulebook category
   - `guidance` — formal guidance notes
   - `circulars` — regulator notices/circulars
   - `enforcement_decisions` — published enforcement actions
   - `faqs` — published FAQ documents
   - `forms` — registration/regulatory forms

2. **`doc_type_values` extended** from 5 → 8 to include `"regulation"`, `"form"`, `"faq"` — supporting the new categories without breaking the existing `legislation`/`rulebook`/`guidance`/`circular`/`judgment` taxonomy.

**Back-compat preserved:** `expected_documents` remains the canonical flat list. `mcr_generator.py:281`, `sync/completeness_checker.py:132`, `scripts/add_jurisdiction.py`, and the 6 existing MCR `.md` files all continue to work unmodified. The new `material` field is **additive**:

- A manifest that uses only `expected_documents` (no `material` block) continues to work as before.
- A manifest with both gets the same MCR result via `expected_documents`, AND gains finer-grained category accounting via `material`.
- A future mcr_generator can be updated to prefer `material` for category-level gap reporting; expected_documents stays as the flat de-duplicated index.

## VARA worked example — before/after

| | Before (v1.0) | After (v1.1) |
|---|---:|---:|
| Top-level fields | 13 | 15 (+`secondary_sources`, +`material`) |
| `expected_documents` count | 12 | 13 (+VARA-MR2024) |
| Material categories enumerated | 0 (implicit "rulebooks-only") | 8 (1 populated with VARA-MR2024, 1 with 12 rulebooks, 6 empty placeholders) |
| Quick Lookup gap (VARA-MR2024) representable? | No | **Yes** |

**The `VARA-MR2024` entry** carries:
- `doc_type: "regulation"` (the new doc_type_value)
- `tier: 1` (CRITICAL severity — referenced by VARA-MC Part IV templates)
- `source_url: "https://www.vara.ae/regulations"` with `_pending_verification: true` flag — the regulations index page is known; the specific download URL needs manual confirmation against the live page
- Notes the cite chain (VARA-MC Part IV + compliance manual templates)

**The 6 empty material categories** (`primary_legislation`, `guidance`, `circulars`, `enforcement_decisions`, `faqs`, `forms`) — present as empty arrays. Each is an honest placeholder: VARA has no published case law yet (Sprint 3 closure carry; URL discovery deferred), and the others are not yet enumerated. Future sessions populate them as material is sourced.

**Secondary sources** added: 3 entries pointing at `rulebooks.vara.ae`, `vara.ae/regulations`, `vara.ae/news` — the per-category URL roots a future MCR generator can probe.

## Pattern for migrating other 5 jurisdictions

Each per-jurisdiction migration is the same shape:

1. **Read** the existing `<JURISDICTION>.json` and verify the manifest is on schema v1.0.
2. **Lift** the existing `expected_documents` list into `material.rulebooks` (or whichever category fits — DFSA's "modules" and "sourcebooks" both map to `rulebooks`).
3. **Add** `secondary_sources` for the jurisdiction's per-category URL roots:
   - ADGM → Thomson Reuters portal index + adgm.com FSRA notices + adgm.com legal framework
   - DFSA → Thomson Reuters DFSA portal + dfsa.ae enforcement decisions index
   - BVI → bvifsc.vg published acts + AML guidance index
   - EL_SALVADOR → cnad.gob.sv downloads + Diario Oficial
   - PANAMA → smv.gob.pa published material index
4. **Enumerate** known surfaced gaps into the relevant material category. Specific known gaps per jurisdiction:
   - ADGM/FSRA: GEN 8.5 Approved Person notification rule (Quick Lookup gap, currently appears truncated in corpus per Block A) — this is a corpus integrity issue, not a manifest enumeration issue.
   - DFSA: any standalone regulations distinct from the 22 modules already enumerated
   - BVI: AML/MLR guidance documents (FSC publishes some standalone of the rulebooks)
   - EL_SALVADOR: Diario Oficial primary legislation (Bitcoin Law original, LEAD24 reform decree) — should populate `primary_legislation`
   - PANAMA: any AML/CFT supporting law distinct from SMV regulations
5. **Append** the same `material` block structure with all 8 categories populated or empty.
6. **Add** new `expected_documents` entries for any surfaced gaps so back-compat MCR generation also picks them up.
7. **Validate** the JSON parses, all required fields present, doc_types all in allowed values, all 12 rulebook codes (or equivalent) preserved.
8. **Re-run** the per-jurisdiction MCR (`scripts/mcr_generator.py` or equivalent) — the count should rise from "X/X PRESENT" to "X/Y PRESENT" if any new gaps were added.

## Estimated effort per jurisdiction

| Jurisdiction | Effort | Notes |
|---|---|---|
| ADGM/FSRA | ~60 min | Largest manifest (22+ FSRA rulebooks; need to enumerate standalone regulations + RA material); GEN 8.5 truncation is corpus-side not manifest-side |
| DFSA | ~45 min | 22 modules already enumerated; check for standalone regulations + any DFSA fund laws |
| BVI | ~30 min | Smaller surface; AML/MLR guidance is the likely addition |
| EL_SALVADOR | ~45 min | Need to populate primary_legislation (Bitcoin Law + LEAD + LEAD24) |
| PANAMA | ~30 min | Smallest enumeration; 3 known gaps surface |

**Total:** ~3.5 hours model-active across 5 sessions; or 5 parallel sessions in V2 orchestrator at ~45 min each.

## Recommended next sessions

1. **One follow-up session per jurisdiction** (5 sessions, parallel-safe in V2) — apply the migration pattern above to ADGM/DFSA/BVI/EL_SALVADOR/PANAMA manifests.
2. **One MCR re-run session** after all 5 manifests land — refresh the 6 `~/qanun-docs/mcr/*.md` files against the expanded manifests. This is L10-L15 (or M10-M15 post-register-patch) re-run.
3. **One mcr_generator upgrade session** — update `scripts/mcr_generator.py` to *prefer* `material` over `expected_documents` for category-level gap reporting (output table grouped by category). Optional; can defer to V2.

## Register impact

This memo informs **M20 — Manifest schema expansion + per-jurisdiction migration** (the proposed M-category entry). Status:
- Schema v1.1 landed — **Done**
- VARA migrated — **Done**
- 5 remaining migrations (ADGM, DFSA, BVI, EL_SALVADOR, PANAMA) — **In Progress** (1 of 6 complete)
- MCR re-run — **Open** (depends on all 5 migrations)

The "In Progress" status flips to Done after the 5 remaining jurisdictions are migrated.
