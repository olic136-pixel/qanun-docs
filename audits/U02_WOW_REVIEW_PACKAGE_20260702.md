# U0.2 — Wow-Review Package (CCD/U0.2-CLOSE)

Date: 2026-07-02 · Lane CCD/U0.2-CLOSE · Final main: **`af06bcf`** (all five phases merged: P1 `2d24668` → P2 `582b29c` → P3 `a042fcd` → P4 `34c591a` → P5 `af06bcf`).
**NOT promoted.** `www.qanun.io` still serves the pre-U0.2 deployment — re-verified at close-out (live domain still carries "Zero hallucination" ×3 and "67,056" ×7).

## 0. The one-screen summary

| Item | Value |
|---|---|
| Final main production-target build (the promote target) | `https://qanun-3izr3ir2f-olivers-projects-9b1cb760.vercel.app` (Ready, 26s build; Vercel deployment-protection means the URL 302s to Vercel SSO unless you are signed into the team — open it from the dashboard or while signed in) |
| Promote command (after your go) | `vercel promote https://qanun-3izr3ir2f-olivers-projects-9b1cb760.vercel.app --scope olivers-projects-9b1cb760` |
| Rollback | The domain simply stays where it is until you promote (auto-assign was disabled in `U02_HYGIENE_S1_PULLED_FORWARD_20260702.md` §1). After a promote, rollback = `vercel promote` the previous production deployment (currently the pre-U0.2 one holding `www.qanun.io`), or `vercel rollback`. The hygiene setting itself: PATCH `autoAssignCustomDomains` back to `true` to restore old behaviour. |
| Integrated AT battery on final main | build clean · vitest **230/230** · copy scan **clean** (11 public routes + source) · leak scan **clean** (21 app routes; before: **538** findings) · no-clip **clean** (21 routes × 950/1280/1440/1728; before: **15**) · axe A/AA **clean** (32 routes @1440 + /compliance/twin ×4 widths) · P4 AT **26/26** · P5 AT **8/8** |
| Integration regressions found | **None** in product code. (Two close-out harness notes in §1.3.) |
| Copy inventory | 52 KEEP honoured · 35 REWRITE / 14 KILL executed except the consciously-parked items in §3.2 (billing $299 fixture, BVI FSRA-application card, corpus filename titles, dashboard mixed-signal card) |
| Parks | **24** items (§6), incl. the 6 backend asks |

Per-phase branch previews (each shows that lane's snapshot in isolation):

| Phase | Branch | Preview |
|---|---|---|
| P1 truth layer | `sprint/u02-p1-truth` | `https://qanun-lmc5rsdub-olivers-projects-9b1cb760.vercel.app` |
| P2 design system | `sprint/u02-p2-system` | `https://qanun-p9v0m6nrm-olivers-projects-9b1cb760.vercel.app` |
| P3 entity setup | `sprint/u02-p3-entity` | `https://qanun-czfh2g5ze-olivers-projects-9b1cb760.vercel.app` |
| P4 document reader | `sprint/u02-p4-docs` | `https://qanun-gzjlrd2o1-olivers-projects-9b1cb760.vercel.app` |
| P5 register | `sprint/u02-p5-register` | `https://qanun-q5pm7mi61-olivers-projects-9b1cb760.vercel.app` |

---

## 1. Integrated AT battery — final main, all five lanes together

Each lane AT'd its own snapshot; this section is the same battery re-run once on the
**merged** result (`af06bcf`), local production build (`next build` + `next start`)
signed into the **prod API** (`NEXT_PUBLIC_API_BASE_URL=https://api.qanun.io`, demo
session, TradeDar entity + the audit's job `98937156-…`).

### 1.1 Numbers

| Check | Result on final main | Pre-U0.2 baseline |
|---|---|---|
| `next build` | clean | — |
| `vitest run` | **230 passed / 0 failed** (19 files) | 154 (old main) |
| `scripts/copy_scan.mjs` — source scan | clean (7 stale-number tokens + MALIS + 2 hallucination claims: 0 hits) | multiple hits |
| `scripts/copy_scan.mjs` — rendered, 11 public routes | **all clean**; `/design` 307 → `/sign-in` | fails throughout |
| `scripts/leak_scan.mjs` — 21 authed routes (incl. project detail, doc detail, certificate) | **clean — 0 findings** | **538** (500 uppercase-tracked els, 11 Python reprs, 11 slashed dates, MALIS ×2, lane labels, Obsidian, UUIDs ×3, snake enums ×5, "1 provisions", A4 certificate) |
| `scripts/noclip_scan.mjs` — 21 routes × 950/1280/1440/1728 (84 route-width checks) | **clean** | **15** clipped-control failures (F1–F4; worst: `/projects/[id]` clipped at 1280) |
| axe WCAG 2.0/2.1 A+AA @1440 — 11 public + 21 app routes (32 total) | **clean on every route** | not run pre-U0.2 |
| `scripts/u02_p4_at.mjs` (reader, live data) | **26/26 PASS** — content endpoint 200 in-browser; s8 text; **86 live citation chips** (`supported`+`flagged`); gap doc `722c1de2…` renders `gap` chips + "verification incomplete"; both edit paths above the fold @1440; axe + no-clip + screenshots ×4 widths | View → progress card, no document |
| `scripts/u02_p5_at.mjs` (register, live data) | **8/8 PASS** — dot-leaders provably stripped (API payload still carries them; page renders none); grouped chrome + provenance line; GAP headline 0; corpus links keyboard-focusable; axe clean ×4 widths | dot-leaders + enum chip + lane labels live |
| Copy-inventory spot-checks (rendered, ~60 assertions) | all pass — detail in §3 | — |

Close-out screenshots from this integrated run: `u02_after_screens/close/p4/` (23 files)
and `u02_after_screens/close/p5/` (4 files) — visually identical to the lane evidence,
which is the point.

Not re-run: `scripts/u02_p3_at.mjs` end-to-end (it **creates a prod entity** each run;
the entity-setup route is covered by the leak/no-clip/axe passes above and the flow
logic by 18 unit tests inside the 230). One prod AT entity from the P3 lane run already
exists — see the cleanup ledger (§7).

### 1.2 Integration regressions

**None found.** Every scan that passed per-lane passes on the merged main; the P4/P5
live AT scripts pass unchanged against the same prod data.

### 1.3 Close-out harness notes (not product regressions, worth knowing)

1. **The local harness must run on port 3000 with `AUTH_TRUST_HOST=1`.** The prod
   API's CORS allowlist admits `http://localhost:3000` only (a run on :3100 renders
   designed error states everywhere — which, credit where due, are designed). And
   without `AUTH_TRUST_HOST`, NextAuth throws `UntrustedHost` in the middleware and
   the **middleware fails open** — `/design` and `/dashboard` served a 200 to an
   unauthenticated curl. On Vercel `trustHost` is implied by the platform env, so
   production is unaffected (P1's 307 verified there and re-verified here), but the
   fail-open default is a hardening note for the backlog: an auth-config error
   silently un-gates every protected route rather than failing closed.
2. `/design` gating, re-verified with the env correct: `307 → /sign-in?returnUrl=%2Fdesign`.

---

## 2. Before / after walkthrough

Before shots: `u02_audit_screens/` (live prod, 2026-07-02 audit). After shots:
`u02_after_screens/p1..p5/` (lane evidence) and `close/` (this run). Paths below are
relative to `~/qanun-docs/audits/`.

### 2.1 Landing + public site (P1)

**Before** `u02_audit_screens/home_1440.png` · **After** `u02_after_screens/p1/home_1440.png` (plus `about/product/pricing/legal-*` ×4 widths).
The site stopped lying. "67,056 provisions. Zero hallucination." → "29,451 provisions.
Every citation checked against them." with every number live from the new public stats
endpoint (documents 2,262 · provisions 29,451 · 6 jurisdictions · corpus-as-of date);
the four contradictory stat families (provisions ×4 values, documents ×4, jurisdictions
×5) collapse to one source of truth that degrades to prose, never to a stale figure.
"0 hallucinations", "0 provisions invented", "no credit card / cancel anytime",
"MOST POPULAR" all dead; the sign-up consent links point at real legal holding pages
that state their own status; footer `#` links and the Saudi-in-status column gone
(Saudi only in the roadmap); metadata rebuilt on `www.qanun.io` with a real OG card;
the founder note restyled as a signed note. Tagline used exactly once.
**AT:** copy scan clean (source + 11 routes); axe clean on all public routes; 36 shots.

### 2.2 App shell + dashboard (P2)

**Before** `u02_audit_screens/dashboard_1440.png` · **After** `u02_after_screens/p2/dashboard_1440.png` (20 routes × 4 widths, 80 files).
The shell dropped its mono-caps voice: nav, buttons, table headers and labels move to
sentence-case Inter with one sanctioned 10px micro-label variant; JetBrains Mono is
reserved for law (rule refs, versions, hashes). 70 internal codes now render through
the display dictionary ("FSRA Category 3 — investment management", "Firm admin",
"Devil's Advocate"); one date format app-wide; "1 provisions" impossible. The K-family
breakages died: `/compliance/calendar` no longer crashes (RAG union bug), preflight
no longer hangs forever (designed slow/timeout/missing-entity states), `/twins` API
failure is distinguishable from empty. Jurisdiction strip wraps at 950.
**AT:** leak scan 538 → **0**; no-clip 15 → **0**; axe clean on all 20 routes; 174 tests then, 230 now.

### 2.3 Entity setup (P3)

**Before** `u02_audit_screens/ix_entities_new_initial_1440.png` (ADGM pre-selected + "Select a jurisdiction above to begin" + "Listening to your answers…") · **After** `u02_after_screens/p3/entities_new_step1_1440.png` … `step4_…` (7 step-states × 4 widths + prefill evidence, 29 files).
The LLM-interview split-pane became a four-step staged form — jurisdiction cards
(nothing preselected; the J1 contradiction string no longer exists in the product),
grouped entity types with plain-language meaning lines, a sectioned details form with
inline validation, and a review step whose rows are test-asserted equal to the POST
payload and the created record. Voice is deleted at the source level (built-bundle
greps clean); the one AI affordance left is an optional one-shot "describe it in a
sentence" prefill whose every value is vocabulary-filtered and marked "Prefilled —
check it". Draft persists in localStorage with an honest restore notice.
**AT (lane, live prod API):** keyboard-only end-to-end in **1.3s**; review = payload =
record; abandon/resume proven; axe + no-clip clean per step. This close-out re-covered
the route with leak/no-clip/axe (clean) without re-creating prod entities.

### 2.4 Document suite — reader + certificate (P4)

**Before** `u02_audit_screens/compliance_documents_98937156-…_1440.png` (stat card, 11 "PHANTOM CITATIONS" Python reprs, no document) · **After** `u02_after_screens/p4/doc_reader_top_1440.png`, `doc_reader_callout_1440.png`, `doc_reader_edit_panel_1440.png`, `doc_reader_gapdoc_top_1440.png`, `documents_suite_1440.png` (23 files; re-shot identically in `close/p4/`).
"View" now shows the document: a 68ch reader column at 15/26 with the draft's own
citations replaced in-text by live A1 chips at their API character spans (**86 chips**
on the audit's AML policy — supported/flagged; a real gap doc shows `gap` chips), the
`[support:]` gate markers stripped, and coverage rendered editorially from structured
arrays ("Section 8 does not cite `AML 8.6` — add it or regenerate the section.");
phantom fragments are counted, never printed. Verification header is honest by
construction — 0-citation drafts read "Drafted — verification incomplete", never
COMPLETE; suite figures are server-truth "Drafting progress" so `/compliance/documents`
finally agrees with `/compliance/gap-analysis`. The edit story is told truthfully:
Edit in Word via sideload + labelled bundle (docx + provenance manifest + certificate),
no pretend one-click. Certificate keeps its best-in-app paragraph, loses the "A4" label.
**AT:** 26/26 live checks; axe/no-clip/leak clean incl. reader + certificate routes.

### 2.5 Register / remediation (P5)

**Before** `u02_audit_screens/compliance_twin_1440.png` (`ADGM_FSRA_CAT3` chip, `A2 · DIGITAL TWIN`, "Assessing the money laundering risks of a business ……… 30") · **After** `u02_after_screens/p5/compliance_twin_1440.png` (+950/1280/1728; re-shot in `close/p5/`).
Obligations group by rulebook with dictionary names ("FSRA Anti-Money Laundering and
Sanctions Rules and Guidance"), gaps leading at both levels; TOC dot-leaders provably
stripped (the API payload still carries them — display strip is marked INTERIM against
the corpus ticket and unit-tested with the audit's exact strings); the five audited
wrong-title FSRA rows carry a subdued "title under review" note (scoped to exactly
that audited set, never inferred); provenance footer names the pinned corpus versions;
remediation chrome adopts the reader idioms (corpus-linked section ref, raised-date).
**AT:** 8/8 live; axe clean ×4 widths; leak/no-clip clean; 17 P5 tests inside the 230.

### 2.6 Corpus / query / alerts (P2 typography + P1 strings)

**Before** `u02_audit_screens/corpus_1440.png`, `query_1440.png`, `alerts_1440.png` · **After** `u02_after_screens/p2/` same names.
Query: "10-AGENT MALIS PIPELINE" → "10-agent research pipeline · six jurisdictions";
Obsidian export renamed; the example queries (already the best strings on the surface)
kept. Alerts: counsel-note bodies kept, house dates ("24 March 2026"), editorial
severity words. Corpus: sentence-case chrome and live counts — but the result titles
are still Title-Cased filenames ("Financial Services 1755948 A Regulatory Perspective
On Paym") because the titles are corpus-side data; that fix lives on the
re-segmentation ticket and this surface will look broken-ish until it lands (§5.6).

### 2.7 Leak-inventory delta (the 538 → 0 class numbers)

| Leak family (inventory count on live prod) | Final main |
|---|---|
| A — internal identifiers/enums (18) | 0 rendered — display dictionary + relabels (leak scan classes A/codename: 0 hits) |
| B — raw UUIDs (4) | 0 — `CopyableDetail` truncated-id idiom everywhere incl. certificate |
| C — Python reprs / PHANTOM jargon (12 lines) | 0 — structured coverage parsing; scan asserts |
| D — grammar/dates (3 + 4 formats) | 0 — `pluralise()` + one house format |
| E — truncated/malformed (9) | display-side fixed (placeholder, sidebar, verify-email, separators); **E2/E4 data truncation remains upstream** (§6 backend asks) |
| F — clipped controls ≥900px (15 across 4 routes) | 0 at all four widths |
| G — placeholder/dead links (8) | 0 — real legal pages, careers/socials removed |
| H — stat/metadata contradictions (4 families + 5 metadata defects) | one live source of truth; canonical/OG/metadataBase on `www.qanun.io` |
| I — overclaims (6) | 0 — every claim now verifiable or hedged into workflow |
| J — contradictory states (6) | J1 gone (P3), J2 reconciled (P4), J6 partially (pricing honest; billing fixture parked); **J3/J4 server-side, J5 corpus ranking — parked** (§6) |
| K — broken surfaces (4) | 0 — calendar, preflight, twins, /design all fixed/gated |
| L — corpus-side data bugs (6 families) | display-mitigated where honest (dot-leaders, titles-under-review, phantom counting); **root fixes on `TICKET_CORPUS_DATA_QUALITY_U02_20260702.md`** |

---

## 3. Copy-inventory execution (52 KEEP / 35 REWRITE / 14 KILL)

### 3.1 Verified done (scan + rendered spot-checks on final main)

Every KILL is gone from the rendered product except the two "as display" items parked
below: zero-hallucination hero, second tagline, credit-card boilerplate, /about stat
block, "0 hallucinations", "MOST POPULAR", MALIS strap + billing feature, R1-fork and
STEP-1a engineering notes (both confirmed absent from `/compliance/documents/new`),
PHANTOM/repr coverage notes, lane labels, `/design` public, constant "50%" relevance
(suppressed — no per-result percentage renders), dot-leader titles.
Spot-checked REWRITEs, all present in their new form: proof bar (live numbers +
"Every citation checked against the corpus"), "Where QANUN must infer, it says so.",
"Ten agents. One research note.", pricing FAQ versioning story, footer jurisdictions
column, sign-up consent wording, "Sign in" (no WELCOME BACK), `/system` "RSA" /
"Devil's Advocate" / "UX Advocate", "Firm admin", GIRA H1 "Application form",
"Rule changes" nav, `/changes` single-line empty state, alerts house dates,
gap-analysis scope naming ("10 of the 10 documents required for a Category 3C
application"), entity page "Tiered template catalogue" (112-count dropped),
"six jurisdictions" on the query strap.

### 3.2 Consciously NOT done (with reasons) — the honest list

| Item (inventory grade) | Status | Reason |
|---|---|---|
| `/billing` $299 + `•••• 4242` vs honest `/pricing` (REWRITE) | **Not done** — $299 still renders | Demo fixture needing a product decision (kill the page, gate it, or price for real) — P1+P2 both parked it; a copy edit can't fix a fake invoice |
| "SUBMISSION PACKAGE — FSRA APPLICATION" on the BVI entity (REWRITE, J4) | **Not done** — still renders on `/entity/fuuturatreasuryinc…` | Server-side: readiness is computed against the ADGM set by the backend; frontend relabelling would fake a fix (backend ask, §6) |
| Corpus result titles = Title-Cased filenames (KILL as display) | **Not done** on `/corpus` | Corpus-side data (leak family L3); on the re-segmentation ticket. P2's `documents.ts` de-slugs *document* titles but the corpus browser deliberately shows corpus truth |
| Dashboard entity card "100% READY · 100% COMPLETE · 2 ALERTS" (REWRITE — readiness should acknowledge open alerts) | **Not done — and unclaimed by any lane** (close-out finding) | Fell between P2 (shell) and the readiness honesty work (P4 did documents, not the dashboard card). Small, but it is exactly the mixed-signal the inventory called; goes on the parks list |
| Licence-option Title Case names ("Category 3C — Asset / Fund Manager") (REWRITE-adjacent) | **Not done** | Asserted verbatim by matrix-parity tests sharing constants with backend registries; re-casing risks the drift those tests exist to prevent |
| E9 alert-title ellipsis without tooltip (UI minor) | Not verified either way | Inventory marked it "acceptable pattern"; nobody claimed it |

---

## 4. §7 — The bake-off verdicts, per surface

Question asked of each surface: **"Would this stand next to Harvey/Legora in a
bake-off?"** — judged against the 12 teardown rules, with the previous review's
failure mode (calling competent bones "done") explicitly in mind.

### 4.1 Landing / public — **Yes, with one reservation**
Evidence: `p1/home_1440.png` vs `harvey_home_hero.png` / `legora_home_hero.png`.
Rules met: 7 (no accuracy numbers as claims; "Every citation checked" is Harvey's
"verify before you share or act" register), 8 (demo terminal shows counts + durations,
no confidence %), 10 (corpus-as-of date on the proof bar), 1 (one electric accent),
12 (claim + live-terminal evidence rhythm; the founder note is better than anything
on either competitor's site). Missed/reserved: **rule 6** — the marketing surfaces
still run uppercase-tracked micro-labels ("START RESEARCHING", proof-bar strip,
footer columns) where Harvey/Legora measure literally zero uppercase elements; P2
deliberately left marketing CSS alone to protect P1's verified screenshots. It reads
as a deliberate brutalist voice rather than a generated tell, but it *is* the single
most visible divergence from both competitors' typography. Rule 4 is met in the hero,
partially below (some section headings sit looser than lh 1.05).

### 4.2 Shell + dashboard — **Close; two honesty gaps keep it from "yes"**
Evidence: `p2/dashboard_1440.png` vs `harvey_assistant_y500.png`.
Rules met: 2/3 (editorial chips, chip-sized colour), 5 (mono only for law), 6 in-app
(one sanctioned variant, scan-enforced), 11 at the lookup box (real PRU/COBS prompts).
Missed: the entity card still says **"100% READY" next to "2 ALERTS"** — a mixed
signal Harvey would never ship (§3.2); and at 1440 the viewport right of the entity
card is dead space once alerts are short — Harvey's zero-state fills that with
example-prompt rows. Bones are genuinely good; the card copy and the idle composition
need one more pass.

### 4.3 Entity setup — **Yes**
Evidence: `p3/entities_new_step1_1440.png` vs Legora's plan/approve pattern.
Rules met: 9 (the flow *is* the approval gate: review step = the plan, "Start the
governance suite" = approve), 2 (no enum anywhere), 11 (the prefill panel with a
domain-real example sentence), 12 (functional microcopy throughout, one idea per
step). The one AI affordance is assistive and marked — closer to the competitors'
philosophy than the deleted voice-orb ever was. Weakest point: step 1's card grid +
prefill panel + rail is slightly more furniture than Legora would use, and the
disabled "Continue" is quiet. No rule broken. This is the surface I'd lead the
bake-off with.

### 4.4 Document suite (reader + certificate) — **Yes for the reader; suite list one notch behind**
Evidence: `p4/doc_reader_top_1440.png`, `doc_reader_callout_1440.png` vs `harvey_vault_y1400.png`.
Rules met: 10 (citation chips carry verdict + version + effective date inline — this
*beats* both competitors' public evidence), 2 (Supported/Flagged/Gaps is exactly
Harvey's graded three-state), 7/8 (honest counts, no scores), 12 (the coverage
callouts are functional, editorial). The certificate paragraph remains the best
writing in the product. Held back by data, honestly disclosed: the H1 still reads
"…Capital Management **Lt**" (filename truncation — backend field ask) and the
document's own front-matter re-emits as body text ("Document Reference: TDC-AML-001
Version: 1.0 [DATE]…") — a drafter/corpus defect the reader now makes visible instead
of hiding. A Harvey reviewer would spot both in the first thirty seconds; neither is
a display bug, both must be fixed upstream before this is bake-off-clean.

### 4.5 Register / remediation — **Structure yes; demo-ability no**
Evidence: `p5/compliance_twin_1440.png` vs `legora_lists_y800.png`.
Rules met: 3 (Satisfied chips on a neutral table = Legora's Done/Waived/Under-review
pattern), 10 (per-row version pins + provenance footer naming `VER11.210526` etc.),
2 ("title under review" is an honest middle state). Missed: **the money moment is
unprovable live** — every demo entity has 0 gaps and 0 remediations, so the
rule-change → redline → accept flow (the product's core differentiator, "Regulation
changes once, remediate everywhere") exists only in unit tests and the empty state.
Legora's monitors page *shows* a change with a source+recency chip. Until the demo
org is seeded with a pending remediation and a gap (backend ask), this surface cannot
win its section of a bake-off, however clean it looks.

### 4.6 Corpus / query / alerts — **Query yes · Alerts yes · Corpus no**
Evidence: `p2/query_1440.png`, `p2/alerts_1440.png`, `p2/corpus_1440.png`.
Query meets 11 (four real practitioner questions) and 12; alerts meet 9/10 (counsel-
voice bodies, named refs, house dates). Corpus fails on sight: result titles are
Title-Cased filenames with embedded ingest ids ("Financial Services 1755948 A
Regulatory Perspective On Paym", "(01) Consultation Paper No. 5 Of 2022 Otclps") —
data-side (family L3), but a bake-off judge doesn't care whose fault it is. Add J5
(a register corpus link can land with the wrong jurisdiction ranked first) and the
corpus browser is the weakest surface in the product. Both fixes are backend/corpus
asks (§6); no amount of frontend polish closes them.

**Overall:** landing, entity setup, the reader and the register chrome would hold a
wall next to Harvey/Legora screenshots today. The bake-off is lost, if it is lost, on
**data**: corpus titles, drafter front-matter, the filename H1, and an empty
remediation demo. That is exactly what the parks list is for.

---

## 5. Repo state

- `qanun` main = `af06bcf`, working tree clean, in sync with `origin/main`.
- All five U0.2 branches pushed and in sync with origin:
  `sprint/u02-p1-truth` (`4465338`) · `sprint/u02-p2-system` (`b23e3b5`) ·
  `sprint/u02-p3-entity` (`ef12db7`) · `sprint/u02-p4-docs` (`92d74df`) ·
  `sprint/u02-p5-register` (`5d9a267`).
- Other branches on origin (pre-U0.2, unchanged): `sprint/exec-vercel`,
  `sprint/max5-suite-ui`, `sprint/max5-ui`, `sprint/max6-k-frontend`,
  `sprint/max6-ui-polish`, `sprint/max9-a2-a3-twin`, `sprint/p0-sec-ui`,
  `sprint/u0-design-system`, `sprint/u0-drafter-cert`, `sprint/u0-surfaces`.
- `qanun-api` main = `8472b51` (P1 public-stats endpoint, deployed) — no other
  backend change in U0.2.

## 6. Parks ledger — consolidated from all five lanes + close-out

**Backend asks (the six, plus two):**
1. **Verification rollup on submission status** — per-document verification on
   `/api/submission/{id}/status` so suite figures can be verification-aware (P4).
2. **Catalogue-universe reconciliation** — governance 49-doc catalogue vs 10-doc
   submission package vs 64-template list vs (formerly) "112 templates"; J3
   COMPLETE-vs-Not-Started and J4 BVI-entity-on-ADGM-set are the same server data
   question (P4; J4 is also §3.2's not-done REWRITE).
3. **Obligation-catalogue regeneration** — kills the INTERIM `stripDotLeader`
   (family 1) and `titleUnderReview`/`FSRA_TITLES_UNDER_REVIEW` (family 2); both are
   comment-tagged for deletion against `TICKET_CORPUS_DATA_QUALITY_U02_20260702` (P5).
4. **Demo-data seeding** — one pending remediation + one gap on the demo org; the
   register's accept/redline flow is currently unprovable live (P5; also MAX-9 park).
5. **Filename-title backend field** — a real document title so the reader H1 stops
   being a de-slugged filename ("…Management Lt", E2); also E4's corpus doc titles (P4).
6. **`/corpus` ranking** — register section-ref links land on a fuzzy 20-result
   search that can rank the wrong jurisdiction first (J5) (P5).
7. Structured coverage notes from the drafter (currently string-parsed client-side) (P2).
8. Stale persisted `unique_citations` backfill on `/api/drafting/status` (8 of 10 demo
   docs carry the audit's dishonest 0) (P4).

**Corpus/drafter tickets (filed, root-cause fixes):**
9. `TICKET_CORPUS_DATA_QUALITY_U02_20260702.md` — six families incl. dot-leaders,
   wrong-heading titles, filename titles, lost whitespace, phantom-fragment extractor,
   global certificate ledger row numbers.
10. Drafter re-emits document front-matter as in-content headings (visible honestly in
    the reader) (P4).

**Frontend/product parks:**
11. `/billing` $299 + `•••• 4242` demo fixture vs honest `/pricing` — product decision (P1/P2).
12. Dashboard entity card "100% READY + 2 ALERTS" mixed signal — copy-inventory
    REWRITE, unclaimed by any lane (close-out finding, §3.2/§4.2).
13. Dashboard idle composition at ≥1440 when alerts are present (dead right column;
    example prompts currently earn their keep mainly at 950) (close-out, §4.2).
14. In-app section-level document editing — needs backend mutation endpoints; honest
    Word path shipped instead (P4).
15. Suite table "Required set / Additional templates" split (labelled today, not split) (P4).
16. `EditInWordPanel` copy update when the A6 cohort/Office-Store distribution lands (P4).
17. Marketing-surface uppercase micro-label voice vs teardown rule 6 — deliberate
    brand call to make at wow-review (close-out, §4.1).
18. Licence-option Title Case names (matrix-parity tests pin them) (P2).
19. `/onboarding` jurisdiction picker — untouched, copy already KEEP (P3).
20. `/api/entity-setup/session` server-side drafts unused (localStorage carries the
    draft); revisit if cross-device resume is wanted (P3).
21. GET `/api/entities/{id}` omits `target_jurisdiction` (AT works around via list
    endpoint); `validation_summary` composes a raw licence code (display-swapped) (P3).
22. No in-app create-twin flow for the `/twins` empty state to target (P2).
23. Pre-existing eslint debt: 17 errors on old files (`next build` is the gate and passes) (P1).
24. Middleware fails open on NextAuth `UntrustedHost` misconfiguration — fail-closed
    hardening ask (close-out, §1.3).

## 7. Prod cleanup ledger

| Artefact | Where | Origin | Action |
|---|---|---|---|
| Entity `u02p3atentitydeletable-category3c-e2f34720` ("U02-P3 AT Entity — deletable", no suite started) | prod demo org — visible in the sidebar of every demo-session screenshot | P3 final AT run | delete at leisure |
| Users `t4-smoke-a@example.com`, `t4-smoke-b@example.com` | prod DB | T4 router smoke (2026-07-01) | delete at leisure (same class as e2e-prod-smoke accounts) |
| One smoke NDA artefact under `outputs/nda/` | prod disk | T4 | delete at leisure; retention policy is a T4 open item |

---
*Close-out lane CCD/U0.2-CLOSE, 2026-07-02. No product code was changed by this lane;
the only writes are this package and the `close/` screenshot evidence.*
