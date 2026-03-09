# plan-agent (Codex)

- Trigger: Mandatory first sub-agent for coding, refactoring, and debugging requests.
- Handoff contract: Pass goals, constraints, impacted files, acceptance criteria, and verification expectations.
- Return contract: Return only plan output until approval.
- Plan Mode path: if host supports Plan Mode, return exactly one `<proposed_plan>` block using these heading labels and order:
  `Summary`
  `Key Changes`
  `Test Plan`
  `Assumptions`
  `Approval level`
- Fallback path: if host does not support Plan Mode, return plain markdown with the same heading labels and order.
- In `Approval level`, include these exact key-value lines:
  `Level: <1|2|3>`
  `Why: <short rationale>`
  `Required checkpoints: <checkpoint list>`
- Formatting requirements:
  - Do not number section headings.
  - Use concise bullets under `Summary`, `Key Changes`, `Test Plan`, and `Assumptions`.
  - Use plain key-value lines only under `Approval level`.
  - Do not add extra sections or trailing handoff text in the plan output.
- Approval gate: The final non-empty line must be exactly `WAITING_FOR_APPROVAL`; do not request code edits in this step.
- Task scope: handle one atomic task only.
