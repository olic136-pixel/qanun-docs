# B1 — Parser Hypothesis Verification (FSRA GEN VER13)

**Date:** 2026-05-12
**Source PDF:** `/Users/oliver/ADGM/adgm-corpus/raw/fsra/rulebooks/gen/ADGM1547_7584_VER13270426.pdf`
**Extraction:** `pdftotext -layout` → `/tmp/qanun-overnight/b1-pdf-inspection/gen_ver13.txt` (6,890 lines)
**Parser:** `adgm_corpus/processing/structure_parser.py::parse_rulebook` against `GEN`
**Branch:** sprint/B1-pdf-inspection (no commit — memo-only deliverable)

---

## TL;DR — Hypothesis REFUTED

The CCD hypothesis ("parser only promotes a rule number when lettered
sub-clauses (a)(b)(c) follow; captured rules have lettered children,
dropped rules don't") does not survive contact with the PDF.

The real situation is more pathological: **the parser captures zero
real GEN 3.5.X rules from this PDF.** The four "captured" sub-rules
(3.5.2, 3.5.4, 3.5.16, 3.5.18) are spurious matches against fragments
of body text that happened to wrap to a new line beginning with a
sub-rule-shaped numeric reference. The dropped rules
(3.5.1, 3.5.3, 3.5.5–3.5.15, 3.5.17) are not dropped — they were
never findable to begin with, because FSRA rulebook PDFs do not
include explicit "3.5.X" rule numbers as line prefixes.

This is a structural parser failure, not a regex tweak.

---

## Evidence

### The parser regex

`adgm_corpus/processing/structure_parser.py:26`:

```python
SUB_RULE_RE = re.compile(rf"^{_MODULE_PREFIX}(\d+\.\d+\.\d+)\s*(.*)$", re.MULTILINE)
```

This expects a line that **starts with** an optional module prefix and
then a three-segment dotted number (e.g. `3.5.1`). The parser then
treats that line's continuation as the rule title and the subsequent
indented `(1)(2)(3)` block as the rule body.

### What `SUB_RULE_RE` actually matches in the GEN VER13 text

Running the regex against the full extracted text yields **10 matches
across the entire 6,890-line PDF**:

| ref     | "title" line (first 60 chars)                                    |
|---------|------------------------------------------------------------------|
| 3.3.19  | `(1) An Authorised Person must ensure, as far as reasonabl…`     |
| 3.3.32  | `(1) An Authorised Person must inform the Regulator about…`      |
| 3.3.41  | `(1) An Authorised Person must have a Governing Body and s…`     |
| 3.3.41  | `A (1) This Rule applies to:`                                    |
| 3.4.6   | `The records referred to in Rule 3.4.5 must be maintained for…`  |
| 8.9.6   | `(1) The Regulator may:`                                          |
| 8.10.6  | `A Major acquisition or establishment of subsidiary`              |
| 8.10.12 | `(1) Each Authorised Person and Recognised Body must notif…`     |
| 8.10.13 | `In the case of an Insurer which is a Protected Cell Company`    |
| 8.10.14 | `(1) Subject to (2), an Authorised Person must provide to …`     |

**Zero** of these is a real GEN 3.5.X sub-rule. The four that the parser
"captures" for chapter 3.5 emerge from elsewhere — see below.

### What `parse_rulebook` produces for chapter 3.5

```
GEN 3.5      L1 | 'Cyber Risk Management'                          ← real chapter
GEN 3.5.2    L2 | '(1)(c) should include regular verification…'    ← spurious
GEN 3.5.2(a) L3 | ''
GEN 3.5.2(b) L3 | ''
GEN 3.5.2(c) L3 | ''
GEN 3.5.2(d) L3 | ''
GEN 3.5.2(i) L3 | ''
GEN 3.5.4    L2 | '(2).'                                            ← spurious
GEN 3.5.4(a) L3 | ''
GEN 3.5.4(b) L3 | ''
GEN 3.5.16   L2 | '(3) may be conducted in a variety of ways…'    ← spurious
GEN 3.5.16(a)…(f) L3 | ''
GEN 3.5.18   L2 | ', to ensure that it remains appropriate…'      ← spurious
```

Look at the titles: `'(1)(c) should include regular verification…'`,
`'(2).'`, `'(3) may be conducted…'`, `', to ensure that it remains…'`.
These are sentence fragments. They are reading material from **Guidance
paragraphs** that referenced Rule 3.5.2(1)(c), Rule 3.5.4(2), Rule
3.5.16(3), and Rule 3.5.18 — the references appear to start a wrapped
line because pdftotext rendering placed them at column 1 after a line
break.

### What the PDF actually looks like for chapter 3.5

```
3.5     Cyber Risk Management

        Cyber Risk Management Framework               ← title for 3.5.1 (no number)

         (1)   An Authorised Person must establish and maintain a Cyber Risk Management
               Framework to identify, assess and manage its Cyber Risks effectively.

         (2)   An Authorised Person must ensure the Cyber Risk Management Framework is in
               writing and is approved by its Governing Body.
         …
         (3)   The Cyber Risk Management Framework must:
               (a)   include systems and controls which are proportionate…
               (b)   have clearly defined roles and responsibilities…
         …

         Guidance
         1. An Authorised Person's Cyber Risk Management Framework should form part…
```

The rule number `3.5.1` appears **nowhere** in this block. The rule is
identified by its title (`Cyber Risk Management Framework`) and its
position in the chapter; the numbering `3.5.1` is implicit ("this is
the first titled block under chapter 3.5"). The same pattern applies to
3.5.2 (`Third-Party Cyber Risk`), 3.5.3 (`Governance`), 3.5.5
(`Protection of ICT Assets against Cyber Incidents`), and onwards.

The four "captured" rules are not captured. The parser found body-text
references whose wrap position made them look like sub-rule headings.

### Formatting comparison — captured vs dropped is not the right axis

| Rule    | Title present? | Lettered children? | Body shape           | Real outcome              |
|---------|----------------|--------------------|----------------------|----------------------------|
| 3.5     | yes (chapter)  | n/a                | top-level            | captured (real chapter)    |
| 3.5.1   | yes (`Cyber Risk Management Framework`) | yes (a)(b), (a)(b)(c)(d) | (1)…(7) + Guidance | **not captured, real**   |
| 3.5.2   | no             | yes (a)(b)(c)(d)   | (1)(a)(b)(c)(d) (2) + Guidance | spurious-captured from a Guidance reference |
| 3.5.3   | yes (`Governance`) | yes (a)(b)(c)(d)(e)(f) | (1) (2)(a)…(f)     | **not captured, real**   |
| 3.5.4   | no             | (varies)           | mostly (1)(2) numbered | spurious-captured from a Guidance reference |
| 3.5.5   | yes (`Protection of ICT Assets…`) | no | single paragraph    | **not captured, real**   |
| 3.5.6–15| no title       | sometimes lettered | (1)(2)(a)(b)         | **not captured, real**   |
| 3.5.16  | varies         | varies             | (1)(2)…              | spurious-captured from a Guidance reference |
| 3.5.17  | varies         | varies             | varies               | **not captured, real**   |
| 3.5.18  | varies         | varies             | varies               | spurious-captured from a Guidance reference |

The "captured vs dropped" split is not driven by formatting in the rule
body. It is driven by which Guidance-paragraph reference fragment
happens to appear at column 1 after pdftotext's line-wrap.

---

## Implication for the B1 register item

The B1 register entry currently reads:

> The structure parser drops selective rule numbers within rulebook
> chapters. Confirmed pattern for FSRA GEN 3.5: captures 3.5, 3.5.2,
> 3.5.4, 3.5.16, 3.5.18; drops 3.5.1, 3.5.3, 3.5.5–3.5.15, 3.5.17. […]
> Hypothesis from CCD: parser only promotes a rule number when lettered
> sub-clauses (a)(b)(c) follow.

Both observations need updating:

1. The "captured" sub-rules are **not real captures** — they are noise
   that happens to mimic the captured shape. So the corpus's 130 GEN
   sections for VER13 are dominated by the chapter-level captures
   (3.1–3.6, 4.1–4.8, etc., plus 8.x sub-rules that DO have legitimate
   line-prefixed numbering in their respective chapters), and the
   parser's reported "sub-rule" hits in chapter 3.5 are misleading.

2. The hypothesis is refuted. The real issue is the FSRA Rulebook
   chapter format itself: rules within a chapter are identified by
   title and position, not by an inline number. The current
   `SUB_RULE_RE` regex cannot find them.

### Right-sized fix

This is no longer a half-day regex tweak. A correct FSRA parser needs:

- **Title-based rule detection.** Treat any short bold-or-indented
  heading (rendered as a non-numbered, non-(1) line that is followed
  by `(1)`/`(2)` paragraphs) as the start of a new sub-rule. Track an
  intra-chapter counter to assign `X.Y.N` ref.
- **Untitled rule detection.** When `(1)` appears without an
  immediately-preceding heading, treat it as a continuation OR a new
  untitled rule (FSRA uses both patterns). The cue is usually a
  multi-line gap; pdftotext preserves enough whitespace for a simple
  blank-line heuristic.
- **Guidance suppression.** The `Guidance` block under each rule
  contains numbered sentences (`1. … 2. …`) and lettered alphabet
  lists. The current parser conflates these with rule structure. The
  parser must enter a "guidance" mode on seeing the `Guidance` line
  and exit on next title/chapter.
- **TR portal source-of-truth check.** The DFSA TR portal renders
  each rule with its full number as a heading (`3.5.1 Cyber Risk
  Management Framework`), so an HTML-side scrape (mirroring the DFSA
  approach) would sidestep the PDF parsing problem entirely. Worth
  evaluating whether FSRA TR also exposes per-rule HTML in addition
  to the PDF bundle.

### Size estimate

The B1 register entry sized this as "Multi-day (depends on hypothesis
verification)." With the hypothesis refuted, the parser fix is closer
to **multi-day to a week**:

- Title-based detection: 1–2 days (new regex set + state machine).
- Guidance suppression: 1 day (mode tracking).
- TR portal HTML evaluation: half a day to determine if scraping
  HTML instead of PDF gets us out of the parser problem entirely.
- Regression test suite: at least one full-chapter test per rule
  shape (titled, untitled, single-paragraph, table) — 1 day.

Surface as `B1-revised` in the next session and re-authorise based on
the new size estimate before any parser work begins.

---

## Files

- `/tmp/qanun-overnight/b1-pdf-inspection/gen_ver13.txt` — full
  extracted PDF body
- this memo: `/Users/oliver/qanun-docs/B1_parser_hypothesis_verification.md`

---

## Register

Maps to register item B1.
