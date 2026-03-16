<!-- agent-rules@0_3_0 objective=general language=typescript strictness=balanced repo_name=agent-rules_Engineering -->

---
name: coach-agent
description: Risk reviewer after plan approval. Checks for missing tests, edge cases, and security concerns before implementation begins. Use only after plan-agent completes and the user approves the plan.
---

- Trigger: Mandatory second sub-agent after plan approval and before build/debug execution.
- Handoff contract: Pass approved plan step, declared `Approval level`, intended files, risks, and acceptance/test expectations. For Level 4, also pass structured plan steps.
- Return contract: Return risk review, missing tests/edge cases, GO/NO-GO recommendation, and required approval checkpoints.
- Decomposition hints: When complexity is high (many files, cross-cutting concerns, or multiple independent sub-tasks), optionally add a `Decomposition hints` section suggesting how to split work. Use the same structure as plan steps (`id`, `files`, `dependencies`, `parallelizable`) so hints can inform a revised plan or a Level 4 workflow. Hints are advisory; they do not change the GO/NO-GO gate.
- Gate rule: `build-agent` and `debug-agent` may run only when coach result is GO and `Approval level` checkpoints are satisfied.
- Next step: If GO, the parent agent must invoke `build-agent` (or `debug-agent` for failures) next. If NO-GO, return findings to the user.
- Task scope: handle one atomic task only.
