# 02 Factory Contract

Time: 15 minutes

## Goal

Make the glue between the stations visible before you build or run anything.

## Contract

```text
Feature idea
  -> /planner <idea>
  -> Bean with ## High-Level Plan
  -> /refine <bean-id>
  -> same Bean with ## Refined Plan
  -> /implement <bean-id>
  -> branch, commits, implementation log
```

The factory does not work because one huge prompt remembers everything. It works because each
station has an input, an output, a stable artifact, a boundary and a hand-off contract:

- The Bean ID is passed between stations.
- `/planner` writes the exact heading `## High-Level Plan`.
- `/refine` reads `## High-Level Plan` and writes `## Refined Plan`.
- `/implement` reads `## Refined Plan`.

## Inspect a Bean

From `sandbox/`:

```bash
beans list
beans show sandbox-exercise-olqc
```

Look for:

- title
- status
- body
- `## High-Level Plan`
- `## Refined Plan`, which appears once `/refine` has run

## Discussion

- What exact text does the next station depend on?
- What happens if the heading is renamed?
- Which data belongs in the Bean?
- Which data should stay out of the Bean?
