Enter an autonomous iteration loop: work the task, check the completion condition, repeat
until the condition is met or the iteration cap is reached.

This command is self-contained. Everything the loop needs is below.

## Before starting, get three things from the operator

1. **Task** — what needs to be done, clear and specific.
2. **Completion Promise** — an exactly verifiable condition, not a feeling. "All tests pass",
   "0 lint errors", "the build succeeds". If it cannot be checked by a command's output or
   exit code, it is not a completion promise.
3. **Max Iterations** — a safety cap. Suggest 10 as the default.

Confirm the setup with the operator before the first iteration.

## The loop

1. Work on the task.
2. Check the completion condition.
3. If it is not met, iterate again from the current state of the code.
4. On every iteration report: iteration number, what was attempted, current state.
5. Stop when the completion condition is met OR max iterations is reached.
6. Report the final status honestly as one of two words: **succeeded** (condition met) or
   **exhausted** (cap reached, condition not met). Exhausted is not a failure to hide.

## Properties to be honest about

- **No state between runs.** Each iteration works from the current state of the code plus
  the conversation. There is no checklist, no resume point; a restart starts over.
- **No rollback.** Every iteration modifies the working tree. If iteration 3 breaks
  something, iterations 4 and 5 inherit the breakage and may build on it.
- **No human in the loop.** If it gets stuck, it burns iterations. Watch the output.

## Safety rules

1. **Always set max iterations.** An unbounded loop is the dangerous version of this.
2. **The completion promise must be precise.** If the string "0 errors" can appear in the
   output for the wrong reason, the loop will stop early and report success.
3. **3-iteration stall rule.** If there is no measurable progress for three consecutive
   iterations, stop and surface to the operator rather than burning the remaining budget.
4. Do not run this on a task where a wrong iteration causes damage you cannot undo. There
   are no guardrails here beyond the iteration cap.

## When this is the wrong tool

- The task is not mechanically verifiable — there is nothing to check, so the loop cannot know
  when to stop.
- The work needs human judgment at each step (design, naming, prioritisation, writing).
- The work needs a structured multi-stage generation from a spec rather than repeated
  refinement of something that already exists. This loop fixes existing things; its weakest
  link is the accuracy of the completion promise.
