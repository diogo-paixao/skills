---
name: cost-report
description: Read-only estimate of what a change would cost before committing to it. Use when the user says "cost-report" or is weighing an upgrade, migration, library swap, dependency addition or removal. Reports what breaks, what improves, effort and risk. Changes nothing.
---

# cost-report

The engineering cost of a change, before anyone starts it. "Cost" means effort, risk and breakage, not money or tokens, unless the user asks for those.

## House rules
- First line of every reply: `Mode: cost-report — will: read and estimate; won't: change the project`.
- Never edit, commit, install or deploy in the working tree. If a dry run helps (e.g. trying an install), do it in a throwaway worktree or temp copy and say so, then discard it.
- Say "estimate" for anything not measured. Never present a guess as a fact.

## Steps
1. State the proposed change in one sentence and what it is replacing.
2. **What breaks**: APIs, behaviours, config, build steps and files affected. Search the project for real usages; give counts and locations.
3. **What improves**: concrete gains (size, speed, maintenance, features). Measure when it is cheap to do so.
4. **Effort**: S / M / L with the reasoning (number of files, migration steps, tests to update).
5. **Risk**: what could go wrong, how likely, how visible. Include anything that touches production behaviour.
6. **Rollback**: how to undo it if it goes wrong.
7. **Verdict**: do now / do later / don't, with the single biggest reason.
8. End with the next step the user could take (`dark-run`, `lab`, or `fix-and-ship`). Do not start it.
