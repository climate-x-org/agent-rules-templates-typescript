# agent-rules Engineering Antigravity Guidance

Provider target: Antigravity

This file supplements `AGENTS.md` with provider-specific configuration.
Full engineering guidance (base rules, workflow contract, task recipes,
verification checklist) is defined in `AGENTS.md`.

## Provider Configuration
- Agent directory: `.agents/skills`
- Workflow agents: `plan-agent`, `coach-agent`, `build-agent`, `debug-agent`

## Workflow Chain
For every code-change request, delegate through agents in this strict order:

1. `plan-agent` — produce plan, then STOP and wait for user approval
2. `coach-agent` — review risks/tests, return GO or NO-GO
3. `build-agent` (implementation) or `debug-agent` (failures) — execute approved work
4. **verify** — run lint, type-check, and test commands
5. **handoff** — summarize changes, evidence, and next steps

Do not skip steps or reorder. Each agent returns results to the parent before the next is invoked.
