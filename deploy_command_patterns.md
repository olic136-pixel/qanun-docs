# Deploy command patterns — pipefail + tee canonical forms

**Status:** Authoritative — refer to this when authoring or reviewing any
deploy script, ad-hoc SSH command, or audit pipeline that ends in `| tee`.

**Origin:** C10 (2026-05-11). A1 bulk refresh on 11 May ran a one-line SSH
command of the form `ssh host 'python … | tee report.log'`. The Python
process crashed mid-run; `tee` returned 0; the surrounding shell believed
the deploy succeeded. The next operator only learned the truth from the
empty report file ten minutes later. Pipefail eliminates that gap.

---

## The hazard in one sentence

In bash, the exit status of a pipeline is the exit status of its **last**
command. `python <crashing-script> | tee /tmp/out` returns `tee`'s exit
code (always `0`), masking any upstream Python crash. `set -o pipefail`
changes the rule: the pipeline's exit status becomes the rightmost
**non-zero** exit status, so the upstream Python crash propagates.

---

## Canonical patterns

### 1. Bash scripts under `scripts/`

```bash
#!/usr/bin/env bash
set -euo pipefail   # ← REQUIRED for any script that pipes into tee

# … script body …
python scripts/long_running.py 2>&1 | tee -a "$LOGFILE"
```

`-e` aborts on any non-zero exit. `-u` errors on unset variables.
`-o pipefail` is the relevant flag for `| tee`. The combined
`set -euo pipefail` is the project standard.

### 2. SSH one-liners from the local shell

Wrap the remote command in `bash -c` and set pipefail explicitly inside
the remote shell — otherwise the remote `sh` runs without it.

```bash
ssh root@46.62.247.77 'bash -c "set -o pipefail; \
  cd /home/qanun/ADGM/adgm-corpus && \
  .venv/bin/python scripts/refresh_rulebooks.py --apply 2>&1 | tee /tmp/refresh.log"'
```

Or, simpler, write the script locally and scp it, then run via ssh:

```bash
scp scripts/refresh_rulebooks.sh root@46.62.247.77:/tmp/
ssh root@46.62.247.77 'bash /tmp/refresh_rulebooks.sh'
```

where `refresh_rulebooks.sh` starts with `set -euo pipefail`.

### 3. Ad-hoc local debug commands

Even one-off shell commands that you'll run once and discard need
pipefail if they pipe to tee:

```bash
bash -o pipefail -c 'python -m pytest tests/ -v 2>&1 | tee /tmp/pytest.log'
```

Or in zsh:

```bash
zsh -o pipefail -c 'python -m pytest tests/ -v 2>&1 | tee /tmp/pytest.log'
```

(Plain interactive zsh inherits whatever options are set in `~/.zshrc`;
do not rely on it.)

### 4. Inside heredocs (deploy ceremonies)

When the SSH body is a heredoc, the same rules apply — the remote shell
needs its own `set -o pipefail`:

```bash
ssh root@46.62.247.77 'bash -s' <<'REMOTE'
  set -euo pipefail
  cd /home/qanun/ADGM/adgm-corpus
  .venv/bin/python scripts/refresh_rulebooks.py --apply 2>&1 | tee /tmp/refresh.log
  test -s /tmp/refresh.log
REMOTE
```

Note `<<'REMOTE'` (single-quoted) — prevents the local shell from
interpolating `$LOGFILE` etc before send.

---

## Anti-patterns

These all silently swallow upstream crashes:

```bash
# WRONG — no pipefail, tee returns 0
ssh host "python script.py | tee /tmp/log"

# WRONG — pipefail only set locally, doesn't reach the remote shell
set -o pipefail
ssh host "python script.py | tee /tmp/log"

# WRONG — relies on $? but pipeline already returned tee's 0
python script.py | tee /tmp/log
[ $? -ne 0 ] && echo "failed"   # never fires
```

---

## Lint check

To audit the repo for unprotected pipe-mask patterns:

```bash
# Find every `| tee` line in a .sh file
grep -rn '| *tee' --include='*.sh' .

# For each hit, confirm a `set -o pipefail` (or `set -euo pipefail`)
# precedes the pipe in the same file.
```

A future CI test could automate this; see C10 follow-up below.

---

## Inventory (as of 2026-05-11 overnight)

Audited `scripts/` and `docs/` in `/Users/oliver/ADGM/adgm-corpus/`,
`/Users/oliver/ADGM/qanun-api/`, and `/Users/oliver/qanun/`:

- `adgm-corpus/scripts/resume_pinecone_embed.sh` — has `| tee -a` at lines
  73 + 85; protected by `set -euo pipefail` at line 29. **OK.**
- `adgm-corpus/scripts/monitor_and_finish.sh` — uses `>> $LOG` redirection
  only, no `| tee`. **Not applicable.**
- `adgm-corpus/CLAUDE.md` — SSH command templates do not pipe to tee.
  Each remote heredoc is followed by post-conditions (`ls -la`,
  `systemctl is-active`). Should still gain explicit `set -o pipefail`
  inside the remote heredoc when the pattern grows; flagged as a
  forward-looking note rather than a current bug.
- `adgm-corpus/docs/ADDING_A_JURISDICTION.md` — same pattern; no
  pipe+tee currently.
- `qanun-api/` — no `| tee` matches found in shell scripts or markdown.
- `qanun/` (frontend) — no `| tee` matches found.

**No untrapped pipe-mask patterns remain in the current repos.**

---

## Future register items

Surfaced during the C10 audit:

- **CI lint**: pre-commit hook (or CI step) that fails when a `.sh` file
  contains `| tee` without a prior `set -o pipefail` or `set -euo pipefail`
  in the same file. Filed for future authorisation; not implemented tonight
  to stay within the C10 acceptance scope ("documentation created, scripts
  updated, no untrapped pipe-mask patterns remain").
- **CLAUDE.md deploy template hardening**: the canonical deploy ceremony
  in `adgm-corpus/CLAUDE.md` (corpus.db swap + Python file scp + restart)
  doesn't pipe to tee today, but its constituent commands would benefit
  from `set -o pipefail` for symmetry as soon as anyone adds a `| tee`
  for logging. Forward-looking; document the pattern here so the next
  edit gets it right.
