# C4 — WAL Checkpoint Crash Investigation

**Date:** 2026-05-12
**Author:** Overnight sprint Claude (Opus 4.7) per `Authorise overnight-sprint-2026-05-11`
**Status:** Investigation complete; simple try/except suppression fix landed on `sprint/C4-wal-checkpoint-2026-05-11-overnight`.

---

## Root cause

`scripts/reextract_citations_for_flipped_versions.py` ran:

```python
if not dry_run:
    conn.execute("PRAGMA wal_checkpoint(TRUNCATE)")
    conn.commit()
```

Two problems with this ordering:

1. **The checkpoint runs *inside* the open transaction**, before the
   `commit()`. The per-doc DELETE + INSERT loop above this block is
   wrapped in an implicit transaction; the checkpoint executes against
   a WAL that still contains uncommitted writes.

2. **`PRAGMA wal_checkpoint(TRUNCATE)` is the strictest checkpoint mode.**
   SQLite refuses to TRUNCATE the WAL when other connections are
   reading the DB *or* when uncommitted writes are pending in the
   current connection's WAL frames. The failure mode is
   `sqlite3.OperationalError: database is locked` on the PRAGMA call
   itself.

Today's A1 runs hit this because the live MCP server (or any other
process) was reading the same corpus.db file at the moment the script
attempted to TRUNCATE the WAL. The data was already inserted correctly;
the script crashed during the housekeeping step.

---

## Fix landed

The fix is two-fold and qualifies as "simple try/except suppression
with logging" per the C4 implementation gate:

```python
if not dry_run:
    # C4 fix (overnight 2026-05-11): commit FIRST, then attempt the
    # checkpoint. Pre-C4 order ran the checkpoint inside the open
    # transaction, which fails on SQLite builds where
    # PRAGMA wal_checkpoint(TRUNCATE) requires zero pending writes.
    # The data is now durable after commit() regardless of the
    # checkpoint outcome — the checkpoint is housekeeping that
    # truncates the -wal/-shm sidecars. Wrap in try/except so an
    # external reader blocking TRUNCATE doesn't fail the script.
    conn.commit()
    try:
        conn.execute("PRAGMA wal_checkpoint(TRUNCATE)")
    except sqlite3.OperationalError as e:
        logger.warning(
            "WAL checkpoint failed (data already committed; "
            "sidecar truncate skipped): {}",
            e,
        )
```

Two changes:

1. **Reorder:** `commit()` first, checkpoint after. The commit makes
   the per-doc DELETEs + INSERTs durable; the checkpoint becomes a
   pure housekeeping operation that can fail safely.
2. **Suppress:** `OperationalError` (the SQLite class for lock-conflict
   failures) is caught and logged as a `warning`. Other exception
   types (e.g., `sqlite3.DatabaseError` for corruption) intentionally
   propagate.

The regression test
`TestMain::test_apply_succeeds_when_wal_checkpoint_fails`
simulates a failing checkpoint by wrapping the connection in a proxy
that raises `OperationalError` on the PRAGMA call. Verifies:

- The script returns a successful stats dict.
- The citations row landed (data durability proven independent of the
  checkpoint outcome).

All 8 tests in `tests/test_reextract_citations_for_flipped_versions.py`
pass.

---

## Why this is the right fix (not a bigger one)

The C4 implementation gate said "simple try/except suppression OK; more
complex → memo only". This satisfies the gate:

- The fix is two lines of code plus one log call.
- The reorder is functionally equivalent in the happy path (checkpoint
  runs in both old and new orderings; the new ordering just doesn't
  hold an open transaction).
- The behavior change in the failure path is observable but minimal:
  pre-C4 the script raised `OperationalError` and exited non-zero;
  post-C4 the script logs a warning and exits 0. The committed data is
  identical in both cases.

### Not addressed (forward-looking)

- **Optimal checkpoint timing.** Continuous SQLite WAL operation
  reaches a point where the WAL grows large; the engine performs
  passive checkpoints automatically. Forcing a `TRUNCATE` is a
  deploy-time choice ("I want the -wal/-shm files clean before
  rsync"). Some refresh paths may not need the TRUNCATE at all; a
  `PASSIVE` mode would be a softer fallback. Not changed in this fix.
- **Per-connection isolation.** The script holds a single connection
  open for the whole run. Switching to per-doc transactions (commit
  after each doc) would be more SQL-correct but breaks the
  "atomically reextract all flipped" property today's script relies
  on. Not changed.
- **External reader detection.** A pre-check that warns if other
  connections are open before attempting TRUNCATE would be more
  helpful than the current log message. Forward-looking work.

These are forward-looking improvements, not fixes for C4's
acceptance bar.

---

## Files touched

- `scripts/reextract_citations_for_flipped_versions.py` — fix at line 217.
- `tests/test_reextract_citations_for_flipped_versions.py` — new test
  `TestMain::test_apply_succeeds_when_wal_checkpoint_fails`.

Branch: `sprint/C4-wal-checkpoint-2026-05-11-overnight`.

---

## Register

Maps to register item C4.
