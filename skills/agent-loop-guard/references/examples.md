# Scenario checks

Use these as instruction walkthroughs, not proof of runtime enforcement.
For each trace, apply SKILL.md before the next action.

| Scenario | Actions and observable evidence | Required decision |
| --- | --- | --- |
| Normal execution | Read a failing test: new cause identified. Fix it: diff addresses cause. Run test: passes. | Each verified advance resets stagnation to 0; return completed. No arbitrary three-action cap. |
| Identical calls | Search returns no matches; propose same query with reordered arguments and unchanged corpus. | Stagnation is 1. Reject the duplicate before executing; use a new source with a reason or stop early. |
| Retry exhaustion | Build fails with missing dependency. Correct manifest and retry: same failure. Correct install location and retry: same failure. | Same operation/signature has 3 failures despite strategy changes. Stop; block fourth build. Verified intermediate fixes cannot reset attempts. |
| Stagnation | Three distinct searches test plausible hypotheses but yield no useful facts. | Stagnation becomes 1, 2, 3. Stop immediately after third result; do not issue fourth search. |
| Depth limit | Root A delegates to B; B delegates to C. C proposes spawning D. | C is depth 2. Reject spawn. C may execute useful work directly within budgets or return blocked. |
| Circular delegation | B asks active ancestor A to take over B's unresolved task, or C hands it sideways to an agent already handling it. | Reject the circular assignment. Return a final structured handoff up the parent chain instead. |
| Successful parent handoff | B detects repeated unchanged API failures and returns the handoff below. A has an existing local export. | Merge B's counts; do not retry API through C. Validate export freshness and use it if adequate. |
| Edit cycle | Edit A to B, then revert to A, then propose B again without new evidence. | Do not claim new progress for restored states. Reject the cycle; preserve useful artifacts and hand off. |
| Productive recovery | Search finds nothing (1); inspect a different source and verify required fact (0); produce and verify artifact (0). | Continue and complete; a single miss does not stop normal work. |
| Counter evasion | After three failures, rename operation or launch sibling with zero counts. | Map to existing operation/signature, retain 3, reject execution. |
| Reasoning loop | Three planning passes add no actionable information or evidence. | Count 1, 2, 3 even without tools; stop. Do not start a fourth self-evaluation. |

## Parent handoff example

Child at depth 1 returns and stops:

```yaml
status: loop_detected
objective: "Obtain the report's source records"
attempts: {"read records API / access_denied": 3}
progress: ["Report schema verified in local schema.json"]
last_error: "API returned access_denied"
stop_reason: "Three failed attempts for the same operation/error signature"
recommended_next_action: "Validate the existing local export and build from it if complete"
```

The parent retains the API count of 3. It verifies the export's date, coverage,
and schema, then builds and checks the report. It returns completed with the
report reference. If the export is insufficient and no useful path remains,
it reports blocked with the verified schema and missing records to the user.
It does not claim that API access succeeded.

## Integration smoke check

1. Give the root this skill and a completion criterion; set depth 0 and empty counts.
2. Delegate a separate useful subtask with depth 1, ancestry, and shared counts.
3. Return a child result; merge evidence and counters, counting the outcome once.
4. Verify productive work continues and failed operations keep their original counts.
5. In a host implementation, reject forbidden actions before dispatch, including
   simultaneous siblings that would exceed a shared budget.

These traces test instruction decisions only. Validate actual model compliance
and host enforcement separately in the deployment environment.
