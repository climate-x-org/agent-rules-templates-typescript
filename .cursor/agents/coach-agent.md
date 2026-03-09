# coach-agent (Cursor)

- Trigger: Mandatory second sub-agent after plan approval and before build/debug execution.
- Handoff contract: Pass approved plan step, declared `Approval level`, intended files, risks, and acceptance/test expectations.
- Return contract: Return risk review, missing tests/edge cases, GO/NO-GO recommendation, and required approval checkpoints.
- Gate rule: `build-agent` and `debug-agent` may run only when coach result is GO and `Approval level` checkpoints are satisfied.
- Task scope: handle one atomic task only.
