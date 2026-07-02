# U0.2-P4b — Document Content API (in-app reader backend)

**Date:** 2026-07-02
**Lane:** CCD/U0.2-P4b (qanun design-elevation sprint, backend)
**Repo:** qanun-api — branch `sprint/u02-doc-content` (b573e2f), merged `--no-ff` to main **7bcf671**, deployed to prod (deploy script: `health=200, auth-guard=403`, new PID 4160003, journal clean).
**Suite:** 1100 passed / 1 skipped / 2 xfailed (baseline 1086 + 14 new in `tests/test_u02_document_content.py`).

---

## Endpoint

```
GET /api/documents/{job_id}/content
```

Read-only. Returns a drafted document's full body for the in-app "View
document" reader: ordered sections (heading + body from the same
`sections_json` the DOCX is assembled from), per-citation A1 verification
with character spans, structured per-section coverage (the clean-typed
replacement for the stringified `['AML 4.1']` `coverage_warnings` reprs),
a document-level verification summary, and the provenance handle.

Implementation: `routers/documents.py` (new file, mounted in `main.py`
under `/api`). ADDITIVE — no existing route changed; no writes to any
table; corpus.db only ever read (via the live verifier/coverage helpers);
`A1_DRAFTING_GATE` untouched; `A1_SEMANTIC_SUPPORT` stays OFF (the live
`verify_answer` consults the flag itself and is a no-op while OFF); no new
dependencies.

## Auth

| Case | Response |
|---|---|
| No / invalid bearer token | **401** (`auth.dependencies.get_current_user`; at the edge the platform surfaces missing-credential as **403** — same as every neighbouring endpoint, and what `deploy_prod.sh`'s auth-guard check asserts) |
| Job does not exist | **404** `{"detail": "Job {job_id} not found"}` |
| Job's entity belongs to another org / another user (legacy no-org) | **403** — `{job_id}` is a locator only; access is decided from the principal via `routers.register._resolve_entity` (the shared A2/A10 tenant guard: `Entity.org_id == principal.org_id`, legacy no-org entities fall back to owner-or-unowned) |
| Job exists but drafting not at a readable phase (`created/running/completing/failed`, or empty `sections_json`) | **409** `{"detail": "No drafted content for this job yet (status: …)"}` — readable statuses are `drafted`, `exporting`, `export_failed`, `complete` (content exists from end of Phase A; export state only affects the DOCX artefact) |
| `sections_json` over 5 MB (never observed; prod max 434 KB) | **413** size guard |

## Response schema

Top level (all enum-ish strings are stable lowercase; all counts are ints;
all lists are JSON arrays — never stringified reprs):

| Field | Type | Meaning |
|---|---|---|
| `job_id` | string | The draft job id (== provenance `doc_id`). |
| `entity_id` | string | Owning entity. |
| `doc_type` | string | e.g. `aml_cft_policy`. |
| `target_jurisdiction` | string | e.g. `ADGM`. |
| `status` | string | lowercase job status (`drafted` \| `exporting` \| `export_failed` \| `complete`). |
| `suite_id` | string\|null | Suite membership, if drafted as part of a suite. |
| `document_category` | string\|null | e.g. `application_pack` (null on older jobs). |
| `started_at` / `completed_at` | string\|null | ISO timestamps. |
| `output_filename` | string | DOCX filename (same value the status endpoint exposes; **no filesystem path**). |
| `section_count` | int | Number of sections. |
| `content_chars` | int | Total body characters (payload sizing). |
| `sections` | array | Ordered sections — see below. |
| `verification_summary` | object | Document-level A1 counts — see below. |
| `coverage_summary` | object | Document-level coverage counts — see below. |
| `provenance` | object | Ledger handle — see below. |

### `sections[]` (drafted order)

| Field | Type | Meaning |
|---|---|---|
| `index` | int | 0-based position. |
| `section_id` | string | e.g. `s8`. |
| `title` | string | Section heading. |
| `content` | string | Full drafted body (markdown-ish prose as persisted; may itself start with `#` headings on early sections). |
| `render_mode` | string | `prose` \| `numbered_list` \| `table` … (template `SectionRenderMode`, lowercase). |
| `table_headers` | array\<string\> | Enforced table headers ( `[]` when none). |
| `portability_layer` | int\|null | 0–4 template portability layer. |
| `coverage_pct_as_drafted` | number\|null | The coverage % persisted at draft time (as-drafted signal). |
| `drafted_at` | string\|null | ISO timestamp. |
| `citations` | array | Per-citation A1 records — see below. |
| `coverage` | object | Structured expected-vs-cited — see below. |

### `sections[].citations[]` — live A1 (deterministic Layer-1) per citation

Produced by the **live** `services.verification_service.verify_answer` at
read time (the same annotate path as `/api/addin/section-content`); the
verdicts therefore reflect the **current** corpus.

| Field | Type | Values / meaning |
|---|---|---|
| `ref` | string | Normalised cited ref, e.g. `AML 8.1`. |
| `matched_ref` | string\|null | Corpus ref it resolved to (null if unresolved). |
| `resolution` | string | `resolved` \| `resolved_parent` \| `unresolved`. |
| `strict_support` | string | `supported` \| `unsupported` \| `not_assessed`. |
| `support_flag` | string\|null | `supported` \| `unverified_review` \| null (unresolved — would be stripped by the draft gate). |
| `passes_export_gate` | bool | resolved AND strictly supported. |
| `support_overlap` | number\|null | Content-term containment fraction (0–1). |
| `is_corpus_defect` | bool | Cited section is a known-broken corpus copy (re-segmentation pending). |
| `corpus_version` | string | e.g. `VER11.210526`. |
| `tier` | int\|null | Corpus source tier. |
| `spans` | array\<[int,int]\> | `[start, end)` character offsets of each occurrence **in this section's `content`**, covering the full bracketed citation as rendered (including any `", VERxx, effective …"` suffix) — for reader highlighting. |
| `reason` | string | Human-readable verdict reason (`""` when supported). |

### `sections[].coverage` — structured expected-vs-cited

Recomputed at read time with the **live** `validate_coverage` (same
validator the pipeline uses) against the template's `required_provisions`
and the current corpus. This is the clean replacement for the old
stringified `coverage_warnings` (`"Section s8: 1 provisions not cited:
['AML 8.6']…"`).

| Field | Type | Meaning |
|---|---|---|
| `expected` | array\<string\> | Template-required provisions for this section (`[]` for doc types without a registered template, e.g. tier-0 packs). |
| `covered` | array\<string\> | Required provisions actually cited. |
| `missing` | array\<string\> | Required provisions NOT cited. |
| `phantom_citations` | array\<string\> | Citation-shaped strings in the body that do not exist in the corpus (includes the known recognizer false-positives such as `"ISORY SERVICE IS RENDERED"` — pre-existing data quality, now at least surfaced as clean arrays). |
| `coverage_pct` | number | covered/expected × 100, one decimal. |

### `verification_summary` (document level; all ints except `layer`)

`total_citations`, `resolved`, `resolved_parent`, `unresolved`,
`supported`, `unverified_review`, `corpus_defect`, `passed_export_gate`,
plus `layer: "l1-deterministic"` (no Layer-2/LLM number — semantic support
is OFF).

### `coverage_summary` (document level; all ints)

`expected`, `covered`, `missing`, `phantom_citations` — sums of the
per-section array lengths.

### `provenance`

| Field | Type | Meaning |
|---|---|---|
| `doc_id` | string | == `job_id`; the id the ledger keys on. |
| `record_count` | int | Tamper-evident provenance rows for this job. |
| `corpus_versions` | array\<string\> | Distinct corpus versions cited. |
| `endpoint` | string | `/api/provenance/{job_id}` (existing ledger endpoint for the full chain rows + Merkle root). |

## Example (live demo job, trimmed)

From prod, demo user, job `98937156-c8ba-411d-ae84-09d04da274b9`
(TradeDar AML/CFT Policy — the U0.3 walkthrough job). Full payload:
**103,481 bytes**, 14 sections, served in **2.4 s** (live per-citation
verification against the corpus; subsequent calls are faster once the
resolver caches are warm).

```json
{
  "job_id": "98937156-c8ba-411d-ae84-09d04da274b9",
  "entity_id": "tradedarcateg3a-demo-0001",
  "doc_type": "aml_cft_policy",
  "target_jurisdiction": "ADGM",
  "status": "complete",
  "suite_id": null,
  "document_category": null,
  "started_at": "2026-06-21T15:53:06.458942",
  "completed_at": "2026-06-21T16:05:20.188536",
  "output_filename": "aml_cft_policy_TradeDar_Capital_Management_Lt_20260621_160520.docx",
  "section_count": 14,
  "content_chars": 88166,
  "verification_summary": {
    "total_citations": 26, "resolved": 26, "resolved_parent": 0,
    "unresolved": 0, "supported": 15, "unverified_review": 11,
    "corpus_defect": 0, "passed_export_gate": 15,
    "layer": "l1-deterministic"
  },
  "coverage_summary": {
    "expected": 27, "covered": 26, "missing": 1, "phantom_citations": 19
  },
  "provenance": {
    "doc_id": "98937156-c8ba-411d-ae84-09d04da274b9",
    "record_count": 26,
    "corpus_versions": ["VER11.210526"],
    "endpoint": "/api/provenance/98937156-c8ba-411d-ae84-09d04da274b9"
  },
  "sections": [
    { "…": "13 other sections elided …" },
    {
      "index": 7,
      "section_id": "s8",
      "title": "CDD and EDD Procedures",
      "content": "# Section 8 — CDD and EDD Procedures\n\nTradeDar Capital Management Ltd (\"TradeDar\") is required, as a Category 3C Relevant Person authorised by the FSRA in the ADGM, to apply Customer Due Diligence (\"CDD\") measures to all …[truncated]",
      "render_mode": "numbered_list",
      "table_headers": [],
      "portability_layer": 1,
      "coverage_pct_as_drafted": 80.0,
      "drafted_at": "2026-06-21T16:00:44.933618",
      "citations": [
        {
          "ref": "AML 8.1", "matched_ref": "AML 8.1",
          "resolution": "resolved", "strict_support": "unsupported",
          "support_flag": "unverified_review", "passes_export_gate": false,
          "support_overlap": 0.4444, "is_corpus_defect": false,
          "corpus_version": "VER11.210526", "tier": 1,
          "spans": [[498, 544]],
          "reason": "claim not strictly grounded in the cited section text"
        },
        {
          "ref": "AML 8.3", "matched_ref": "AML 8.3",
          "resolution": "resolved", "strict_support": "supported",
          "support_flag": "supported", "passes_export_gate": true,
          "support_overlap": 0.6364, "is_corpus_defect": false,
          "corpus_version": "VER11.210526", "tier": 1,
          "spans": [[1837, 1883], [2927, 2973], [3748, 3794]],
          "reason": ""
        }
      ],
      "coverage": {
        "expected": ["AML 8.1", "AML 8.3", "AML 8.4", "AML 8.6", "AML 8.7"],
        "covered": ["AML 8.1", "AML 8.3", "AML 8.4", "AML 8.7"],
        "missing": ["AML 8.6"],
        "phantom_citations": ["ISORY OUTPUT ON BEHALF OF A NEW CUSTOMER",
                              "SOCIATE OF A PEP", "ISORY SERVICE IS RENDERED"],
        "coverage_pct": 80.0
      }
    }
  ]
}
```

## Size characteristics

* Prod `draft_jobs.sections_json`: max **434 KB**, mean **27 KB** (281 jobs).
  Response ≈ sections_json + ~15% annotation overhead → whole-document
  return, **no pagination**. Defensive 5 MB / 413 guard only.
* Demo job (14 sections, largest doc class): 103 KB response, 2.4 s.
  Frontend should treat this as a one-shot fetch per document view (no
  polling); citations/coverage are computed live so re-fetching re-verifies
  against the current corpus.

## Frontend mapping notes

* Highlight citations in `content` using `citations[].spans` (offsets into
  the raw `content` string; spans include the surrounding brackets).
* Badge colours: `support_flag` — `supported` (green) /
  `unverified_review` (amber) / null with `resolution: "unresolved"`
  (red — draft-gate would strip); `is_corpus_defect` (grey, "known corpus
  defect, re-segmentation pending").
* `coverage.missing` is the honest per-section gap list (the old
  `['AML 8.6']` leak, now a real array).
* `coverage_pct_as_drafted` (stored at draft time) can differ from
  `coverage.coverage_pct` (recomputed vs the current corpus/template) —
  show the recomputed one; the as-drafted value is provenance context.
* Deep-link the provenance drawer to `provenance.endpoint`.

## Security review (self, fresh-eyes)

**Verdict: SHIP.**

* **AuthN** — route bound to the live `auth.dependencies.get_current_user`
  (asserted by test); no token → 401/403 per house convention (live-verified
  403 at the edge, same as neighbours).
* **AuthZ / IDOR** — `job_id` is never trusted as authorisation: after the
  404 existence check, access goes through `routers.register._resolve_entity`
  (the SAME shared tenant guard as A2 register / A10 feedback): job →
  entity → `entity.org_id == principal.org_id` (403 on mismatch, regardless
  of role); legacy no-org entities use owner-or-unowned. Enumerating random
  job_ids yields 404; a guessed-valid foreign job yields 403 with no data.
  404-vs-403 semantics identical to `/api/addin/section-content/{job_id}`
  and `/api/feedback` neighbours.
* **No secret / internal fields** — payload audited (test-asserted):
  `output_path` (filesystem path), `error_message` (raw exception text),
  `entity_context` (questionnaire facts), provenance `model_id`,
  prompts — all excluded. `output_filename`, verdict `reason` strings,
  `corpus_version`, `tier` are all already public on neighbouring
  endpoints.
* **Read-only** — zero ORM writes; corpus.db reached only through the
  existing read-only verifier/coverage helpers. No mutation endpoints in
  the module (test asserts GET-only route table).
* **Injection / traversal** — `job_id` used solely as a parameterised ORM
  filter; no filesystem or SQL string interpolation.
* **DoS surface** — authenticated-only; response bounded by the 5 MB
  sections_json guard (413); verification cost is linear in citations
  (~26 for the largest doc class, 2.4 s worst-case observed). No LLM
  calls, no API spend (`A1_SEMANTIC_SUPPORT` OFF is respected by the
  verifier itself).
* **Guardrails** — `A1_DRAFTING_GATE` drop-in untouched; batch
  `/api/drafting/draft` untouched (regression tests assert neighbour
  routes intact); deploy script verified auth-guard + health post-restart.

## Evidence

* Deploy: `DEPLOY OK: 7bcf671871f969cc7b7c9d2d72ad66b637442bc8 (health=200, auth-guard=403)`; service restarted 07:03:27 UTC (PID 4160003), journal clean.
* Live: unauth → 403; absent job → 404; demo job → 200, 103,481 B, 2.4 s (journal lines for all three on PID 4160003).
* Tests: 14 new, full suite `1100 passed, 1 skipped, 2 xfailed`.
