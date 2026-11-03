# Take your factory home

Two steps. The first carries the factory you built in the sandbox off the calculator and onto a
real project. The second adds the loop that makes it improve. They mirror the two halves of the
training: first the spine, then the loop.

If you are in the session, open [EXERCISE.md](EXERCISE.md). It is the timed, step-by-step guide
for both steps. This page holds the mechanics it refers to.

## The spine: your factory on a real project

1. Make a new repo for your project:

   ```bash
   mkdir ~/my-project && cd ~/my-project
   git init
   ```

2. Scaffold a minimal real project. Paste the scaffold prompt below into Claude Code. It creates
   the smallest thing the factory can run against.

3. Copy your factory in: the skills, settings and hooks you built in the sandbox, and the Beans
   config. The trailing dot matters:

   ```bash
   cp -R <path-to>/agentic-software-factory/sandbox/.claude/. .claude/
   cp <path-to>/agentic-software-factory/sandbox/.beans.yml .
   printf '.beans/\nruns/\n' >> .gitignore
   ```

   Rename the Bean prefix in `.beans.yml` to your project's short name.

4. Take the factory off the calculator. Your skills run `npm run build` and `npm test` and may
   name calculator files as examples. Replace both commands with your project's own, and write
   them into `CLAUDE.md` under a `## Build and test` heading, so the implement gate and the next
   reader find them in one place.

5. Commit the skeleton, so the implement station starts from a clean tree:

   ```bash
   git add -A
   git commit -m "scaffold + factory"
   ```

Then run a work item through all three stations:

```text
/planner <your feature in one sentence>
/refine <bean-id>
/implement <bean-id>
```

### The scaffold prompt

```text
Scaffold the smallest real project I can run an agent factory against.
Stack: <pick one, e.g. TypeScript + Vitest, Python + pytest, Go>.

Create only a skeleton, not the feature:
- a manifest with a build command and a test command
- one source file with one trivial function
- one passing test for it
- extend .gitignore with this stack's dependency, build, and test-cache folders
  (e.g. Python: __pycache__/, .pytest_cache/; Node: node_modules/, dist/). The
  implement gate runs build and test, and an un-ignored cache dirties the tree
  and aborts the next feature's preflight

Then install dependencies, run the build, run the tests, and show me all three
green. Write the build and test commands into CLAUDE.md under "## Build and test".
Do not build any feature yet, I will do that through /planner next.
```

### What carries over

Two things are project specific: the build command and the test command. Every phase, every
guardrail and the station contract stay as you built them. Check it with a diff:

```bash
diff -ru <path-to>/agentic-software-factory/sandbox/.claude/skills .claude/skills
```

## The loop: instrument/

Evals that tell a good Bean from a bad one, and one guard that runs on every implement. Use it
once you have done exercises 06 to 08. See [instrument/README.md](instrument/README.md).

## The one thing to take away

The calculator was the rig. The factory is the product. The skills you point at your own codebase
are the same ones you built here. The contract and the guardrails carry over unchanged. Only the
build and test commands are project specific.
