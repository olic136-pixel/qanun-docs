# Hetzner Deploy Plan (Sprint 10 Reference)

**Block M — Sprint 6 prep overnight (15-16 May 2026)**

Local `adgm-corpus`, `qanun-api`, and `qanun` (frontend) have all drifted
substantially ahead of Hetzner production across Sessions 3 → Sprint 5.
Sprint 10 executes the deploy; this memo is the concrete plan so that
session starts from a checklist, not a blank page.

## Drift Summary (local ahead of Hetzner, as of 16 May 2026)

**adgm-corpus** — local master `491ff1d`, corpus.db `c061d461…4c4c`:
- Session 3: B1.GEN-ROLLOUT (parser_v2 GEN — corpus.db + ChromaDB + Pinecone)
- Session 4a: parser_v2 dedupe, F1 DFSA prefix-strip, F2 VARA URL, F3 PDF title hygiene
- Session 4b: parser_v2 PRU/COBS/MIR rollout, B4 FSRA refresh, A3 K7 retag, case law schema (H20-H22), VARA raw scrape, partial El Salvador enrichment
- Sprint 3 closure: VARA/SV/DFSA/BVI section parsing + dual-vector-store embedding, ObsidianAgent.run() (21,540 vault notes), BVI case law (20 decisions), MKT supersede
- Sprint 3 Cleanup: FTS5 `_sanitise_fts_query` rewrite, parser refinements
- Sprint 6 prep (this session): DFSA case law (9 decisions), VARA+SV citations (0→3315), DFSA CMC parser (44 sections)

**qanun-api** — local main `e68e1fe`:
- Sprint 4: I1-I9 governance suite backend (DocumentSuite, AppendixSpec, context propagation, suite orchestration, suite API endpoints, jurisdiction endpoint)
- Sprint 5: I16 suite coverage validator, I17 per-jurisdiction conftest fixtures
- Schema: `draft_suite_jobs` table + `draft_jobs.suite_id` column (migration `add_suite_jobs_20260329.py`)

**qanun (frontend)** — local main `d87b11d`:
- Sprint 5: I15 lib/api/suite.ts, I13 per-jurisdiction questionnaires, governance-suite page test coverage
- (Vercel auto-deploys from git push — no manual deploy step)

## Pre-Deploy Backup (production-side, MANDATORY)

```
ssh root@46.62.247.77 '
  mkdir -p /home/qanun/backups
  cp /home/qanun/ADGM/adgm-corpus/corpus.db /home/qanun/backups/corpus.db.pre-deploy-$(date +%Y%m%d_%H%M)
  cp /home/qanun/ADGM/qanun-api/qanun_demo.db /home/qanun/backups/qanun_demo.db.pre-deploy-$(date +%Y%m%d_%H%M)
  ls -la /home/qanun/backups/ | tail -4
'
```

## Deploy Order

### 1. adgm-corpus

**Python files** — scp in a single batch (per CLAUDE.md "corpus deploy includes Python code changes" rule). Touched across the drift window:
- `adgm_corpus/mcp/server.py` (G14 namespace routing, Sprint 3 closure E2)
- `adgm_corpus/processing/citation_extractor.py` (Blocks E1 + J — inline patterns + per-jurisdiction dispatcher)
- `adgm_corpus/processing/parser_v2/` (entire package — state_machine.py, format_profiles.py)
- `adgm_corpus/processing/vara_parser.py` (Sprint 3 closure + Sprint 3 Cleanup L2 split)
- `adgm_corpus/processing/structure_parser.py` (if touched)
- `adgm_corpus/storage/db.py` (FTS5 `_sanitise_fts_query` rewrite — Sprint 3 Cleanup D1)
- `adgm_corpus/agents/obsidian_agent.py` (run() implementation)
- `adgm_corpus/case_law/` (verifier.py + __init__.py — H21)
- `scripts/process_all.py` (USE_V2_PARSER flag map)
- run `git diff <hetzner-HEAD>..HEAD -- adgm_corpus/ scripts/ --name-only` to get the exact list

**corpus.db** — 270MB+; use `rsync --partial --progress` not plain scp (resumable). Per CLAUDE.md canonical deploy procedure:
```
sqlite3 corpus.db "PRAGMA wal_checkpoint(TRUNCATE);"   # commit must precede this
rsync --partial --progress corpus.db root@46.62.247.77:/tmp/corpus.db.staging
ssh root@46.62.247.77 '
  mv /tmp/corpus.db.staging /home/qanun/ADGM/adgm-corpus/corpus.db &&
  chown qanun:qanun /home/qanun/ADGM/adgm-corpus/corpus.db &&
  chmod 644 /home/qanun/ADGM/adgm-corpus/corpus.db &&
  ls -la /home/qanun/ADGM/adgm-corpus/corpus.db
'
```
**The chown/chmod is non-negotiable** — scp/mv as root preserves the local 600 perms; the `qanun` service user then can't read it and MCP `_search_corpus` silently degrades to FTS5-only. Verify `qanun:qanun 644` before restart.

### 2. qanun-api

**Python files** — scp `routers/` + `services/` (Sprint 4 governance suite endpoints + validators):
- `routers/drafting.py`, `routers/corpus.py`
- `services/drafting_templates.py`, `services/drafting_service.py`, `services/coverage_validator.py`
- `git diff <hetzner-HEAD>..HEAD --name-only` for the exact list

**qanun_demo.db** — **DO NOT overwrite production qanun_demo.db.** It carries live application data (entities, draft jobs, users). Instead, apply the `draft_suite_jobs` schema migration remotely:
```
scp migrations/add_suite_jobs_20260329.py root@46.62.247.77:/tmp/
ssh root@46.62.247.77 'cd /home/qanun/ADGM/qanun-api && .venv/bin/python /tmp/add_suite_jobs_20260329.py qanun_demo.db'
```
The migration is idempotent (CREATE TABLE IF NOT EXISTS + duplicate-column guard) — safe if already applied.

### 3. qanun (frontend)

No-op. Vercel auto-deploys from `git push origin main`. Verify the
deployment completed: `curl -s -o /dev/null -w '%{http_code}' https://qanun.io`
(expect 200 or 307 auth-redirect).

### 4. Service restart + verification

```
ssh root@46.62.247.77 '
  systemctl restart qanun-api &&
  sleep 10 &&
  systemctl is-active qanun-api &&
  journalctl -u qanun-api --since "30 seconds ago" --no-pager | tail -20
'
```
Per CLAUDE.md: ignore the pre-existing `git error: ... 00-Inbox/` noise and
the cancel-scope RuntimeError that accompanies the prior process shutdown.
Anything else is a real new error — investigate before declaring success.

**Wait for the init_db FTS5 reindex** — per memory `feedback_init_db_async_completion`,
adgm-corpus init_db's FTS5 reindex takes ~30s on the live corpus. Wait for
the journal "Database initialised at" line, NOT just `systemctl is-active`.

### 5. Live verification via MCP tools

- `search_corpus` against new content (VARA/SV/DFSA/BVI section refs — e.g. `VARA-COMP I.A.1`, `SV-DASP Art.37`, CMC chapters)
- `get_rule` resolves new section_refs
- `corpus_status` returns updated counts (sections, citations, case law)
- Frontend `/compliance/governance-suite` 6-step flow end-to-end against a demo entity

## Vector Stores

- **ChromaDB** at `/home/qanun/ADGM/adgm-corpus/chroma` — a directory of
  SQLite-style files; deploy by `rsync -a chroma/ root@…:/home/qanun/ADGM/adgm-corpus/chroma/`.
  Verify `adgm_docs` collection count post-deploy (~73,500+).
- **Pinecone** — cloud-hosted; no deploy step. Verify per-namespace counts
  match expected post-deploy: `adgm`, `vara`, `dfsa`, `bvi_fsc`,
  `el_salvador`, `panama_smv`, `default`. Pinecone is already in sync (the
  overnight sessions upserted directly to the live index).

## Rollback Path

If service fails post-restart:
1. `cp /home/qanun/backups/corpus.db.pre-deploy-* /home/qanun/ADGM/adgm-corpus/corpus.db`
2. `cp /home/qanun/backups/qanun_demo.db.pre-deploy-* /home/qanun/ADGM/qanun-api/qanun_demo.db` (only if it was touched — it shouldn't be)
3. `cd /home/qanun/ADGM/adgm-corpus && git checkout <PREVIOUS_HEAD>` (same for qanun-api)
4. `systemctl restart qanun-api`
5. Verify health endpoint

## Cron / Systemd Timers — verify all active post-deploy

- `qanun-regulatory-monitor.timer`
- `qanun-review-cycle.timer`
- `qanun-corpus-announcements.timer`
- `qanun-corpus-version-check.timer`
- `qanun-backup.timer`
- `qanun-calendar-alerts.timer`

`ssh root@46.62.247.77 'systemctl list-timers | grep qanun'`

## Estimated Wall-Clock

- corpus.db rsync (270MB): ~10-20 min (the bottleneck)
- chroma/ rsync: ~5-10 min
- Python file scp: ~2 min
- Verification: ~10-15 min
- **Total: ~30-50 min** if no surprises

## Risk Considerations

- Service downtime during restart: ~30-60s (including FTS5 reindex)
- In-flight production request failures during the restart window
- Pinecone is already live-synced — but verify per-namespace counts; a
  partial upsert from an overnight session would show as a count mismatch
- The `qanun:qanun 644` perms step is the single most common deploy
  failure mode (documented under CLAUDE.md K8 deploy 2026-05-10) — do not
  skip it
- Multiple sessions' worth of drift means a larger-than-usual diff;
  budget extra verification time
