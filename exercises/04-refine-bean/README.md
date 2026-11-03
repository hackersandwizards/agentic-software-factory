# 04 Refine Bean

Time: 45 to 60 minutes

## Goal

Build `/refine`: it reads a Bean with `## High-Level Plan`, explores the codebase through one
read-only subagent, and appends `## Refined Plan`.

## Exercise

Create:

```text
sandbox/.claude/skills/refine/SKILL.md
```

Frontmatter:

```yaml
---
name: refine
description: Use after /planner. Takes a Bean with ## High-Level Plan, explores the codebase through a read-only subagent, and appends ## Refined Plan.
argument-hint: <bean-id>
allowed-tools: Read, Grep, Glob, Bash, Agent
---
```

Required workflow:

1. Read the Bean with `beans show <bean-id> --json`.
2. Parse `.body`.
3. Extract the literal `## High-Level Plan` section.
4. Abort if the section is missing.
5. Set status to `in-progress`.
6. Dispatch exactly one read-only subagent to explore the codebase.
7. Compose and append `## Refined Plan`.
8. Verify every referenced existing path.

Required schema:

```markdown
## Refined Plan

### Files to change

- path:line: what changes
- path:NEW: why a new file is needed

### New signatures

- ReturnType functionName(Args): purpose

### Test sketch

- test name: Input -> Expected
```

## Hard rules

- Do not edit source code.
- Do not edit `.beans/*.md` directly.
- Use exactly one subagent dispatch.
- The subagent is read-only: no edits, no builds, no tests.
- Every existing path in the refined plan must be verified.
- The heading must be exactly `## Refined Plan`.

## Test

The sandbox ships `sandbox-exercise-olqc` (parentheses support) with a `## High-Level Plan` and no
refined plan yet. Refine it, or a Bean your own `/planner` created:

```bash
cd sandbox
claude
> /refine sandbox-exercise-olqc
```

Then `beans show sandbox-exercise-olqc` and check every path under `### Files to change` against
the code.
