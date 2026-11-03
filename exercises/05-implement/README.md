# 05 Implement

Time: 45 to 60 minutes

## Goal

Build `/implement`, the first station that writes code: it reads a Bean with `## Refined Plan`,
works on a feature branch with a hard build and test gate before every commit, and logs the result
back to the Bean.

## Exercise

Create:

```text
sandbox/.claude/skills/implement/SKILL.md
```

Frontmatter:

```yaml
---
name: implement
description: Use after /refine. Takes a Bean with ## Refined Plan, implements it step by step on a feature branch with a build and test gate before every commit, and appends ## Implementation Log.
argument-hint: <bean-id>
allowed-tools: Read, Edit, Write, Bash, Glob, Grep
---
```

Required workflow:

1. Preflight, read-only: read the Bean with `beans show <bean-id> --json` and extract the
   `## Refined Plan` section.
2. Abort before touching anything when the section is missing or empty, the Bean is `completed`,
   the working tree is dirty (`git status --porcelain`), or you are not on `main`.
3. Create the branch `feat/<bean-id>-<slug>`. Abort if it already exists.
4. For each step under `### Files to change`: edit, run `npm run build`, run `npm test`, then
   commit only the files this step touched. Give each step at most two fix attempts.
5. Append `## Implementation Log` to the Bean: branch, one line per commit with its SHA, and the
   final test status.
6. All green: set the Bean to `completed`. Still red: leave it `in-progress` and write down the
   last error and what the fix attempts tried.

## Hard rules

- Never commit on `main`. Check the branch before every commit, not only the first.
- Stage files by name, never `git add -A` or `git add .`.
- No commit with a failing build or failing tests.
- Do not edit `.beans/*.md` directly: fetch the body, append locally, write it back with
  `beans update <bean-id> --body-file <file>`.
- Never push and never merge.

## Test

Implement the Bean you refined in [04](../04-refine-bean/README.md). The preflight refuses a dirty
tree, and your new skills and the refined Bean count as changes, so commit them first (and
`.plans/` from 01, if you kept it):

```bash
cd sandbox
git add .claude .beans
git commit -m "factory: planner, refine, implement"
claude
> /implement sandbox-exercise-olqc
```

Then check:

```bash
git log --oneline main..HEAD
npm test
beans show sandbox-exercise-olqc
```

Try the guards too: run `/implement` again on the completed Bean, and once with an uncommitted
change. Both must stop before creating a branch.
