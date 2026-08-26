# /ralph -- Autonomous Iteration Loop for Claude Code

> Define a task. Set a completion condition. Let it run.

Ralph is an autonomous iteration loop. Give it a task, a verifiable completion condition, and a max iteration cap. It works until done or stopped.

## Install

```bash
mkdir -p ~/.claude/commands
cp ralph.md ~/.claude/commands/
```

Then type `/ralph` and define your task.

## How It Works

1. Define: task, completion condition ("all tests pass"), max iterations (default 10)
2. Ralph iterates: work → check condition → continue or stop
3. Reports each iteration: what was attempted, current state
4. Auto-stops if no progress for 3 consecutive iterations
5. Final report: succeeded or exhausted

## Safety

- Max iteration cap prevents runaway loops
- 3-iteration stall detection surfaces problems early
- Operator can interrupt at any time


<!-- forge-usage:v1 -->

## What it actually does

`/ralph` turns a task with a checkable finish line into an unattended loop: work, check the
condition, repeat, stop. You supply three things and then stop being the feedback relay —

1. **Task** — clear and specific.
2. **Completion Promise** — exactly verifiable. "All tests pass", "0 lint errors", "build
   succeeds". If no command's output or exit code can decide it, it is not one.
3. **Max Iterations** — the safety cap. Default 10.

Every iteration reports its number, what it attempted, and the current state. It ends on one
of two words: **succeeded** (condition met) or **exhausted** (cap reached, condition not
met). Exhausted is reported plainly rather than dressed up.

## What it does not have

Stated up front because these are the ways it bites:

- **No state between runs.** Each iteration works from the current state of the code plus the
  conversation. A restart starts over; there is no resume point.
- **No rollback.** Every iteration modifies the working tree. If iteration 3 breaks something,
  iterations 4 and 5 inherit the breakage and may build on top of it.
- **No human in the loop.** If it gets stuck it burns iterations. Watch the output.

The **3-iteration stall rule** is the one guardrail: no measurable progress for three
consecutive iterations and it stops and surfaces rather than spending the rest of the budget.

## The sharp edge is the completion promise

The weakest link is not the model, it is your finish line. If the string `0 errors` can appear
in the output for the wrong reason, the loop stops early and reports success — and you get a
confident "succeeded" on a job that is not done. Write the promise so it can only be true
when the work is actually finished, and prefer an exit code to a string match.

## Usage

```bash
mkdir -p ~/.claude/commands
cp ralph.md ~/.claude/commands/
```

```
/ralph
Task: fix every failing test in tests/api/
Completion Promise: `pytest tests/api/` exits 0
Max Iterations: 8
```

It confirms the setup with you before the first iteration.

## When not to use it

- The task is not mechanically verifiable — the loop cannot know when to stop.
- The work needs judgment at every step: design, naming, prioritisation, writing.
- A wrong iteration would cause damage you cannot undo. There are no guardrails here beyond
  the cap and the stall rule.

Its sweet spot is fixing existing things — migrations, lint cleanup, test coverage, build
errors — not generating new ones.

## Requirements

Claude Code with a `~/.claude/commands/` directory. Self-contained: no protocol file, no
dependencies, nothing to configure.

<!-- /forge-usage:v1 -->

## Part Of

This command is part of the [Logos Protocol](https://github.com/angyal168/logos-protocol) -- an open protocol for building an AI assistant that actually knows you.

## License

MIT

<!-- forge-related:v1 -->

## Related

This repo is one module. It handles unattended iteration loops; it does not compose itself into a working system -- that wiring is a separate job.

- **[The Forge Full Stack Bundle for Claude Code](https://notes.aingyal.com/go/gh-ralph/nlajnm/)** -- a paid pack of Claude Code commands from the same author ($129).
- [All tools, free and paid](https://tools.aingyal.com/?utm_source=github&utm_medium=readme&utm_campaign=ralph) -- the full index.

Listed so you can find them if they are useful to you. Nothing here is required to use this repo, which stays free.

<!-- /forge-related:v1 -->
