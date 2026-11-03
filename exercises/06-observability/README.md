# 06 See it (observability)

Time: 30 minutes

A factory you cannot see is a factory you cannot trust. Trace the run.

## Goal

Feel the difference observability makes. Run the factory with no record, then with one, and
compare what is left behind.

## Before you start

You need a working `/planner`, `/refine` and `/implement` in `sandbox/.claude/skills/`, your own
from 03 to 05. If yours are not ready, your trainer has a working set to copy in.

## First, without the hook

Run a station and watch the run scroll away. From `sandbox/`:

- run something, for example `/refine sandbox-vzwt` or `/implement` on a refined Bean
- when it finishes, ask: what durable record of that run exists? The Bean holds the plan and the
  log. Everything else, which tools ran, what it tried, whether tests passed along the way, is
  gone once the transcript scrolls.

A run has three layers: artifacts (partly captured, in the Bean), execution (lost) and
conversation (lost).

## Then, with the hook

This folder ships a working trace hook, `trace-run.sh`. Install it from `sandbox/`:

```bash
mkdir -p .claude/hooks
cp ../exercises/06-observability/trace-run.sh .claude/hooks/trace-run.sh
```

Then add a `Stop` entry next to the existing hooks in `.claude/settings.json`, keeping
everything else in the file:

```json
"Stop": [
  { "hooks": [{ "type": "command", "command": "bash .claude/hooks/trace-run.sh" }] }
]
```

Commit the hook (`git add .claude && git commit -m "trace hook"`), since `/implement` refuses a
dirty tree. Restart your Claude session so the hook loads (exit, then run `claude` again: settings are read
at startup). Run a station again, then look:

```bash
cat runs/trace.jsonl
```

Every turn now leaves a line, since the `Stop` hook fires at the end of each reply: timestamp,
branch, files changed, commit count. `runs/` is in `.gitignore`, so the trace never dirties the
tree `/implement` checks.

## Compare

- What can you see now that you could not before?
- Which of the three layers did the hook capture, and which is still missing?
- Open `.claude/hooks/trace-run.sh`: it is a handful of lines. What one field would you add for
  your team's factory?

## Reflection

What is invisible when a run goes wrong, and which layer would you most want back?
