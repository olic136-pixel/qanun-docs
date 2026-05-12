# B2 — DFSA Sourcebook Handler Design Memo

**Date:** 2026-05-12
**Author:** Overnight sprint Claude (Opus 4.7) per `Authorise overnight-sprint-2026-05-11`
**Status:** Design memo only — DO NOT IMPLEMENT this session per the B2 spec.
**Inputs:** B3 inventory (`dfsa_inventory_authoritative.md`), this memo's live-portal investigation.

---

## Scope

Bring the six DFSA sourcebooks (CMC, FPR, PRS, PRU, RAR, RPP) into
working refresh state through a single handler that complements the
A1.b `DFSARulebookScraper`. Each sourcebook must parse to a non-trivial
section count (>50 for substantive sourcebooks), respect the
single-current invariant, and survive idempotence runs.

Today's A1 bulk result (the regression):
- PRU: 0 sections
- CMC: 0 sections
- RPP: 4 sections (vs expected hundreds)

Surgical rollbacks restored DFSA-PRU doc 2431 and DFSA-CMC doc 2449
to is_current=1 with their legacy 73-section content. RPP stayed at
the partial 4-section state. The three untouched legacy sourcebooks
(FPR 164, PRS 86, RAR 187) are healthy at their current legacy
section counts but were never refreshed against the May 2026 portal.

---

## Live-portal investigation findings

Inspected each sourcebook's landing page + entiresection URL.

### Common structure

- Landing page: same Drupal 10 layout as modules; `<main>` wrapping the
  body; single `/entiresection/<N>` link as the canonical body URL.
- Entiresection page: same `<main>` container; long flat body with
  TOC at top and body paragraphs below.

### Per-sourcebook divergence

| Code | Body length | Numbering format                          | A1 parser outcome | Diagnosis |
|------|-------------|-------------------------------------------|-------------------|-----------|
| FPR  | ~155k       | `FPR X.Y.Z` (dots)                        | Untested in bulk; healthy at legacy | Compatible with current parser |
| PRS  | ~150k       | `PRS X.Y.Z` (dots, but rules sometimes duplicated `PRS 1.1.1 PRS 1.1.1`) | Untested in bulk; healthy at legacy | Compatible; duplicate-prefix needs dedup |
| RAR  | ~150k       | `RAR X.Y.Z` (dots)                        | Untested in bulk; healthy at legacy | Compatible with current parser |
| RPP  | ~385k       | `RPP X-Y-Z` (**hyphens**, not dots)       | 4 sections (parser missed) | Parser regex doesn't match hyphenated sub-rules |
| CMC  | ~85k        | `CMC <N>` chapters only, then numbered `1.` paragraphs (no rule-level X.Y) | 0 sections | Parser expects rule-level numbering; CMC doesn't have it |
| PRU  | **~850 bytes** at entiresection URL — essentially empty | unknown — landing page exists but body content is elsewhere | 0 sections | URL discovery: the `/entiresection/N` for PRU does not return body content |

### Sample evidence — RPP hyphenated numbering

```
Regulatory Policy and Process Sourcebook (RPP) April 2022 Edition
RPP 1 RPP 1 Introduction
RPP 1-1 RPP 1-1 Purpose
RPP 1-1-1 The purpose of the Regulatory Policy and Process …
```

Current `SUB_RULE_RE` is `^(?:PREFIX\s+)?(\d+\.\d+\.\d+)\s*(.*)$` —
matches dots only. RPP needs `(\d+(?:[.\-]\d+){1,2})`.

### Sample evidence — CMC chapter-only numbering

```
Code of Market Conduct (CMC) [VER4/11-22]
CMC 1 Introduction
CMC 2 Market Manipulation and Fraud
…
CMC 11 Enforcement Powers
```

Then within each chapter:
```
CMC 1 Introduction
Purpose
1. The purpose of the Code of Market Conduct is to provide Guidance …
2. The Code is intended to:
(a) help persons to determine whether or not conduct is Market Abuse;
(b) …
```

There are no `CMC X.Y` rules; only chapter-level `CMC <N>` plus
inline-numbered paragraphs. The parser must treat each chapter as the
section unit (level 0 → level 1 directly) and capture numbered
paragraphs as level-2 sub-rules with synthetic `(1)`, `(2)`, … refs.

### Sample evidence — PRU's empty entiresection

PRU's landing page links to `/entiresection/22662`. The returned page's
`<main>` contains only 847 chars of nav text — no rulebook body. The
actual PRU body must be reachable via a different URL pattern (perhaps
`/rulebook/prudential-returns-module-pru-ver1012-25/<chapter-slug>`
sub-pages, or a different per-chapter URL that the master page doesn't
expose).

**Open question for implementation.** Crawl PRU's landing page to
find the actual body URL: it likely embeds chapter-level links that
the regex didn't pick up. Worth a targeted re-fetch with a different
extraction (look for `<a>` tags inside specific TOC containers).

---

## Design choice — separate scraper vs per-code branch

### Option A: separate `DFSASourcebookScraper`

Pros:
- Clean class boundary; module logic untouched.
- Sourcebook-specific parsing strategies don't leak into the module path.
- Easy to test per-strategy.

Cons:
- Two scrapers to maintain; orchestrator needs to dispatch.
- Code duplication between module/sourcebook (Drupal fetch, content_hash
  computation, write_rulebook delegation).

### Option B: per-code dispatch inside `DFSARulebookScraper`

Pros:
- Single scraper class; dispatch is a per-code routing table.
- Shared fetch + hash + write paths.

Cons:
- Class becomes a multi-strategy switch.
- Test coverage harder (one class, many code paths).

### Recommendation: **Option C — strategy pattern**

A single `DFSARulebookScraper` orchestrating multiple `Parser` strategies:

```python
# Per-code parser selection
PARSER_STRATEGIES = {
    # Modules (standard X.Y.Z dotted numbering)
    "COB": ModuleParser(),
    "GEN": ModuleParser(),
    "AML": ModuleParser(),
    # … 13 more modules …
    # Sourcebooks
    "FPR": ModuleParser(),       # compatible
    "PRS": ModuleParser(),       # compatible (with dedup post-step)
    "RAR": ModuleParser(),       # compatible
    "RPP": HyphenatedRuleParser(),
    "CMC": ChapterParagraphParser(),
    "PRU": ChapterPageParser(),  # URL discovery is different too
}

def fetch_rulebook(self, code: str) -> dict | None:
    parser = PARSER_STRATEGIES.get(code)
    if parser is None:
        return None
    url = MODULE_URLS.get(code)
    if url is None:
        return None
    body = parser.fetch_body(url, client=self.client)
    if body is None:
        return None
    sections = parser.parse(body, code)
    full_text = parser.full_text(body)
    return self._doc_dict_from_html(code, url, body.url, body.html, sections=sections, full_text=full_text)
```

This keeps the existing module path unchanged (FPR/PRS/RAR opt into
`ModuleParser`) while RPP/CMC/PRU get their own classes. The single
`DFSARulebookScraper` continues to own fetch ergonomics, hash
computation, and write_rulebook delegation.

**Adopt Option C.** Falls back to Option B if the strategy class
infrastructure proves over-engineered; falls back to Option A if the
two strategies diverge dramatically in URL discovery.

---

## Per-strategy specifications

### `ModuleParser` (no-op refactor of current A1.b path)

Used by COB, GEN, AML, PIB, AMI, AUD, CIR, FER, GLO, IFR, MKT, PIN,
REC, REP, TKO + sourcebooks FPR, PRS, RAR.

Inputs: module landing URL.
Outputs: `(full_text, sections[])`.
URL discovery: find `/entiresection/<N>` link on landing page.
Body extraction: `_extract_main_text` (post-C7 robust).
Section parsing: existing `structure_parser.parse_rulebook` with
dotted X.Y.Z regex. PRS-specific dedup step removes lines where the
prefix is repeated (`PRS 1.1.1 PRS 1.1.1` → `PRS 1.1.1`).

### `HyphenatedRuleParser`

Used by RPP only.

Inputs / outputs: same as ModuleParser.
URL discovery: same.
Body extraction: same.
Section parsing: new regex `SUB_RULE_HYPHEN_RE = ^(?:PREFIX\s+)?(\d+(?:[.\-]\d+){1,2})\s+(.*)$` (matches both dotted and hyphenated forms; allows future modules to mix). Section_ref preserves the as-written form (`RPP 1-1-1`, not normalised to `1.1.1`) so cross-references resolve.

Acceptance bar: RPP refresh produces >100 sections, including
recognisable headings like `RPP 1`, `RPP 1-1`, `RPP 1-1-1`.

### `ChapterParagraphParser`

Used by CMC only.

Inputs / outputs: same.
URL discovery: same.
Body extraction: same.
Section parsing: NEW. Match chapter heading `CMC <N> <Title>` (regex
`^CMC\s+(\d+)\s+(.+)$`). For each chapter, scan body until the next
chapter heading. Within a chapter, recognise:
- Section subheadings ("Purpose", "Status", "Structure") → level 2
  with synthetic ref `CMC <N>.<subhead>`
- Numbered paragraphs `1.`, `2.`, … → level 2 with synthetic ref
  `CMC <N>(<num>)`
- Lettered sub-clauses `(a)`, `(b)` → level 3 with synthetic ref
  `CMC <N>(<num>)(<letter>)`

Acceptance bar: CMC refresh produces sections for all 11 chapters
plus their inline numbered paragraphs (target: >50 sections total).

### `ChapterPageParser`

Used by PRU only.

URL discovery: extend search beyond `/entiresection/`. Specifically:
- Fetch the landing page.
- Look for `<nav>` or TOC links inside the landing page body.
- Identify per-chapter URLs (likely `/rulebook/<slug>/<chapter-slug>`).
- Fetch each chapter URL; combine into a synthetic full_text.

Body extraction: same as ModuleParser per chapter.
Section parsing: existing dotted X.Y.Z regex, applied per chapter.

Open implementation question: confirm PRU's landing page actually
contains chapter URLs in a discoverable way. If not, fall back to
"fetch the PDF URL directly" (the landing page links to a PDF
download).

Acceptance bar: PRU refresh produces enough sections to match the
legacy 73-section state (or more if the May 2026 version expanded).

---

## Risk register

- **R1 — Strategy explosion**. If more sourcebooks emerge with novel
  numbering schemes, each gets its own strategy. Mitigation: keep
  strategies small; share via composition (e.g., `body extraction` is
  shared but `parser` differs).
- **R2 — Section_ref convention drift**. Cross-jurisdiction tools
  (B7 portability map) expect normalised section_refs. Hyphenated
  RPP refs (`RPP 1-1-1`) won't compare cleanly to dotted refs unless
  the portability layer normalises. Surfaces in A5.B.
- **R3 — PRU URL discovery may not work as designed**. The landing
  page may not have chapter-level URLs; PRU may need a PDF fallback
  path. Plan for this in implementation; budget ~half-day for the
  discovery work alone.
- **R4 — CMC synthetic refs are not in any existing system**. Any
  consumer that searches for `CMC 1(1)` won't find it because the
  syntax doesn't appear elsewhere. Mitigation: document the synthetic
  ref scheme in the scraper-authoring guide (C9) and add a test that
  recognises both `CMC 1(1)` and free-text "Section 1 of CMC 1".

---

## Implementation size estimate

- Strategy infrastructure refactor: 1 day
- ModuleParser refactor (no behaviour change): half-day
- HyphenatedRuleParser + RPP test: 1 day
- ChapterParagraphParser + CMC test: 1.5 days
- ChapterPageParser + PRU URL discovery: 1.5 days
- Integration testing (all 6 sourcebooks refresh idempotently): 1 day

**Total: 5–6 days.** The original B2 register entry sized "Multi-day"
which is consistent.

---

## Dependencies

- B3 (inventory reconciliation) — landed in this session.
- B1 parser fix — out of B2's scope; parser fix is for FSRA module-style
  rulebooks where the rule numbers aren't on the page (different
  problem from sourcebooks).
- A1 invariant (`MultiCurrentInvariantError`) — landed in this session.
  B2 strategies route through `write_rulebook`, so the invariant
  applies automatically.

---

## Out-of-scope tonight

This memo is design only. No code implemented. Authorise B2
implementation in a future session — suggested phrase
`Authorise B2-sourcebook-handler-implementation`.

---

## Register

Maps to register item B2.
