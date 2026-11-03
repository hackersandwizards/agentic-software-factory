# 08 Make it stick (learning loops)

Time: 35 minutes

Close the loop. A failure you find once should never silently recur: escapes become tests.

## Goal

Turn one failure into a permanent guard, and write the lesson down.

## Red-team

Use [red-team-inputs.md](red-team-inputs.md). Commit your work first: `/implement` refuses a dirty
tree, and only input 4 is meant to test that. Feed the factory bad input and watch each station.
Find one escape: a station that continues instead of aborting, or bad output that slips past your
07 check.

Red-team the skills you built yourself: your own factory is the more honest target. If you work
with the set your trainer handed out, expect it to break less easily, since it is hardened, and
compare it with your own on the same bad input.

## Build the guard

This is where an eval stops being something you run by hand and becomes part of the process: it
runs automatically, every time the factory runs. Take the escape you found and wire a check for
it in with the right mechanism:

- a hook that blocks `/implement` when `## Refined Plan` is missing
- a rule, or a skill self-check
- a new check added to your 07 eval set, run by the station that produces the Bean

Re-run the bad input and confirm it now fails loudly. (Cheap deterministic checks like these are
worth running on every step. An LLM judge is too slow to gate every run: that kind you run
offline across many Beans, which is what the grown-up version does.)

## Codify

Add one line to the factory's `CLAUDE.md` or conventions so the lesson persists: name the check
and the signal you will watch to know it worked.

## Verify

- the bad input that escaped now fails loudly
- the lesson is written down

## Reflection

Prompt, rule, hook, script or human: which mechanism did you pick, and why?

Short on time? The smallest possible loop closure is to add a check to your 07 eval set that catches it.
