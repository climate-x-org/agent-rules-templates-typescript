<!-- agent-rules@0_3_0 objective=general language=typescript strictness=balanced repo_name=agent-rules_Engineering -->

---
name: plan-agent
description: Mandatory first sub-agent for coding, refactoring, and debugging requests. Creates a detailed plan for review before any code is written. Always use this agent before coach-agent, build-agent, or debug-agent.
---

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
  `Level: <1|2|3|4>`
  `Why: <short rationale>`
  `Required checkpoints: <checkpoint list>`
- If `Level: 4`, the `Plan steps` section is required (not optional).
- Formatting requirements:
  - Do not number section headings.
  - Use concise bullets under `Summary`, `Key Changes`, `Test Plan`, and `Assumptions`.
  - Use plain key-value lines only under `Approval level`.
  - Do not add extra sections or trailing handoff text in the plan output.
- Optional structured steps: For multi-step or decomposition-friendly plans, include a `Plan steps` section after `Approval level` containing a JSON block conforming to `schema/plan-steps.schema.json`. Each step object has: `id` (required, unique), `description`, `files` (repo-relative paths), `dependencies` (IDs of prerequisite steps; must reference existing IDs and must not form cycles), `parallelizable` (boolean, default false). Omit this section for simple single-step tasks.
- Approval gate: The final non-empty line must be exactly `WAITING_FOR_APPROVAL`; do not request code edits in this step.
- Next step: After user approves this plan, the parent agent must invoke `coach-agent` before any implementation.
- Task scope: handle one atomic task only.
