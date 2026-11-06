---
name: agent-loop-guard
description: Keep coding, analysis, and tool-based tasks focused and context-efficient; prevent unproductive retries, stagnation, and recursive delegation. Do not apply to simple conversational replies.
---

# Agent Loop Guard

Complete the task with observable evidence. Never invent progress or execution.

## Minimize scope and context

- Define the smallest scope that delivers the requested outcome. Ask one short
  question only if necessary; otherwise follow existing project conventions.
- Search before opening files; read only relevant sections. Avoid dependencies,
  caches, build output, and lockfiles unless the task specifically requires them.
- Make the smallest compatible change and reuse existing patterns.
- Batch independent reads and checks. Start validation with the smallest relevant
  check; broaden only when the change or evidence warrants it.
- Delegate only when it reduces total work, including coordination and context cost.
- Keep the final response short: result, validation performed, and real pending items.

## Keep one compact record

Before execution, define the objective and measurable completion/progress evidence
(e.g., a failing check passes, a required artifact is verified, or a new fact resolves
an uncertainty). Keep: objective, depth, active delegation path, attempt counts,
stagnation count, last action/result, and references to useful partial results.
Retain only relevant evidence; do not log full reasoning.

Use stable operation keys: intended effect + target + relevant input state.
Group equivalent tools, argument orderings, paraphrases, and renamed tasks under
the same key. Normalize error signatures by cause/code and affected resource;
ignore timestamps, request IDs, and incidental wording.

## Enforce limits

- Allow **3 total attempts**, including the first, for an operation/error signature.
  Count each execution returning that signature. Block attempt 4. Preserve counts
  across strategy changes, agents, handoffs, and context summaries.
- Start root depth at **0**; children use **1**, grandchildren **2**.
  At depth **2**, never delegate.
- Stop after **3 consecutive unproductive steps** for the objective.
  Count tool actions, searches, planning/reasoning passes, edits, and delegation
  outcomes. Reset only on verified progress toward the objective.
- Rewording, identical outputs, repeated reasoning, renaming counters, and
  temporarily undoing/reapplying the same edits are not progress.
- Never reset budgets by replacing an agent or splitting/renaming the same task.

Three is a ceiling, not a requirement to repeat a known failure.

## Before and after each action

1. Identify the objective; read remaining attempt and stagnation budgets.
2. Check depth and the active delegation path.
3. Compare the action with prior attempts. Require a concrete reason to expect
   new evidence or useful change. Skip unchanged calls, empty repeat searches,
   endless replanning, and edit/revert cycles. Change strategy or stop.
4. Execute one useful action. Do not call tools just to perform this guard check.
5. Compare the result with the progress criterion. Update attempts and stagnation
   once per action; count a returned child outcome once, not its every internal step.
6. Continue if productive. Otherwise change strategy within remaining budgets.
   Stop immediately when a limit is reached; do not perform another work action.

An identical call can be useful after a verified input/state change or a bounded
scheduled poll. Waiting alone is not progress; unchanged poll results consume
stagnation budget. Use runtime waiting/event support for long external waits.

## Delegate without cycles

Pass this guard, the objective, progress criterion, inherited counts, depth + 1,
and active agent/objective path to each child. Share attempt counts across siblings;
do not use parallel attempts to evade limits. Do not send work to an active ancestor
or revisit an unresolved objective in the active path. Returning a final result to
the parent is a handoff, not new delegation.

## Stop and hand off

Stop the affected agent's work immediately. Cancel its pending duplicate work
where supported. Preserve successful partial results. Return to the parent using:

```yaml
status: loop_detected
objective: "Specific objective"
attempts: {"operation / error signature": 3}
progress: ["Verified result or artifact reference; empty if none"]
last_error: "Observed error, or null"
stop_reason: "Limit or repeated cycle detected"
recommended_next_action: "Concrete different approach, missing evidence, or user action"
```

Use status `completed` for verified completion, `blocked` for a missing prerequisite,
and `loop_detected` for exhausted budgets or a detected cycle.
Include stagnation/depth in stop_reason when relevant.

Parents must merge counts and results before continuing. Never spawn a replacement
to repeat failed work. Continue only with materially different work or new evidence,
without reopening an exhausted operation/error budget. Stop and report partial
results and the blocker to the user when the root reaches a limit. A genuinely new
task may start fresh; relabeling unfinished work may not.

## Integrate

Load this file into the root's instructions before work. Initialize its record once.
Include these instructions and the inherited record in every subagent context.
Persist the compact record through summaries/restarts; if unavailable, recover it
or report blocked instead of assuming fresh budgets. No connector is required.

These are instruction-based safeguards, not runtime enforcement. A skill alone
cannot guarantee termination if an agent ignores instructions. For hard guarantees,
have the host enforce shared atomic counters, ancestry checks, cancellation,
tool timeouts, and an overall action/time budget outside the model. Local retry
and stagnation limits alone cannot bound an endless sequence of distinct tasks.

Read [examples.md](references/examples.md) only when integration checks or scenario
traces are needed.
