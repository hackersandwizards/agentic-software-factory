# Agentic Software Factory

The exercises for [Agentic Software Factory: Advanced Team Training](https://www.hackersandwizards.dev/trainings/agentic-software-factory/)
by hackers&wizards. You clone this repo at the start and build a small software factory in it
with Claude Code: three stations, planner, refine and implement, that hand one work item to each
other through a durable artifact, then the observability, evals and guards that make the factory
trustworthy.

The training builds on Agentic Engineering for Developers and QA. You already know CLAUDE.md,
Skills, Rules, subagents and hooks; here they become factory stations.

## The factory

```text
/planner <idea>       -> Bean with ## High-Level Plan
/refine <bean-id>     -> same Bean with ## Refined Plan
/implement <bean-id>  -> feature branch, commits, ## Implementation Log
```

A [Bean](https://github.com/hmans/beans) is a work item in a Markdown file, managed by the `beans`
CLI. The stations never share a conversation. They share the Bean and an exact contract: the
headings each station writes and the next one reads.

## Exercises

All exercises run in `sandbox/`, a small TypeScript calculator with tests. Do them in order: each
station builds on the one before.

Build the factory:

1. [Planning Skill](exercises/01-planning-skill/README.md): a Skill that writes a plan file
2. [Factory Contract](exercises/02-factory-contract/README.md): inspect a Bean and the hand-off
3. [Planner to Bean](exercises/03-planner-to-bean/README.md): the planner creates a Bean
4. [Refine Bean](exercises/04-refine-bean/README.md): a read-only subagent turns the plan into
   files, signatures and tests
5. [Implement](exercises/05-implement/README.md): branch, build and test gate, commit, log

Make it trustworthy:

6. [See it](exercises/06-observability/README.md): a hook that traces every run
7. [Test it](exercises/07-evals/README.md): evals that tell a good Bean from a broken one
8. [Make it stick](exercises/08-learning-loops/README.md): turn an escape into a guard

Afterwards, [take-home/](take-home/README.md) carries your factory onto a project of your own and
adds its improvement loop.

## Setup

You need:

- Claude Code
- the `beans` CLI
- `jq`
- Node.js 26 or newer, with npm
- `git`

```bash
brew install hmans/beans/beans
beans version
```

Build and test the sandbox:

```bash
cd sandbox
npm install
npm run build
npm test
```

Every test passes on a fresh clone. Start Claude Code inside `sandbox/`, so its `CLAUDE.md` and
the `beans prime` hook in `.claude/settings.json` load.

## Layout

```text
exercises/   one folder per exercise, in order
sandbox/     the calculator the factory works on, with two Beans to start from
take-home/   your factory on your own project, and its improvement loop
```
