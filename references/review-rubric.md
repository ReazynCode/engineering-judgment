# Engineering review rubric

Load after the independent attempt is complete. This rubric guides critique, not the initial user prompt. It is not a mandatory checklist to recite.

| Lens | Review focus |
| --- | --- |
| Requirements | Real user outcome, scope, constraints, observable success, ambiguous or unsupported assumptions. |
| Architecture | How responsibilities/data flow meet those requirements, boundaries, ownership and persistence where needed; avoid prescribing technologies without justification. |
| Failure Modes | Plausible interruptions, inconsistent state or external failures relevant to the actual flow; recovery, user visibility and completed-work preservation. |
| Tradeoffs | Complexity versus benefit at expected usage, cost/latency where material, reversibility, simpler alternatives and overengineering. |
| Verification | Evidence that proves the user outcome, meaningful failure/recovery coverage and observability; distinguish mocked, live and still-unverified behavior. |

Review all five lenses, but report only meaningful strengths and prioritized gaps. For each significant gap, connect the user's assumption → a realistic consequence → the underlying concept → a focused invitation to reconsider. Clearly label missing facts versus mistaken reasoning. Research external facts when needed; do not ask the user to guess facts you can verify. Do not turn every possible risk into a requirement.

Recommendations are proposals until the user adopts them. Do not flatter incorrect reasoning, invent certainty, or silently supply the whole architecture. Invite one revision/confirmation round and continue only as needed for consequential unsettled points. A category intentionally left blank can be discussed in review; it is not grounds for an endless interview.
