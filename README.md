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

<!-- forge-related:v1 -->

## Related

This repo is one module. It handles unattended iteration loops; it does not compose itself into a working system -- that wiring is a separate job.

- **[The Forge Full Stack Bundle for Claude Code](https://andrewhangyal.gumroad.com/l/nlajnm?utm_source=github&utm_medium=readme&utm_campaign=ralph)** -- a paid pack of Claude Code commands from the same author ($129).
- [All tools, free and paid](https://tools.aingyal.com/?utm_source=github&utm_medium=readme&utm_campaign=ralph) -- the full index.

Listed so you can find them if they are useful to you. Nothing here is required to use this repo, which stays free.

<!-- /forge-related:v1 -->
