---
name: swarm
description: Launch parallel agents, one lane each, to work through many issues at once. Use when the user says "swarm" and lists lanes (e.g. "swarm - ui, media, a11y, background") or has a backlog to split by responsibility. Plans first, works in worktrees, reviews in an approval ladder. Never ships.
---

# swarm

A coordinator plus one agent per lane. Lanes work in parallel on separate branches; the user approves bottom-up; nothing goes live.

## House rules
- First line of every reply: `Mode: swarm <phase> — will: plan, coordinate, edit and commit on lane branches; won't: deploy or merge into a deploying branch`.
- Nothing starts until the user approves the plan.
- Each lane works in its own git worktree and branch. Lanes use dark-run behaviour: commit, never ship.
- Never merge into a branch that deploys (check `SHIPPING.md` if present; if unsure, ask). Merge into an integration branch (default `swarm/<date>`). Promoting it to production is a separate `ship` step.
- If it is unclear whether the user wants action or an explanation, explain or ask.

## Lane contract
Every lane has: **Mission** (one sentence), **Owns** (paths it may edit), **Doesn't touch** (everything else), **Assigned issues**, **Done means** (checkable: tests pass, no console errors, screenshots match), **Report** (what changed, evidence, open questions).

## Phases

### 1. Plan (nothing runs yet)
The coordinator reads the issues and presents:
- Lane table: lane, mission, assigned issues, owned paths.
- Items that fit two lanes or none, as questions for the user.
- Overlap warning: files more than one lane is likely to touch. Shared files (tokens, layout, `package.json`, lockfile) get exactly one owner.
- Dependencies: lanes that must run in sequence.
- **Cap and cost**: recommended number of agents, and a plain note that parallel agents multiply cost roughly by the lane count. Suggest merging lanes when issues are small. Default cap: 4 lanes unless the user asks for more.
- Then ask: "Approve, or tell me what to change."
The user tweaks scope here. Mid-flight changes (reassign an issue, widen a lane, pause one) are handled by updating the plan and telling the affected agents.

### 2. Work
- Launch lane agents in parallel, each in its own worktree.
- Each lane produces several small branches, grouped by issue or theme, so reviews stay small.
- **Out-of-lane rule**: a problem outside a lane goes into a shared `findings` note for the coordinator; it is not fixed.
- **Messaging**: lanes message each other only when their work overlaps (e.g. "I changed the button tokens"). Everything else goes to the coordinator.

### 3. Approval ladder
1. **Level 1**: the user approves each branch within a lane.
2. **Level 2**: approved branches are raised to the coordinator, which checks them together (conflicts, tests, dependencies).
3. **Level 3**: the coordinator merges into the integration branch. Independent branches merge as they arrive; dependent ones wait for what they depend on and merge in order.

### 4. Wrap-up
One combined report: branches merged, branches waiting, findings logged, checks run, anything left. Then: "Integration branch is not live. Use `ship check` when ready." Offer to run the session's handoff if the user has one.
