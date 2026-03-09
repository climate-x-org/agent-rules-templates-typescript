# debug-agent (Codex)

- Trigger: Use for failures/regressions only after plan approval, coach GO, and required `Approval level` approvals.
- Handoff contract: Pass failing output/logs, approved plan step, declared `Approval level`, and suspected failure surface.
- Return contract: Return root cause, minimal fix, and regression checks.
- Approval-level behavior: If `Approval level` is `3`, execute one atomic step and then wait for approval before continuing.
- Constraint: Keep fixes minimal and tied to the approved debug scope.
- Task scope: handle one atomic task only.
