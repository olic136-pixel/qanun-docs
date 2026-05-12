# DFSA Inventory — Authoritative Reconciliation

**Date:** 2026-05-12
**Author:** Overnight sprint Claude (Opus 4.7) per `Authorise overnight-sprint-2026-05-11`
**Source-of-truth pages:**
- DFSA TR master index: `https://dfsaen.thomsonreuters.com/rulebook/dubai-financial-services-authority-dfsa`
- Local code inventory: `MODULE_URLS` in `adgm_corpus/collection/scrapers/dfsa_rulebooks.py` @ branch `sprint/A1-scrapers-2026-05-11`
**Method:** HTTP HEAD on each MODULE_URLS entry; HTTP GET on master index; regex extraction of module-shaped slugs.

---

## Headline

- All 22 `MODULE_URLS` entries return HTTP 200 — no link rot today.
- Master index lists **21** module-shaped paths.
- **One MODULE_URLS entry is NOT linked from the master index**: PRU.
- Master index has **zero** module-shaped paths that are absent from
  `MODULE_URLS` — there is no "newly added module" we're missing.
- The four SOW-only codes (`AUT`, `COD`, `MIR`, `OSR`) are not on the
  master index; their alias / non-alias state is documented below.

---

## Code-by-code classification

Notation: **module** = primary regulatory rulebook, mid-to-large
section count expected. **sourcebook** = secondary guidance / forms /
process document; smaller section count. **aliased** = SOW name
resolved to inventory code via `SOW_CODE_ALIASES`. **deprecated** =
SOW name with no current inventory equivalent (content lives
elsewhere).

| Code | TR slug                                                              | Type        | Notes |
|------|----------------------------------------------------------------------|-------------|-------|
| AFN  | application-forms-and-notices-module-afn-ver5211-22                  | module      | Forms |
| AMI  | authorised-market-institutions-ami-ver3001-26                        | module      | |
| AML  | anti-money-laundering-counter-terrorist-financing-and-sanctions-module-aml-ver3004-26 | module | |
| AUD  | auditor-module-aud-ver1001-26                                        | module      | Alias target for SOW `AUT` |
| CIR  | collective-investment-rules-cir-ver4001-26                           | module      | |
| CMC  | code-market-conduct-cmc-ver411-22                                    | **sourcebook** | Today's A1 bulk rolled it back to legacy doc 2449 |
| COB  | conduct-business-module-cob-ver5001-26                               | module      | |
| FER  | fees-module-fer-ver3504-26                                           | module      | |
| FPR  | fund-protocol-rules-fpr-ver102-19                                    | **sourcebook** | Healthy at legacy 164 sections |
| GEN  | general-module-gen-ver7101-26                                        | module      | |
| GLO  | glossary-module-glo-ver6401-26                                       | module      | |
| IFR  | islamic-finance-rules-ifr-ver2212-25                                 | module      | |
| MKT  | markets-rules-mkt-ver2701-26                                         | module      | SOW only knew it as part of MIR/COD content |
| PIB  | prudential-investment-insurance-intermediation-and-banking-module-pib-ver5201-26 | module | |
| PIN  | prudential-insurance-business-module-pin-ver1804-23                  | module      | |
| PRS  | price-stabilisation-module-prs-ver704-18                             | **sourcebook** | Healthy at legacy 86 sections |
| PRU  | prudential-returns-module-pru-ver1012-25                             | **sourcebook**, **NOT ON MASTER INDEX** | Live URL works; A1 bulk got 0 sections |
| RAR  | recovery-and-resolution-rar-ver104-21                                | **sourcebook** | Healthy at legacy 187 sections |
| REC  | recognition-rec-ver1305-24                                           | module      | |
| REP  | representative-office-module-rep-ver1211-22                          | module      | |
| RPP  | regulatory-policy-and-process-sourcebook-rpp-april-2022-edition      | **sourcebook** | Slug uses `-edition` not `-verN-NN` |
| TKO  | takeover-rules-module-tko-ver0804-20                                 | module      | |

### Modules (16)
AFN, AMI, AML, AUD, CIR, COB, FER, GEN, GLO, IFR, MKT, PIB, PIN, REC, REP, TKO.

### Sourcebooks (6)
CMC, FPR, PRS, PRU, RAR, RPP. **B2 handler scope.**

### Aliased SOW codes (1)
AUT → AUD (already in `SOW_CODE_ALIASES`).

### Deprecated SOW codes — content lives elsewhere (3)
- COD ("Code of Conduct") → content folded into CMC (Code of Market Conduct sourcebook).
- MIR ("Markets and Investment Rules") → content folded into MKT + AMI.
- OSR ("Outsourcing Rules") → content folded into GEN §5–6.

These three are deliberately NOT aliased; the A1 orchestrator
surfaces them as "NOT IN INVENTORY" warnings, which is the correct
operator-visible signal.

---

## MODULE_URLS vs TR master index — drift findings

### Finding 1 — PRU not linked from master index

`PRU` resolves cleanly via direct URL
(`https://dfsaen.thomsonreuters.com/rulebook/prudential-returns-module-pru-ver1012-25`)
but the master DFSA index does not list it. Three hypotheses:

- (a) PRU is intentionally "hidden" by DFSA — it's a returns/reporting
  sourcebook and may be navigated to from a different parent
  (e.g., reporting forms, not the master rulebook list). This would
  explain why the URL stays live but isn't on the headline index.
- (b) PRU was recently removed from the master and is on its way to
  archive — DFSA may publish a replacement under a new code.
- (c) The page is intentionally listed only on the master under a
  different category (e.g., `/rulebook/reporting`) which the current
  regex didn't catch.

**Recommended action.** When B3 is actioned (currently this memo,
investigation only), add a `pruning_check` step that flags any
MODULE_URLS entry not present on the master after each `--apply`
run. Today PRU is the only such entry.

### Finding 2 — Zero new modules surfaced

Cross-checking the 21 module-shaped paths on the master index against
the 22 `MODULE_URLS` keys shows no new codes appearing on the master
that aren't already in our scraper inventory. The scraper inventory
is current. **No additions needed.**

### Finding 3 — RPP slug is unique

RPP's URL ends in `-april-2022-edition` rather than `-verN-NN`. The
current `_parse_slug_version` regex (DFSA scraper) expects the latter
shape and likely returns `version_str=""` for RPP. Today's A1 bulk
got "4 sections" out of RPP — consistent with the scraper not
parsing the sourcebook correctly. **B2 handler must handle the
`-edition`-style version suffix.**

### Finding 4 — All MODULE_URLS resolve

22/22 HTTP HEAD: 200 OK. No link rot. The C6 register item (DFSA
MODULE_URLS refresh script) remains a maintenance-friendly nice-to-have,
but there's no current breakage requiring it.

---

## Alias map (canonical as of 2026-05-12)

```python
SOW_CODE_ALIASES: dict[str, str] = {
    "AUT": "AUD",
}
```

- `AUT` (SOW name "Authorisation Module") → `AUD` (live "Auditor
  Module") since 11 May 2026 per `Authorise A1-apply-canaries`.

Three SOW codes intentionally NOT aliased (their content lives in
other modules / sourcebooks):

| SOW code | Original SOW name           | Current content location |
|----------|-----------------------------|--------------------------|
| COD      | Code of Conduct             | CMC (Code of Market Conduct sourcebook) |
| MIR      | Markets & Investment Rules  | MKT (Markets Rules) + AMI (Authorised Market Institutions) |
| OSR      | Outsourcing Rules           | GEN §5–6                 |

---

## Implication for B2 (sourcebook handler)

B3's findings define B2's input set:

- B2 must handle **six sourcebooks**: PRU, CMC, RPP, FPR, PRS, RAR.
- Of these:
  - **CMC, PRU, RPP** are the three that A1's module-shaped scraper
    failed against today (0 sections, 0 sections, 4 sections
    respectively) — primary B2 targets.
  - **FPR, PRS, RAR** are healthy at legacy section counts (164, 86,
    187 respectively). B2 must not regress these. Their current
    is_current=1 docs in corpus.db are the baseline.
- B2 must handle the **`-edition` URL slug variant** (RPP).
- B2 must produce non-trivial section counts (>50 for substantive
  sourcebooks).

These constraints fold into the B2 design memo (next deliverable).

---

## Suggested `DFSA_RULEBOOKS` update

Current `DFSA_RULEBOOKS` already enumerates all 22 codes correctly.
**No update needed.** RPP's slug variant and PRU's master-index
omission are handler / observability issues, not inventory issues.

Document the per-code classification in a comment next to
`DFSA_RULEBOOKS` (or a new `DFSA_RULEBOOKS_BY_TYPE` mapping) so the
next reader doesn't need to consult this memo:

```python
DFSA_MODULES = ("AFN", "AMI", "AML", "AUD", "CIR", "COB", "FER",
                "GEN", "GLO", "IFR", "MKT", "PIB", "PIN", "REC",
                "REP", "TKO")
DFSA_SOURCEBOOKS = ("CMC", "FPR", "PRS", "PRU", "RAR", "RPP")
DFSA_RULEBOOKS = DFSA_MODULES + DFSA_SOURCEBOOKS  # type: tuple[str, ...]
```

Surfaced as a B3-followup register item.

---

## Register

Maps to register item B3. Inputs the design phase of B2 (sourcebook
handler). The maintenance script under C6 (MODULE_URLS refresh) is
informed by this audit but not blocked on it.
