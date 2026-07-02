# U0.2 — Design-Elevation Sprint Report

Date: 2026-07-02 · Sprint CCD/U0.2 · Per-lane sections appended as lanes close.

---

## P1 — Truth Layer (CCD/U0.2-P1)

**Repos:** `qanun` (frontend, branch `sprint/u02-p1-truth` → merged `main 2d24668`) ·
`qanun-api` (one additive endpoint, `main 8472b51`, deployed to prod).
**No promotion:** `www.qanun.io` still serves the pre-P1 deployment (verified post-merge:
old copy incl. "Zero hallucination" still live on the domain; the new `main` build
`qanun-cuzt7wmaa-…vercel.app` is Ready and awaits Oliver's `vercel promote` after wow-review.

### 1. Stats — single source of truth

**Decision: no suitable endpoint existed → one tiny additive endpoint was added.**
The 104,924 figure the audit saw on `/system` comes from the auth-gated, MCP-dependent
`/api/system/status`, and it counts **all** sections including superseded rulebook
versions (2,654 docs / 104,924 sections all-versions). `/api/system/corpus-health` is
also auth-gated and leaks the corpus filesystem path. Neither was usable publicly.

**New:** `GET /api/public/corpus-stats` (qanun-api `routers/public_stats.py`):
- Unauthenticated, org-free, **no parameters**, read-only (`mode=ro` sqlite URI),
  15-min in-process cache, opaque 503 on failure (no path/sqlite detail leaks).
- Honest definitions: `documents` = current documents (2,262); `provisions` =
  sections of **current** documents (29,451 — not the all-versions 104,924);
  six live jurisdictions grouped server-side from internal `source_entity` values
  so no internal enum leaves the API (ADGM incl. FSRA/ADGM_RA/ADGM_COURTS; DIFC incl.
  DFSA/DIFC_COURTS; VARA; El Salvador; BVI; Panama). MONDAQ/UAE_FEDERAL count toward
  totals but are not presented as jurisdictions. `last_updated` is date-only.
- **Security review (self, documented in module docstring): SHIP.** Aggregate public
  counts only; no user input reaches SQL; cache bounds abuse cost; no org/user/entity
  data; internal enums and paths verified absent by test.
- Tests: 7 new (`tests/test_public_stats.py`) incl. no-internal-enum and no-Saudi
  assertions; **full backend suite 1107 passed / 1 skipped / 2 xfailed** (baseline
  1100+1+2). Deployed via `scripts/deploy_prod.sh` per DEPLOY.md — `DEPLOY OK 8472b51
  (health=200, auth-guard=403)`. Live: `curl https://api.qanun.io/api/public/corpus-stats`
  → 2,262 / 29,451 / 6 jurisdictions / last_updated 2026-06-30.

**Frontend:** `lib/marketing/corpusStats.ts` fetches it server-side with
`revalidate: 3600` on every marketing page (`/`, `/about`, `/product`, `/pricing`,
footer). On fetch failure every surface **degrades to prose without numbers** —
never to a stale figure (stat blocks are omitted, hero falls back to
"Every citation checked against the corpus."). Jurisdiction lists (hero line already
static-correct; live grid; footer column) derive from the payload; the constants
module supplies names only as an offline fallback.

**Important honesty note for wow-review:** the truthful provision count is **29,451**,
not the 65–67k the site used to claim. The marketing numbers were never real
(no query of the corpus produces them). Landing/About/Pricing now show 29,451 —
smaller, but defensible to the digit.

### 2. Before → after, worst offenders

| Where | Before (live prod, verbatim) | After |
|---|---|---|
| Landing hero | "67,056 provisions. Zero hallucination." | "29,451 provisions. Every citation checked against them." (number live) |
| Landing meta / root meta | "…65,822 provisions. Three jurisdictions. Zero hallucination." | No numbers in metadata; "Every claim graded against pinned corpus provisions." |
| Proof bar | "84% AVERAGE GROUNDING RATIO — 0 PROVISIONS INVENTED" + stale per-jurisdiction counts | live docs/provisions/jurisdictions + "Every citation checked against the corpus" + "corpus as of ‹date›"; per-jurisdiction line from payload |
| `/product` Quick Lookup stat | "0 hallucinations" + "Cited and accurate." | "Inline — citations on every answer" + "Cited inline, so you can verify before you rely on it." (teardown rule 7: reliability as workflow, not a score) |
| `/product` Reference heading | "Every claim grounded. Every provision cited." / "QANUN does not speculate." (beside a SPECULATIVE tier) | "Where QANUN must infer, it says so." — the tier system *is* the story |
| `/product` heading | "A 10-agent pipeline that thinks like a senior lawyer." | "Ten agents. One research note." |
| `/about` stat block | 2,366 / 65,822 / **3** jurisdictions (contradicting landing's 6) | live 2,262 / 29,451 / 6 |
| Pricing FAQ | "ingest new documents within hours of publication… over 2,366 documents and 65,822 sections" | versioning story (each provision carries rulebook version + effective date) + live counts; no latency SLA claimed |
| CTA strip / sign-up | "NO CREDIT CARD REQUIRED · CANCEL ANYTIME" / "14-day free trial. No credit card required." (no billing, no trial config exists) | "Access on request while pricing is finalised" / "Full research access while pricing is finalised — no payment is taken." |
| Footer STATUS column | ADGM · VARA · El Salvador · **Saudi Arabia** (a COMING market listed on the status list; 3 live ones omitted) | "Jurisdictions" column: the six live ones from the stats payload; Saudi appears **only** in the landing COMING roadmap |
| Footer links | Careers/Privacy/ToS/Security all `href="#"`; two `#` social icons | Careers + socials removed; legal links → real holding pages; `hello@qanun.ai` in the bottom bar |
| Sign-up consent | "I agree to the Terms of Service and Privacy Policy" — **both `href="#"`** | Links → `/legal/terms` + `/legal/privacy` with honest wording: "…which are in final legal review — the linked pages state their current status and what applies in the meantime." |
| Founder block | Pull-quote styling + "Author of the COBS 23.12.2 brief reproduced in the research terminal above." | Kept (it is the best copy on the site) but restyled as a signed founder's note: "A NOTE FROM THE FOUNDER" kicker, no quotation-mark ornament, byline only; the self-attribution line cut |
| `/query` strap · `/billing` · GIRA H1 | "10-AGENT MALIS PIPELINE" / "Full MALIS agent pipeline" / "GIRA Application Form" | "10-agent research pipeline · six jurisdictions" / "Full 10-agent research pipeline" / "Application Form" (minimal string fixes only; app copy otherwise left to P2) |
| Landing tagline | "THE LAW, DECODED." twice on one page | Second use replaced: "PUT A QUESTION TO THE CORPUS." |
| Demo terminal metadata | "14 claims · grounding 84% · 78s" | "14 claims · 3 provisions cited · 78s" (counts + durations only, rule 8); the "72% — Advanced" numeric-confidence readout in the product demo panel removed |
| Dead components | `HowItWorks` / `TrustSection` / `ProductPanel` / `CapabilityCards` (unimported, carrying 65,822 / 2,484 / "No hallucination — ever") | deleted |

### 3. Legal holding pages

`/legal/terms`, `/legal/privacy`, `/legal/security` — one designed `LegalHolding`
template (marketing chrome, status panel, "what it will cover", "our practice today",
contact). Each states plainly: *"This document has been drafted and is being finalised
with counsel. The settled version will be published on this page before general
availability… Until then, nothing on this page is a contractual term."* — wording tied
to the C1 publish pipeline; the pre-counsel drafts in `~/qanun-docs/legal/` are **not**
published. "Our practice today" lists only commitments that are already true (no
payment taken; no training on customer data; encrypted in transit/at rest;
delete-on-request via hello@qanun.ai).

### 4. Metadata

- `metadataBase` → `https://www.qanun.io` (was `qanun.vercel.app` on **every** page).
- Per-route `canonical` + `og:url` via relative alternates from the root layout —
  verified per-route on the built site (`/about` → `https://www.qanun.io/about`, etc.).
- `public/og-card.png` (1200×630 @2x): restrained brand card from the design tokens —
  ink field, white Q block + wordmark, "THE LAW, DECODED." with the electric accent,
  hairline footer with the six jurisdictions. No gradients, no sparkles. Wired as
  `og:image` + `twitter:image`; `summary_large_image` no longer points at nothing.
- Title template `%s — QANUN`; page-specific titles/descriptions on About/Product/
  Pricing/Legal; no corpus numbers and no accuracy claims anywhere in metadata.
- `/design` removed from the middleware public allowlist → unauthenticated request
  307s to `/sign-in` (audit A14/K4 closed). Verified on the built site.

### 5. AT evidence

- **Banned-copy scan** — `scripts/copy_scan.mjs` (re-runnable at close-out; scans the
  local build via `next start` or any `BASE_URL`): source scan (no 67,056 / 65,822 /
  2,382 / 2,366 / 2,484 / 63,397 / 13,337, no MALIS, no hallucination claims) +
  rendered scan over 11 public routes (hallucinat*, no credit card, cancel anytime,
  qanun.vercel.app, MALIS, GIRA, "provisions invented", "grounding ratio", stale
  numbers, `href="#"`, Saudi in footer / outside the roadmap, canonical + og:url on
  www.qanun.io, og:image + twitter:image present, `/design` gated). **Result: clean.**
- **Vitest:** 165 passed / 0 failed (baseline 154; +11 truth-layer tests incl. updated
  legacy ProofBar/pricing/footer contracts). **Build:** clean (`next build` ✓).
- **Backend suite:** 1107 passed / 1 skipped / 2 xfailed.
- **axe (WCAG 2.0/2.1 A+AA, animations settled, full-page scroll):** clean on all nine
  public routes (`/`, `/about`, `/product`, `/pricing`, `/sign-in`, `/sign-up`,
  `/legal/*`). This required a real contrast pass (faint white/20–white/40 and
  black/25–black/50 micro-text lifted to AA-passing tokens; in-text links underlined;
  the decorative demo terminals also marked `aria-hidden` and the proof-bar scroll
  region made keyboard-focusable).
- **Screenshots:** 9 routes × 4 widths (1280/1440/1728/950), scrolled so in-view
  sections render → `~/qanun-docs/audits/u02_after_screens/p1/`.

### 6. SHAs / deployments

| What | Ref |
|---|---|
| qanun-api endpoint | `b55fa94` on `sprint/u02-p1-public-stats`, merged `main 8472b51`, **deployed to prod** (DEPLOY OK, health 200, auth-guard 403) |
| qanun truth pass | `73f08da` (stats+copy), `02e05f5` (legal+consent+/design), `fe17509` (metadata+OG), `4465338` (AT tooling) on `sprint/u02-p1-truth` |
| qanun merge | `main 2d24668` (merge --no-ff), pushed |
| Vercel | branch preview `https://qanun-lmc5rsdub-olivers-projects-9b1cb760.vercel.app`; main production-target build `https://qanun-cuzt7wmaa-olivers-projects-9b1cb760.vercel.app` (Ready, **NOT promoted** — `www.qanun.io` unchanged, verified) |

### 7. Carry-forwards (out of P1 scope, noted for later lanes)

- App-side copy (enums, coverage notes, Python reprs, date formats, readiness
  contradictions) — P2's lane; only MALIS/GIRA headline strings and the two
  hard-coded corpus numbers on app pages were touched here.
- `/pricing` vs `/billing` contradiction: pricing page is now honest ("on request",
  no badge), but `/billing`'s $299/•••• 4242 demo fixture remains an app-surface item.
- Pre-existing eslint debt: 18 errors on old main → 17 on this main (none in files
  added by P1; `npm run lint` was not a P1 gate, `next build` is and passes).
- The corpus `last_updated` renders as ISO date (`2026-06-30`); if D3/date-format
  standardisation lands a site-wide format, the proof bar should adopt it.

---

## P2 — App-wide design-system hardening (CCD/U0.2-P2)

**Repo:** `qanun` only (branch `sprint/u02-p2-system` → merged `main 582b29c`). Backend untouched.
**No promotion:** `www.qanun.io` still serves the pre-U0.2 deployment (verified post-merge: "Zero hallucination" / 67,056 still live on the domain). Branch preview `https://qanun-p9v0m6nrm-…vercel.app`; main production-target build `https://qanun-qt4wyiz9n-…vercel.app` (awaits `vercel promote`).

### 1. Typography hierarchy — rebuilt in the token layer

Two families, strict roles (teardown rules 4/5/6). **Inter is the voice** — display → labels, all sentence case; **JetBrains Mono is reserved for law**: citation refs, rule ids, corpus versions, hashes. Zero uppercase-tracked text outside ONE sanctioned variant.

| Role | Spec | Use |
|---|---|---|
| `text-display` | 32/34 · −0.02em · 600 | display moments (tightens as it grows) |
| `text-title` | 20/24 · −0.015em · 600 | page titles |
| `text-heading` | 16/22 · −0.01em · 600 | section headings |
| `text-ui` | 14/20 · 500 | controls, nav |
| `text-body` | 13/20 · 400 | dashboard body |
| `text-caption` | 11/16 · 400 | table meta, hints |
| `text-label` | 11/15 · +0.01em · 500 | form/table labels, kickers — **sentence case, sans** (re-spent: was 10px mono +0.24em) |
| `text-microlabel` | 10/14 · +0.08em · 500 · uppercase | **the ONE sanctioned uppercase style** — only via `<MicroLabel>` / `.micro-label`, which emit `data-ds="micro-label"` (the AT whitelist hook). Sparing: stat eyebrows, section kickers |

Applied at the primitives so it cascades: `DSButton` (was mono-caps +0.12em → 13px medium sentence case), `DSTableHeaderCell`, `DSField` label, `.sidebar-link-new` (nav was 11px mono-caps +0.15em → 13px sentence case), `.data-table th`, A1 badges (`SUPPORTED` → editorial "Supported/Resolved/Flagged/Stripped/Gap", rule 2 — colours/icons/dot-shapes untouched). Then ~45 app files converted off inline mono-caps (376 occurrences on old main). Mirrored in `lib/design-tokens.ts` (`tokens.type`). `/design` (auth-gated since P1) now documents the hierarchy and the mono-is-for-law rule.

### 2. Reflow, never clip — audit family F closed

Old app (live prod), measured by the new no-clip AT: **15 interactive-element clip failures**; P2 build: **0 at 950/1280/1440/1728**.

| Audit | Fix |
|---|---|
| F1 documents table @950 (STATUS cut, ACTIONS off-viewport) | low-priority columns fold below 1100px; table in a named, keyboard-focusable scroll region (visible affordance) |
| F2 `/projects/[id]` @950 **and** 1280 (worst offender) | selects → wrapping pill filters; claims table → focusable labelled scroll region; grid column `minmax(0,1fr)` + accordion min-width chain (the cycle triggers were 1113px wide even at 1728) |
| F3 certificate VERDICT/ROW HASH @950 | labelled scroll region on the ledger table |
| F4 dashboard jurisdiction strip @950 | tabs wrap (all six rendered from `lib/constants/jurisdictions`) |
| E1 placeholder truncation | short placeholder + `aria-label` |
| E6 sidebar self-truncation | rail 220→240px, sans (narrower than mono-caps), `title` tooltips on truncation |
| sidebar/dashboard crush @950 | two-column dashboard stacks below 1100px; alert cards keep icons + editorial severity words |

### 3. Display dictionary — `lib/display/`

`labels.ts` (single module): **70 codes mapped across 7 families** — licence categories (7: `CATEGORY_3C` → "Category 3C — asset manager", `BVI_BUSINESS_COMPANY` → "BVI business company"…), licence packs (`ADGM_FSRA_CAT3` → "FSRA Category 3 — investment management"), roles (6: `firm_admin` → "Firm admin"), pipeline agents (15: `rsa` → "RSA", `devils_advocate` → "Devil's Advocate"), rulebooks (18: `VARA-CRM` → "VARA Compliance & Risk Management Rulebook", used as tooltips on mono citation-prefix chips), portability layers (5, + `<PortabilityLegend>` one-liner legend rendered where the chips appear), job/doc statuses (18). Plus `sectionLabel('s7')` → "Section 7". **Unknown code → humanised text (never the raw code) + warn-once in dev.**
`format.ts`: ONE date format app-wide ("21 June 2026" / "21 June 2026, 16:05") replacing the four found by the audit (D3), and `pluralise()` killing "1 provisions" (D1).
`coverage.ts`: parses the raw coverage-warning strings — Python reprs and "PHANTOM CITATIONS" jargon (C1/C2) never render; phantom lines become "Section 1 — 2 citations could not be verified against the corpus and were removed." (the chopped mid-word fragments are counted, never shown); not-cited lines cite the real refs in mono with coverage %.
`documents.ts`: strips "— composed" suffixes (A17), sanitises template descriptions carrying engineering notes/decision-log/founder-name (A8/A9), derives display titles from filename slugs (E2), strips register TOC dot-leaders (display-side; corpus fix stays on the re-seg ticket).
Job UUIDs (B1–B3) demoted everywhere to a shared `<CopyableDetail>` row (truncated display, one-click copy of the full id). Lane labels gone: "A2 · DIGITAL TWIN" → "Live register", "A3 · RULE-CHANGE → REDLINE" → "Rule-change redlines", "QANUN · A4 PROVENANCE" → "Qanun · Certificate of provenance"; "A1-verified" → "verified"; "Export to Obsidian" → "Export memo (Markdown)".

### 4. Marketing copy out of the product

Register pitch paragraph → dismissible first-run explainer (localStorage-persisted) with a one-line functional subhead. Dashboard idle state applies rule 11: three domain-real example prompts (PRU 1.3.3(2), COBS 23.12.2, PRU 3.6) that fill the lookup box — no dead space at 950. Empty states across app surfaces now name a next action; `/twins` API failure is a designed error state distinct from the true empty state (K3).

### 5. Broken surfaces (family K) — root causes

- **K1 `/compliance/calendar` crash:** backend `_rag_status()` returns `UPCOMING` for null/unparseable due dates; the frontend `RagStatus` union and `RAG_CONFIG` lacked it → `RAG_CONFIG[rag].tw` = the `reading 'tw'` TypeError on every load with such an obligation. Fixed: union + config extended, safe `ragConfig()` accessor degrades unknown values to a neutral chip. RAG chips now editorial ("Due soon", not "RED"). Verified loading clean (no pageerror).
- **K2 preflight hang:** frontend bug, two-part. (a) With no `entity_id` in the URL the fetch effect early-returned and `loading` stayed `true` forever — the unbounded "Loading preflight" skeleton the audit saw. Missing entity is now a designed state. (b) The fetch had no budget — added honest progressive state (slow notice at 8s) + 30s timeout → designed error with Retry. The backend endpoint itself is synchronous registry+DB reads (fast); no backend change needed.
- **K3** `/twins` 404-vs-empty: fixed (designed error state). **K4** `/design`: closed in P1; content updated in P2.

### 6. AT evidence

| Check | Old app (live prod) | P2 build |
|---|---|---|
| `scripts/leak_scan.mjs` (enums/UUIDs/reprs/codenames/plurals/dates + computed-style uppercase outside `[data-ds="micro-label"]`) | **FAIL — 538** (500 uppercase-tracked els; 11 Python reprs; 11 slashed dates; MALIS ×2; lane labels; Obsidian; UUIDs ×3; snake enums ×5; "1 provisions"; A4 certificate) | **PASS — clean** |
| `scripts/noclip_scan.mjs` (20 routes × 950/1280/1440/1728; bounding boxes vs viewport, scroll regions must be keyboard-focusable + named) | **FAIL — 15** | **PASS — clean** |
| axe WCAG 2.0/2.1 A+AA (20 app routes @1440, real session/data) | — | **clean** (required lifting legacy greys gray-400/500, black/30–40, #16A34A small text to AA; accessible names on selects/inputs/switches) |
| vitest | 165 baseline | **174 passed / 0 failed** (+9 display-layer tests) |
| `next build` | — | clean |

Scans run signed-in against the built app + prod API (demo session, real data — the same entity/job the audit used). Screenshots: **20 routes × 4 widths → `u02_after_screens/p2/`** (80 files). Worst-clip before/after: `u02_audit_screens/compliance_documents_950.png` / `projects_tradedarcateg3a-demo-0001_1280.png` vs `u02_after_screens/p2/compliance_documents_950.png` / `projects_tradedarcateg3a-demo-0001_1280.png`.

### 7. SHAs / deployments

| What | Ref |
|---|---|
| Foundation (tokens, primitives, dictionary, shell, dashboard, K1/K2) | `d5e47d3` |
| /design + AT tooling + display tests | `6878e12` |
| App-wide conversion (4 parallel lanes) | `74306e9` |
| Live-scan fixes (plurals, accordion min-width) | `e9eb1f6` |
| axe A/AA pass | `b23e3b5` |
| Merge | `main 582b29c` (--no-ff), pushed; **NOT promoted** — `www.qanun.io` unchanged, verified |

### 8. Deferred (with reasons)

- **Entity setup** (`compliance/entities/new`, `components/qanun/cee/*`) incl. audit J1 (pre-selected-ADGM vs "Select a jurisdiction") — its own later lane by scope; shared chrome (shell, preflight, gira headers) done.
- **Document-suite structural redesign** — later lane; P2 did typography + the named leak/clip fixes only.
- **Marketing typography** (`.btn-primary`/`.btn-secondary`/`.micro-label` CSS classes, MarketingNav uppercase, QanunWordmark) — marketing surfaces are P1/P4 territory; changing them would churn P1's verified screenshots. P4 should apply rule 6 there.
- **`/billing` $299 + `•••• 4242` vs `/pricing` "on request"** — demo fixture; needs a product decision, not copy.
- **Licence-option Title Case names** ("Category 3C — Asset / Fund Manager" etc.) — asserted verbatim by matrix-parity tests and sourced from constants shared with backend registries; re-casing risks drift the tests exist to prevent.
- **Corpus-side data bugs (family L)** — TOC dot-leader titles, lost whitespace, filename titles, phantom-fragment extractor: display-mitigated here; the real fix stays on the corpus re-segmentation ticket.
- **Backend niceties**: coverage notes should be emitted structured (currently string-parsed client-side); `exporting` status unmapped in the shared dictionary (local override used); no in-app create-twin flow for the `/twins` empty state to target.

---

## P3 — Entity-setup rebuild (CCD/U0.2-P3)

**Repo:** `qanun` only (branch `sprint/u02-p3-entity` → merged `main a042fcd`). Backend untouched (business logic read-only; the flow drives the existing entity-creation contract).
**No promotion:** `www.qanun.io` still serves the pre-U0.2 deployment (verified post-merge: "Zero hallucination" / 67,056 still live). Branch preview `https://qanun-czfh2g5ze-olivers-projects-9b1cb760.vercel.app`; main production-target build `qanun-6jgm9b1iy-…` (awaits `vercel promote`).

### 1. Flow map — the form IS the flow

`/compliance/entities/new` rebuilt from the LLM-interview split-pane (J1's contradictory
"Select a jurisdiction above to begin" + pre-selected ADGM + "Listening to your answers…"
ghost panel) into a four-step staged flow on the P2 token layer:

1. **Jurisdiction** — six designed cards from `lib/constants/jurisdictions` (equal heights
   via grid-stretch + min-height, `hyphens:none`/`text-wrap:pretty` (no mid-word wraps),
   one Lucide icon set at strokeWidth 1.5, `aria-pressed` selection). Nothing preselected;
   the J1 contradiction string no longer exists in the product (asserted by test + AT).
2. **Entity type** — options with display-dictionary labels + a what-this-means line each,
   grouped "Licensed activity" / "No licence required" (every jurisdiction offers an
   unlicensed track; SV gated tracks render visible-but-disabled "Coming soon").
3. **Details** — sectioned form: identity / licensing position (type chip + Change link,
   MLRO·CO·SEO with leave-blank hints) / activities (per-jurisdiction chip vocabulary) /
   structure (AUM band select, fund-manager toggle). Inline validation (name required;
   licensed types need ≥1 activity), calm error copy, focus moved to first error.
4. **Review** — every value in labelled rows (optionals honestly "Not provided"), per-group
   Edit links back to the owning step, explicit "Start the governance suite" checkbox
   (default on — preserves the old flow's behaviour), background corpus check
   (ADGM/VARA/EL_SALVADOR via the existing `/api/entity-setup/validate`; never blocks
   create; failure degrades to a quiet "corpus check unavailable" line; the backend's raw
   licence code in `validation_summary` is swapped for its display label client-side).

**Backend contract unchanged:** `POST /api/entities` → (optional) `PATCH /api/entities/{id}`
profile → (optional) `POST /api/drafting/suite {tiers:[1,2]}` → redirect to suite job or
`/entity/{id}`. Duplicate name+type (API's `created:false`) is a designed state: "already
exists" panel with "Open the existing entity" + "Change the name" — nothing is written.

**Save-and-resume:** whole wizard state persists to localStorage on every change
(`lib/entity-setup/state.ts`, versioned key, foreign/malformed drafts dropped, entity types
validated against the stored jurisdiction on restore). Return shows a "Draft restored from
‹time›" notice + Start over. Decision note: the backend `/api/entity-setup/session` store
exists but is keyed by a server id the client would have to keep locally anyway and its
blob is shaped for the old conversation flow — localStorage carries the draft directly.

**Steps/progress:** numbered StepRail (done steps clickable; reaching review through the
rail still passes details validation); focus moves to the step heading on every transition
(effect-driven, deterministic — the original rAF version could steal focus mid-typing).

### 2. Voice OUT — proof

Deleted entirely: `components/qanun/voice/VoiceOrb.tsx`, `lib/voice/extractQuestion.ts`,
`app/api/voice/{speak,transcribe}` (OpenAI TTS/Whisper proxies), the CEE
`ConversationEngine` + `EntityProfilePane` ("Listening to your answers…"), and the VOICE
button/voiceMode/TTS paths inside `PreflightConversation` (the documents-preflight chat
itself stays — not this lane's surface). `package.json` carried no speech deps (voice was
server-proxied) — none to remove.
`grep -ri "voice\|speech\|listening" app components lib` → 6 hits, all pre-existing
typography comments ("Inter is the voice", "house voice") — no code. Built bundle
(`.next/static` + `.next/server`) greps clean for VoiceOrb / voiceMode / "Listening to
your answers" / `/api/voice`.

### 3. The AI affordance — assistive, not the medium

One optional "Describe the entity in a sentence" panel on step 1
(`components/qanun/entity-setup/PrefillPanel.tsx` + `lib/entity-setup/prefill.ts`): a
single one-shot extraction over the **existing `/api/cee/chat` proxy** (the same route the
old flow used for its extraction pass — no chat, no interview). Every returned value is
filtered against the flow's own vocabularies (jurisdiction, entity-type options,
activity lists, AUM bands); free-text names pass through. Prefilled fields carry a
"Prefilled — check it" chip and are ordinary inputs; the mark clears on first edit.
Failure/empty extraction is a calm inline note. Live proof (prod build):
"Meridian Digital Custody, a VARA-licensed virtual asset custodian… MLRO Fatima Al Rashid,
about USD 40m" → jurisdiction VARA + `vasp_cust` + name + MLRO + "USD 25–100m" + Custody
services, 6 marks, mark-clears-on-edit verified
(`entities_new_step3_prefilled_1440.png`). Note: the old flow's model id
(`claude-sonnet-4-20250514`) is retired and 404s — the entire conversation flow had been
silently broken; prefill and the preflight chat now use `claude-opus-4-8`.

### 4. Option data — honest sourcing

`lib/display/entityTypes.ts` centralises entity types + activity vocabularies per
jurisdiction with an explicit honesty note: **no backend endpoint serves this today**;
sets are mirrored from the app's existing sources (classify page categories, the
governance-suite launcher's registry-pinned LICENCE_TYPES, `sv-categories.ts`,
jurisdiction-questions option lists). `lib/display/labels.ts` extended with the ~30 codes
the flow submits so every surface renders the same human label. Jurisdiction cards come
from `lib/constants/jurisdictions` (six everywhere).

### 5. AT-3 evidence

| Proof | Result |
|---|---|
| End-to-end ADGM entity, **keyboard only** (`scripts/u02_p3_at.mjs`: Tab/Space/Enter/typing only, request-intercepted) | **1.3 s** from step-1 settled to `/entity/…` redirect (budget 180 s) — prod API, final run |
| Abandon/resume | Filled to step 3 (name + activity), hard reload → step 3 restored, values intact, restore notice shown; Start over clears the draft |
| Review = POST payload = created record | Review rows asserted equal to the intercepted `POST /api/entities` payload AND the API record re-fetched after creation (name/type/jurisdiction/activities/MLRO; jurisdiction via the list endpoint — the single-entity GET omits `target_jurisdiction`, pre-existing backend shape) |
| No voice code | Source grep + built-bundle grep clean (§2) |
| axe WCAG 2.0/2.1 A+AA | Clean on every step ×4 states (steps 1–4, validation-errors, prefill-error, duplicate) at 1440 |
| No clipped controls | Clean per step at 950/1280/1440/1728 (`u02_p3_screens.mjs`); shared `noclip_scan` (now incl. `/compliance/entities/new`) clean |
| Designed states | initial (no selection — no contradiction), inline validation errors, prefill failure, duplicate name, create error w/ retry, resume notice — all screenshotted |
| Leak scan | clean (route added to the shared scan set) |
| vitest | **192 passed / 0 failed** (baseline 174 + 18 P3: option dictionary, draft persistence, validation, payload builders, prefill mapper, page flow/J1/no-voice, resume) |
| `next build` | clean |

**Prod artifact for cleanup ledger:** ONE entity created in the prod demo org by the final
AT run — `u02p3atentitydeletable-category3c-e2f34720` ("U02-P3 AT Entity — deletable"),
no governance suite started (the AT unchecks the toggle, keyboard-Space). Same class as
the existing smoke artifacts; delete at leisure. Local iteration ran against a local
qanun-api checkout (uvicorn + qanun_demo.db, seeded demo user).

Screenshots: **7 step-states × 4 widths + prefill evidence → `u02_after_screens/p3/`**
(29 files). Before/after worst offender: `u02_audit_screens/ix_entities_new_initial_1440.png`
(J1: selected ADGM + "Select a jurisdiction above to begin" + "Listening to your answers…")
vs `u02_after_screens/p3/entities_new_step1_1440.png`.

### 6. SHAs / deployments

| What | Ref |
|---|---|
| Flow rebuild + voice removal + tests | `8753b80` |
| AT hardening (focus determinism, model id, label swap) + AT scripts | `ef12db7` |
| Merge | `main a042fcd` (--no-ff), pushed; **NOT promoted** — `www.qanun.io` unchanged, verified |
| Vercel | branch preview `https://qanun-czfh2g5ze-olivers-projects-9b1cb760.vercel.app` (Ready); main build `qanun-6jgm9b1iy-…` (production-target, awaits promote) |

### 7. Parks / carry-forwards

- **`/onboarding` jurisdiction picker** — separate surface (auth group), untouched; its copy rows were already KEEP in the copy inventory.
- **Backend niceties (read-only this lane):** GET `/api/entities/{id}` omits `target_jurisdiction` (AT works around via the list endpoint); `validation_summary` is a composed string carrying the raw licence code (display-mitigated client-side); no endpoint serves entity-type/activity vocabularies (client dictionary with honesty note, §4).
- **`/api/entity-setup/session` + tier-0 write-back** — unused by the new flow (localStorage draft). If server-side drafts are wanted later (cross-device resume), the endpoint exists.
- **jurisdiction-questions.ts / PreDraftQuestionnaire** — still used by the documents-preflight lane; untouched beyond voice removal + the dead model id fix.
- **Demo AT entities** — prod: `u02p3atentitydeletable-category3c-e2f34720` (deletable); local db also carries "U02-P3 Local Probe — deletable" probes.

---

## P4 — Document suite rebuild: the reader (CCD/U0.2-P4)

**Repo:** `qanun` only (branch `sprint/u02-p4-docs` → merged `main 34c591a`). Backend untouched — the data source is P4b's live `GET /api/documents/{job_id}/content` (qanun-api `7bcf671`, already deployed).
**No promotion:** `www.qanun.io` still serves the pre-U0.2 deployment (verified post-merge: "Zero hallucination" / 67,056 still live). Branch preview `https://qanun-gzjlrd2o1-olivers-projects-9b1cb760.vercel.app` (Ready); main production-target build `qanun-7gftk6eg2-…vercel.app` (Ready, awaits `vercel promote`).

### 1. "View" now shows the document

The audit's sharpest failure — View → a progress card with a download button, no
document — is closed at both ends:

- **Suite table `View →`** now routes to `/compliance/documents/{jobId}` (the reader),
  not the drafting-progress screen; the draft-complete screen's primary action is
  **"Read the document"** (bundle download demoted to secondary, still labelled).
- **The detail page IS the document.** `components/qanun/reader/DocumentReader.tsx`
  renders every drafted section with typographic care: a new `--text-reader` token
  (15/26) on a measured 68ch column — dashboard chrome stays 13/20; the drafted text
  reads like a legal document. Designed section headings ("Section 8 — CDD and EDD
  Procedures", from `sectionLabel`); in-content headings demoted below them; hairlines,
  markdown tables (parsed with per-cell offsets), numbered items, bold/italic emphasis
  (no literal asterisks), `---` rules.
- **Citations anchored in the text at their API character spans.** `lib/display/reader.ts`
  segments each section's raw content around `citations[].spans` and replaces the raw
  bracketed text (`[AML 8.1, VER11.210526, effective 21 May 2026]`) with an
  `A1CitationChip` carrying the LIVE Layer-1 verdict — `supported` / `flagged`
  (unverified_review) / `gap` (unresolved; the draft gate would strip) — mapping is
  downgrade-only, corpus defects noted in the tooltip. Version + effective date move
  into the chip tooltip (rule 10: named source + freshness inline); the drafter's
  inline `[support: …]` gate markers are stripped, never rendered.
- **Coverage callouts anchored to their sections, from the structured arrays** (never
  the stringified reprs): *"Section 8 does not cite `AML 8.6` — add it or regenerate
  the section. (4 of 5 required provisions cited.)"* Phantom fragments are counted,
  never shown: *"3 citation-shaped fragments in this section do not match any corpus
  provision and are not counted as citations."*
- **Provenance footer:** "Citations verified against `VER11.210526` at the time this
  page loaded · deterministic text check — semantic verification is not yet applied."
- **States:** loading = skeleton of the reader itself; designed 404 (not found), 403
  (another org's workspace), 409 (**not-yet-drafted** panel with live job status +
  "View drafting progress"), and a retryable generic error. Reader→certificate→back
  loop verified coherent (certificate back-link already targeted the document page).

### 2. The editing story — explicit and honest

Header actions (both above the fold at 1440, AT-asserted): **Edit in Word** (primary)
· **Download bundle** (secondary, captioned "Bundle: .docx + provenance manifest +
certificate" — verified against `bundle_docx_with_provenance`: ZIP = DOCX +
PROVENANCE.json + certificate PDF/HTML) · Certificate (ghost).

"Edit in Word" opens `EditInWordPanel` — no pretence of one-click integration:
1. Download the bundle, open the .docx in Word.
2. Add the QANUN add-in **by sideloading** (`https://qanun-addin.vercel.app/manifest.xml`,
   copyable + Open link; "Insert → Add-ins → Upload My Add-in, or ask your Office
   admin"), with the what-you-get line: clause drafting inserted as tracked changes
   with per-citation verification comments, and "Verify changes" re-checks edited
   text. The panel states plainly the add-in is in pilot, not in the Office Store.

**In-app section-level editing: OUT of scope, parked** — it needs backend mutation
endpoints that don't exist (no per-section PATCH; the add-in's `draft-clause` routes
serve Word, not the web reader).

### 3. Readiness honesty

- **Document level (display-layer, shipped):** `documentVerificationState()` derives
  the ONLY status class a drafted document may present, from the live
  `verification_summary` — never file existence. 0 verifiable citations →
  **"Drafted — verification incomplete"**; partial → same label + honest counts
  ("15 of 26 citations supported · 11 flagged for review"); only all-supported reads
  "Verified — all N citations supported". Unit-tested with a 0-citation fixture
  (AT-5 hard). **No true 0-citation doc exists in prod once live-verified** — but
  `/api/drafting/status` persists `unique_citations: 0` on **8 of 10** demo docs
  (exactly the audit's "Citations: 0 / COMPLETE" dishonesty); the reader ignores that
  stat and uses the live endpoint.
- **Suite level (display-layer, shipped):** the J2 16%-vs-100% contradiction was a
  client bug — server `complete_count` (10) divided by the client's template-catalogue
  size (64). Now server-truth (`total_documents`/`completion_pct` from
  `/api/submission/{id}/status`) and relabelled **"Drafting progress"** with the
  microcopy "Counts drafted files in the required set — open a document to see its
  citation verification." Suite status chips read **"Drafted"**, never "Complete"
  (asserted by test). `/compliance/documents` now agrees with `/compliance/gap-analysis`.
- **Server-side (documented, not touched):** `/compliance/governance`'s 33% (16/49)
  comes from a different server universe (`/api/governance/entities/{id}/profile`'s
  49-doc governance catalogue) than the 10-doc submission package; J3's
  COMPLETE-vs-Not-Started and J4's BVI-entity-on-ADGM-set are the same server data
  question. **Backend asks:** (a) per-document verification rollup on the submission
  status endpoint so suite figures can be verification-aware; (b) reconcile/name the
  governance-catalogue vs submission-package universes; (c) backfill the stale
  persisted `unique_citations`.

### 4. Suite/list keep-and-wire

Portability legend (P2 component) already wired on the suite page — kept; job UUIDs
already demoted via `CopyableDetail` — kept (reader header uses the same idiom);
table reflow (F1 column folding) — kept, scans clean. Shared status dictionary now
owns the export-phase codes (`exporting`, `export_failed`, `review_required`,
`skipped`, `created`) — the P2 park on local overrides is closed; `JobStatusChip`
falls back to `statusLabel()` for unknown codes.

### 5. AT-5 evidence

| Check | Result |
|---|---|
| `scripts/u02_p4_at.mjs` (built app, prod API, demo session) | **26/26 PASS** |
| Network honesty (CLAUDE.md rule) | page called `GET /api/documents/{job}/content` → 200 observed in-browser |
| Full text + live chips on the demo doc | s8 body text asserted; **86 citation chips** (`supported` + `flagged`) with real `data-a1-state`s |
| Real `gap` chips | `722c1de2…` (Board Governance Charter, 3 unresolved live) renders `data-a1-state="gap"` + "verification incomplete" header |
| Coverage callout | editorial register asserted ("does not cite … add it or regenerate") from structured arrays |
| Both edit paths above the fold @1440 | bounding boxes < 900px, no scroll; panel opens with manifest + sideload honesty |
| 0-citation ≠ COMPLETE | unit fixture (AT-5 hard) + page test; no real 0-citation doc survives live verification (see §3) |
| Leak scan (incl. reader + certificate routes) | **clean** (no repr, no `[support:]`, no full UUID, no PHANTOM jargon — also AT-asserted) |
| axe WCAG 2.0/2.1 A+AA | clean @1440: reader (demo + gap doc), edit-panel open, suite (one contrast fix: callout context line) |
| No-clip | clean at 950/1280/1440/1728 (AT script + shared `noclip_scan`) |
| vitest | **213 passed / 0 failed** (baseline 192 + 21: display-layer, reader blocks, verification honesty, page states, edit panel) |
| `next build` | clean |
| Reader→certificate→back | navigated and asserted |

Screenshots: **23 files → `u02_after_screens/p4/`** — reader at 4 scroll stops × 4
widths (the dashboard shell scrolls inside `<main>`, so reader evidence is viewport
captures at scroll stops; fullPage shots of 33k-px documents paint blank below the
fold), suite ×4, edit-panel + gap-doc evidence. Before/after worst offender:
`u02_audit_screens/compliance_documents_98937156-…_1440.png` (stat card + Python-repr
coverage notes, no document) vs `u02_after_screens/p4/doc_reader_top_1440.png` +
`doc_reader_callout_1440.png`.

### 6. SHAs / deployments

| What | Ref |
|---|---|
| Reader + display layer + honesty + tests | `7281551` |
| AT tooling + contrast/italic polish | `92d74df` |
| Merge | `main 34c591a` (--no-ff), pushed; **NOT promoted** — `www.qanun.io` unchanged, verified post-merge |
| Vercel | branch preview `https://qanun-gzjlrd2o1-olivers-projects-9b1cb760.vercel.app` (Ready); main production-target build `qanun-7gftk6eg2-…vercel.app` (Ready, **awaits promote**) |

### 7. Parks / carry-forwards

- **In-app section-level editing** — needs backend mutation endpoints (none exist); parked with the honest Word path shipped instead (§2).
- **Backend asks (§3):** verification rollup on submission status; governance-vs-submission universe reconciliation (J3/J4 remain server-side); stale `unique_citations` backfill; a real document-title field (H1 is still the best-effort de-slugged filename — "…Management Lt", E2's data truncation).
- **Corpus/drafter data quality now visible (honestly) in the reader:** phantom citation-shaped fragments (counted, never rendered) and early sections re-emitting the document front-matter as in-content headings — re-segmentation / drafter tickets, not display bugs.
- **Suite table lists the full template catalogue** while the stats describe the 10-doc required set (labelled); a "Required set / Additional templates" split is a future polish.
- **Add-in cohort distribution** — the panel tells the sideload truth; when the A6 cohort/Office-Store path lands, only `EditInWordPanel` copy changes.

---

## P5 — Register/remediation polish (CCD/U0.2-P5)

**Repo:** `qanun` only (branch `sprint/u02-p5-register` → merged `main af06bcf`). Backend read-only.
**No promotion:** `www.qanun.io` still serves the pre-U0.2 deployment (verified post-merge: "Zero hallucination" / 67,056 still live on the domain). Branch preview `https://qanun-q5pm7mi61-olivers-projects-9b1cb760.vercel.app` (Ready); main production-target build `qanun-3izr3ir2f-…vercel.app` (awaits `vercel promote`).
**The other half of P5** — the corpus data-bug filing — was pulled forward and closed earlier: `TICKET_CORPUS_DATA_QUALITY_U02_20260702.md` (six families, exact rows).

### 1. What P2 had already covered on these surfaces (verified, not redone)

The `/compliance/twin` register + remediation surface kept its U0 structure but P2's app-wide
conversion had already landed most of the §3 rules here:
- lane labels killed (`A2 · DIGITAL TWIN` → "Live register", `A3 · RULE-CHANGE → REDLINE` → "Rule-change redlines"); "A1-verified" empty-state wording → "a verified redline";
- licence-pack enum → `licencePackLabel` (`ADGM_FSRA_CAT3` → "FSRA Category 3 — investment management");
- marketing paragraph → dismissible first-run explainer (localStorage);
- designed empty (no entity) / loading skeleton / retryable error / 403 foreign-org states;
- `stripDotLeader` existed in `lib/display/documents.ts` and was already wired into `RegisterMatrix`;
- GAP headline stat (honest, dashed-degraded when >0), gaps-first flat ordering, A1 state grammar on status pills, `MonoRef` on rulebook/version chips, editorial `A1VerifiedBadge` derived from the real verdict, side-by-side/inline redline, accept-flow audit row.

### 2. What P5 did

**Interim dot-leader cleanup (ticket family 1), marked interim.** `stripDotLeader` is now
explicitly commented as INTERIM against `TICKET_CORPUS_DATA_QUALITY_U02_20260702` family 1
("remove once the obligation catalogue is regenerated"; the helper must not grow beyond
trailing furniture), regex extended to spaced leaders (". . . . 12"), and **unit-tested with
the audit's exact strings**: "Assessing the money laundering risks of a business
................................. 30" → clean, ditto AML 8.1 "…41"; guards prove titles
legitimately ending in numbers ("Chapter 4.5", "Reporting under Rule 30") are untouched.
Proven live: TradeDar's register (whose API payload still carries the dots — verified by
curl) renders both titles clean; the AT asserts no `[.…·]{4,}\s*\d+` anywhere on the page.

**Family 2 (wrong-heading titles) — NOT display-fixed.** Verified all five rows are in the
ticket (§2: COBS 3.4/COBS 6.1/GEN 6.1/GEN 3.3/GEN 5.3). The honest affordance test passed:
the mismatches were individually verified in the live audit (leak inventory §L.2), so a
subdued "· title under review" note (text-label, faint, tooltip explaining the pin is
unaffected) renders beside the as-is title for **exactly that audited FSRA set** —
`titleUnderReview()` is scoped to `source_entity === 'FSRA'`, marked INTERIM, and never
infers beyond the list. No title is guessed or rewritten.

**Register density/hierarchy.** Obligations now grouped by rulebook (`groupByRulebook`,
pure + unit-tested): group header = mono code + dictionary name + per-group counts (gap
count in gap colour when >0); groups ordered by gap count then code, rows within a group
gap → open → satisfied then section-ref numeric order — gaps lead at both levels, GAP
headline unchanged. The FSRA rulebook codes the catalogue actually carries (GEN/COBS/AML/
PRU/MIR/FSMR) were missing from the display dictionary (falling to humanised fallback) —
added, so headers and chip tooltips read "FSRA Conduct of Business Rulebook" etc.

**Provenance/freshness (teardown rule 10).** Register footer mirrors the P4 reader idiom:
"Register read live at the time this page loaded · obligations pinned against `VER11.210526`,
`VER23.290426`, `VER14.210526` — each row names its own pin." (distinct versions computed
client-side from the rows; capped at 4 + "and N more"; omitted when no version data).

**Remediation chrome → P4 reader patterns.** Section ref is now a corpus link (same
group-hover + ExternalLink idiom as register rows, mono preserved); a raised-date freshness
line ("Raised 21 June 2026", house format) joins the doc-type meta. The old→new version
trigger chips, side-by-side redline, honest A1 badge and the accept-flow audit row all kept
as U0.2 built them; status chips were already chip-sized and editorial.

### 3. AT evidence

| Check | Result |
|---|---|
| `scripts/u02_p5_at.mjs` (built app, prod API, demo session, TradeDar) | **8/8 PASS** |
| Dot-leader titles provably cleaned | unit (audit-exact strings) + live (API payload carries dots; page renders none) |
| Grouped chrome + provenance line + GAP headline | asserted live |
| Keyboard walk | corpus links focusable; remediation empty state designed; redline-toggle/accept-reject walk **skipped — no live remediations exist** (see parks) |
| axe WCAG 2.0/2.1 A+AA | clean at 950/1280/1440/1728 on `/compliance/twin` |
| Leak scan (full route set incl. twin, doc reader, certificate) | **clean** |
| No-clip (full route set × 950/1280/1440/1728) | **clean** |
| vitest | **230 passed / 0 failed** (baseline 213 + 17 P5: dot-leader exact strings, under-review scoping, grouping, matrix render incl. footer + affordance-count, remediation chrome, dictionary) |
| `next build` | clean |
| Screenshots | `u02_after_screens/p5/compliance_twin_{950,1280,1440,1728}.png` |

### 4. SHAs / deployments

| What | Ref |
|---|---|
| P5 polish + tests + AT script | `5d9a267` on `sprint/u02-p5-register` |
| Merge | `main af06bcf` (--no-ff), pushed; **NOT promoted** — `www.qanun.io` unchanged, verified post-merge |
| Vercel | branch preview `https://qanun-q5pm7mi61-olivers-projects-9b1cb760.vercel.app` (Ready); main build `qanun-3izr3ir2f-…` (production-target, awaits promote) |

### 5. Parks / carry-forwards

- **No live remediation data**: every demo entity has 0 remediations and 0 gaps, so the pending-card chrome (redline toggle, accept/reject) is proven by unit tests + the designed empty state live; the MAX-9 park stands — **backend demo-data seeding** (a pending remediation + a gap on the demo org) is what makes this surface demo-able. Backend read-only this lane.
- **Interim code to delete on catalogue regeneration**: `stripDotLeader`'s strip (family 1) and `titleUnderReview`/`FSRA_TITLES_UNDER_REVIEW` (family 2) — both commented with the ticket reference.
- **J5** (register corpus links land on a fuzzy 20-result search whose top hit can be the wrong jurisdiction) — a `/corpus` search-ranking issue, not a register issue; the link contract itself is correct and test-asserted.

---

## CLOSE — Integrated verification on final main (CCD/U0.2-CLOSE)

Final main `af06bcf` (all five phases), verified together against the prod API
(local production build, port 3000, demo session): `next build` clean · vitest
**230/230** · `copy_scan` clean (source + 11 public routes; `/design` 307) ·
`leak_scan` **clean over 21 authed routes** (pre-U0.2 baseline: 538) ·
`noclip_scan` **clean at 950/1280/1440/1728** (baseline: 15) · axe WCAG 2.0/2.1 A+AA
**clean on 32 routes @1440** (+ `/compliance/twin` at all four widths) ·
`u02_p4_at` **26/26** · `u02_p5_at` **8/8**. **No integration regressions.**
`www.qanun.io` re-verified still pre-U0.2. Full package incl. before/after
walkthrough, copy-inventory execution audit, per-surface bake-off verdicts, parks
(24) and prod-cleanup ledger: `U02_WOW_REVIEW_PACKAGE_20260702.md`. Close-out
screenshot evidence: `u02_after_screens/close/`. Harness notes: prod-API CORS admits
`localhost:3000` only; local `next start` needs `AUTH_TRUST_HOST=1` or the NextAuth
middleware fails **open** (fail-closed hardening ask parked).
