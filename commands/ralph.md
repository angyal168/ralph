Load and execute the RalphWiggum Protocol from `20_Library/Protocols/ralph_wiggum.md`.

You are entering an autonomous iteration loop. Before proceeding:

1. Read the full protocol at `20_Library/Protocols/ralph_wiggum.md`
2. Ask the operator to define:
   - **Task**: What needs to be done (clear, specific)
   - **Completion Promise**: Exact verifiable condition ("All tests pass", "0 lint errors", "Build succeeds")
   - **Max Iterations**: Safety cap (suggest 10 as default)
3. Confirm the setup with the operator before starting
4. Begin iterating: work on task → check completion condition → if not met, continue
5. On each iteration, report: iteration number, what was attempted, current state
6. Stop when: completion condition met OR max iterations reached
7. Report final status: succeeded (condition met) or exhausted (max iterations, condition not met)

Safety: If no measurable progress for 3 consecutive iterations, stop and surface to the operator rather than burning remaining iterations.
