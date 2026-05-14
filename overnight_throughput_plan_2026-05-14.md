# Overnight Throughput Plan — Orchestrator-Driven Sessions

**Date:** 14 May 2026
**Owner:** Oliver Cook KC (CLO)
**Status:** Implemented — Orchestrator V1 built same day (register O1, `~/qanun-orchestrator/` `188a6a9`)

> This memo captures the design reviewed in-chat with Oliver on 14 May 2026 and
> implemented the same session as Orchestrator V1. It was originally drafted
> against a 16 May date stamp in the build brief; the system clock read 14 May,
> so all artifact dates follow the system clock (see Memory: brief-date-vs-system-clock).

---

## Problem

Three consecutive overnight CCD sessions — Sprint 4, Sprint 5, Option C — each
surfaced two recurring facts:

1. **Majority-pre-built code is the default, not the exception** (Memory #23/#28).
   Briefs are written as forward-looking specs; prior development sessions have
   already implemented substantial chunks. The work collapses from "build" to
   "verify+extend", which is much faster than the brief assumes.
2. **Per-session model-active throughput is empirically bounded** (Memory #20):
   ~13-52 min model-active regardless of how large the brief is. A single "big
   overnight brief" does not consume the available wall-clock window — it
   finishes in well under an hour and the remaining 5-7 hours sit idle.

Combined effect: the overnight wall-clock window is running at roughly **10-15%
utilisation**. The "one big brief" model cannot fill the window because a single
CCD session self-terminates long before the window closes.

## Solution

An **orchestrator** that runs N independent bounded CCD sessions sequentially via
`claude --print` headless mode. Each session is a self-contained bounded brief;
the orchestrator chains them. V1 single-threaded gives ~6-8× current utilisation
(6-8 sessions across the window) with no parallelism complexity. V2 adds
parallelism + per-resource locking for a further multiple.

## Architecture (V1)

1. **Repo:** new `~/qanun-orchestrator/`, independent of adgm-corpus / qanun-api /
   qanun / qanun-docs. Lives in `~` alongside them.
2. **V1 = sequential.** One session at a time. Sufficient to fill 6-8 hours if the
   queue holds 6-8 sessions. No file locking needed (no concurrent writes).
3. **Subprocess primitive:** `claude --print` with the prompt piped from stdin.
   Output captured to `logs/{session_id}/output.txt` + `result.json` (timestamps,
   exit code, halt flag).
4. **Halt detection:** the session prompt instructs CCD to write `HALT.md` in its
   working directory on halt; the orchestrator checks for that file after the
   subprocess exits. Also halts on non-zero exit and on 90-min wall-clock timeout.
5. **Queue format:** `.md` files with YAML frontmatter (`session_id`, `depends_on`,
   `estimated_duration_mins`, `halt_strategy`). Body is the CCD prompt.
6. **Failure routing:** non-zero exit / `HALT.md` present / timeout → `queue/halted/`;
   otherwise → `queue/completed/`.
7. **Morning surface:** `aggregate_morning_log.py` produces `MORNING-SURFACE.md`
   from `completed/` + `halted/`, halted sessions surfaced first for review priority.

## V1 Scope Boundary

**In V1:** sequential execution, file-based queue, YAML frontmatter prompts, HALT
detection (file marker + exit code + timeout), morning aggregator.

**Deferred to V2:** parallel session execution; per-resource locking
(`corpus.db.lock`, `chroma.lock`, `pinecone.lock`); `depends_on` dependency-graph
resolution (V1 accepts the frontmatter field but ignores it — runs alphabetical by
`session_id`); systemd timer auto-start.

## Operating Model

- Oliver populates `queue/pending/` with bounded session briefs during the day.
- The orchestrator runs overnight, draining the queue sequentially.
- Oliver reviews `MORNING-SURFACE.md` the next morning — halted sessions first.

## Prerequisites (verified 14 May 2026)

- `claude --print` validated on macOS — `echo "..." | claude --print` returns clean
  markdown, exit 0.
- Option C activation pipeline live — validates the "build → smoke → close fast"
  bounded-session shape.
- Sprint 6 prep memos in place — rich inputs for future agent-run sessions.

## Status

Orchestrator V1 built 14 May 2026 — register item **O1 → Done**. End-to-end smoke
passed (2 sessions, both clean). First real overnight queue to be populated by
Oliver for the next available night.
