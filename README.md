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

## Part Of

This command is part of the [Logos Protocol](https://github.com/angyal168/logos-protocol) -- an open protocol for building an AI assistant that actually knows you.

## License

MIT
