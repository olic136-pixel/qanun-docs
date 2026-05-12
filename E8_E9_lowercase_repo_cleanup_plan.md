# E8 + E9 — Lowercase Repo Cleanup Plan

**Date:** 2026-05-12
**Author:** Overnight sprint Claude (Opus 4.7) per `Authorise overnight-sprint-2026-05-11`
**Mode:** Investigation only — DO NOT DELETE per HG6. Recovery plan per item below.

---

## E8 — `~/qanun-api/` lowercase clone

### State

- HEAD: `3e8b698` on branch `main`.
- Origin: `git@github.com:olic136-pixel/qanun-api.git`.
- Canonical clone (`~/ADGM/qanun-api/`) HEAD is `4998ae3` — 12 commits
  ahead of the lowercase clone's main.
- Lowercase clone main has zero commits NOT in origin/main.
- Modified working-tree files: just `.claude/gates/*.md` (overnight
  noise, per the clean-tree-definition memory).
- Untracked working-tree dirs: none of note.

### Worktrees (7)

| Path                                                        | Branch                   | HEAD     | Unique commits vs origin/main |
|-------------------------------------------------------------|--------------------------|----------|------------------------------|
| `.claude/worktrees/adgm-ra-scaffold`                        | claude/adgm-ra-scaffold  | 8c84501  | 0                            |
| `.claude/worktrees/k11-enrichment`                          | claude/k11-enrichment    | 5183206  | 0                            |
| `.claude/worktrees/k12-filter-fix`                          | claude/k12-filter-fix    | 4998ae3  | 0                            |
| `.claude/worktrees/k8-fix`                                  | claude/k8-fix            | 5420b7c  | 0                            |
| `.claude/worktrees/k9-synthesis`                            | claude/k9-synthesis      | 634abdb  | 0                            |
| `.claude/worktrees/recursing-meitner`                       | claude/recursing-meitner | aa853b2  | 0                            |
| `.claude/worktrees/tender-clarke`                           | claude/tender-clarke     | aa853b2  | 0                            |

**No worktree contains commits not already in origin/main.** All seven
claude/* branches have been merged or absorbed into the canonical
history.

### Recovery plan for E8

**No recovery work needed.** The lowercase clone is a stale read-only
copy with no unique commits in main and no unique commits in any of
its seven worktrees. It is safe to delete in a future authorised
session.

Suggested authorisation phrase: `Authorise E8-delete-lowercase-qanun-api`.

Recommended pre-delete safety check (idempotent):

```bash
cd /Users/oliver/qanun-api
for wt in $(git worktree list --porcelain | grep ^worktree | awk '{print $2}'); do
  cd "$wt"
  branch=$(git rev-parse --abbrev-ref HEAD)
  ahead=$(git log origin/main..HEAD --oneline 2>/dev/null | wc -l)
  echo "$wt ($branch): $ahead ahead"
done
# All zeros → delete is safe.
cd ~ && rm -rf /Users/oliver/qanun-api
```

---

## E9 — `~/adgm-corpus/` lowercase clone

### State

- HEAD: `17460e9` on branch `master` (matches local `origin/master`
  — both stale; canonical local is on `f3347b0`).
- Origin: `git@github.com:olic136-pixel/adgm-corpus.git`.
- The lowercase clone has NOT fetched from origin in some time
  — its local `origin/master` ref is at the same `17460e9` and is
  far behind the actual remote.
- Working-tree modifications: **10 modified files** + 1 untracked dir
  (`infrastructure/`).

### Modified files

| File                                                | Diff scope                                          | Likely classification |
|-----------------------------------------------------|-----------------------------------------------------|-----------------------|
| `.DS_Store`                                         | macOS metadata                                      | noise — ignore        |
| `adgm_corpus.egg-info/SOURCES.txt`                  | build artefact                                      | noise — ignore        |
| `adgm_corpus/collection/scheduler.py`               | small (~lines around 61)                            | needs inspection      |
| `config/schedule.yaml`                              | small (+2 lines around 7)                           | needs inspection      |
| `embedding_cache.db`                                | binary build artefact                               | noise — ignore        |
| `intelligence_pkg/mcp_server.py`                    | medium (+6 lines around 12)                         | needs inspection      |
| `intelligence_pkg/pipeline.py`                      | medium (+3 lines around 37)                         | needs inspection      |
| **`lexis/ingestion/pinecone_client.py`**            | **LARGE — 134 lines (canonical) vs 300 lines (lowercase); +166 lines of Cloudflare Worker proxy mode** | **HIGH-PRIORITY recovery** |
| `lexis/mcp/lexis_server.py`                         | small (+1 line around 2)                            | needs inspection      |
| `scripts/process_all.py`                            | small (~lines 1-9)                                  | needs inspection      |

### Untracked content

`infrastructure/cloudflare-worker/`:
- `worker.js` (3,965 bytes)
- `wrangler.toml` (315 bytes)
- `.wrangler/` (build state — likely safe to ignore)

The cloudflare-worker matches the proxy-mode addition in
`lexis/ingestion/pinecone_client.py`: the worker is the *server side*
of the proxy that the client invokes when `PROXY_BASE_URL` /
`PROXY_SECRET` are set, used to bypass GCP IP blocking on
Pinecone's data plane.

### Recovery plan for E9

**Block 1 — Cloudflare Worker + pinecone_client proxy mode (HIGH PRIORITY)**

The lowercase clone contains a working IP-block bypass for Pinecone
that is **not** in the canonical clone:

```python
# lowercase pinecone_client.py top of docstring
"""Pinecone wrapper for corpus storage and retrieval.

Supports two modes:
  1. Direct SDK (default): Uses the official Pinecone Python SDK.
     Works when the server IP is not blocked by GCP.
  2. Proxy mode: When proxy_base_url is set, routes all data-plane
     calls (query, upsert, delete, stats) through a Cloudflare Worker
     reverse proxy using httpx. This bypasses GCP IP blocking.

The proxy_base_url and proxy_secret are read from environment variables
PROXY_BASE_URL and PROXY_SECRET if not passed explicitly.
"""
```

Plus:
- A `_ProxyMatch` dataclass mimicking Pinecone's `ScoredVector` for
  duck-typing.
- Methods that branch on `proxy_base_url` and either call the SDK or
  POST to the worker.
- `infrastructure/cloudflare-worker/worker.js` — the worker code itself.

**Recovery action:** before deletion, copy these to a preservation
branch in the canonical repo:

```bash
cd /Users/oliver/ADGM/adgm-corpus
git checkout -b chore/preserve-cloudflare-proxy
cp /Users/oliver/adgm-corpus/lexis/ingestion/pinecone_client.py \
   /tmp/lowercase-pinecone-client.py
cp -r /Users/oliver/adgm-corpus/infrastructure ./infrastructure
git add infrastructure/
git commit -m "chore: preserve cloudflare-worker + pinecone proxy mode from lowercase clone (E9 recovery)"
git push --set-upstream origin chore/preserve-cloudflare-proxy
```

Then decide in a separate session whether to MERGE the proxy mode
back into the canonical `pinecone_client.py` or leave it as a
preservation branch.

**Block 2 — Smaller modified files (LOWER PRIORITY)**

The remaining six small-diff files (`scheduler.py`, `schedule.yaml`,
`mcp_server.py` × 2, `pipeline.py`, `lexis_server.py`,
`process_all.py`) need pairwise inspection before deletion. Each
diff is small enough that the canonical version is almost certainly
the right one, but the lowercase versions may contain comments,
defaults, or test hooks that weren't carried forward.

**Recovery action:** dump each pair to a side-by-side diff for the
operator to eyeball:

```bash
cd ~
mkdir -p /tmp/qanun-overnight/e9-diffs
for f in adgm_corpus/collection/scheduler.py config/schedule.yaml \
         intelligence_pkg/mcp_server.py intelligence_pkg/pipeline.py \
         lexis/mcp/lexis_server.py scripts/process_all.py; do
  out=/tmp/qanun-overnight/e9-diffs/$(echo "$f" | tr '/' '_').diff
  diff -u /Users/oliver/ADGM/adgm-corpus/$f \
          /Users/oliver/adgm-corpus/$f > "$out" 2>/dev/null
done
ls -la /tmp/qanun-overnight/e9-diffs/
```

Eyeball each diff; if nothing of value, proceed to delete the
lowercase clone.

**Block 3 — Build / noise files (NO RECOVERY)**

`.DS_Store`, `embedding_cache.db`, `adgm_corpus.egg-info/SOURCES.txt`
are all build / OS artefacts. No recovery needed.

### Pre-delete safety check

```bash
# Confirm no live tooling points at /Users/oliver/adgm-corpus
grep -r "/Users/oliver/adgm-corpus" \
  /Users/oliver/Library/Application\ Support/Claude/ \
  /Users/oliver/ADGM/ 2>/dev/null | grep -v ".venv\|node_modules\|.next"
# Empty result → no live config pins this path.

# Backup the entire lowercase clone before delete (one-shot safety).
tar czf /tmp/qanun-overnight/lowercase-adgm-corpus-pre-delete.tar.gz \
  -C /Users/oliver adgm-corpus
ls -lah /tmp/qanun-overnight/lowercase-adgm-corpus-pre-delete.tar.gz

# Now delete.
rm -rf /Users/oliver/adgm-corpus
```

The tar is the catch-all for anything overlooked.

### Suggested authorisation phrase

`Authorise E9-delete-lowercase-adgm-corpus-after-recovery`

The phrase is intentionally long — the operator should mentally
confirm that Block 1's recovery has happened before invoking.

---

## Cross-cutting findings

1. **The lowercase clones are not "redundant" — they preserve
   abandoned-or-forgotten work.** The cloudflare-worker is the clearest
   example. Don't treat lowercase-clone cleanup as a single "rm -rf";
   each clone needs an audit of its unique content first.
2. **The audit method that surfaced the cloudflare-worker was line-
   count and date comparison on modified files.** A faster heuristic
   when scanning future "stale" clones: any file > 5x the canonical's
   line count is a candidate for unique content extraction.
3. **The CLAUDE.md Phase-1-reconcile note** ("Do not point new tooling
   at /Users/oliver/adgm-corpus/") already says this clone is
   "scheduled for retirement in Phase 3". E9's recovery work is the
   prerequisite for that retirement. Not actioned tonight.

---

## Register

Maps to register items E8 and E9.
