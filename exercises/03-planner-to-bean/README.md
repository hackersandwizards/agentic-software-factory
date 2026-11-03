# 03 Planner to Bean

Time: 30 to 45 minutes

## Goal

Turn your planning Skill from [01](../01-planning-skill/README.md) into the factory's first
station: it creates a Bean instead of a `.plans/<task>.md` file. If you skipped 01, start from the
frontmatter below.

## Exercise

Change or create:

```text
sandbox/.claude/skills/planner/SKILL.md
```

Frontmatter:

```yaml
---
name: planner
description: Use when starting a new feature. Creates a new Bean with a high-level plan and acceptance criteria. No code, no file paths.
argument-hint: brief feature description
allowed-tools: Read, Grep, Glob, Bash
---
```

Required workflow:

1. Capture the feature idea.
2. Clarify only if needed.
3. Present 2 or 3 approaches.
4. Stop and wait for the user's explicit approach choice.
5. Self-review for abstraction level.
6. Create a Bean through the `beans` CLI.

Required Bean section:

```markdown
## High-Level Plan

**Approach**: ...

**Steps**

- ...

**Acceptance Criteria**

- ...

**Non-Goals**

- ...
```

## Hard rules

- Do not edit source code.
- Do not edit `.beans/*.md` directly.
- Do not include file paths, function names, class names or line numbers.
- Use `beans create`.
- The heading must be exactly `## High-Level Plan`.

## Test

```bash
cd sandbox
claude
> /planner Add a power operator ^ to the calculator
```

Inspect:

```bash
beans list
beans show <new-id>
```
