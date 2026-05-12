# Phase 2 Backlog

Items surfaced during the post-overnight integration session and other
sources that are NOT actioned immediately but should land in a future
session.

---

## Process items

### Integration prompt drafting checklist — verify symbol locations

**Source:** A1 master integration merge, 2026-05-12.

Verify symbol locations before specifying import paths in smoke checks.
The A1 master integration prompt assumed
`MultiCurrentInvariantError` would live in `adgm_corpus.storage.db`
(conceptually a storage invariant); the actual location is
`adgm_corpus.collection.scrapers.adgm_rulebooks` (next to
`write_rulebook`). Future integration prompts should grep for the
symbol on the source branch before specifying its import path, rather
than guessing based on conceptual placement.

Suggested checklist for the next integration prompt:

```
# Before specifying any "from X import Y" smoke check:
git checkout <sprint-branch>
grep -rn "class Y\b\|^def Y\|^Y =" <package>/ | head
# Use the discovered path in the prompt.
```
