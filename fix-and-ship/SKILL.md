---
name: fix-and-ship
description: Fix a problem with options, figures and a recommendation, then put it live after the user approves. Use when the user says "fix-and-ship" or wants a problem solved and shipped in one flow. Requires the project's SHIPPING.md. The user's approval is mandatory before anything goes live.
---

# fix-and-ship

Diagnose, compare options, recommend, wait for approval, then fix and ship.

## House rules
- First line of every reply: `Mode: fix-and-ship <phase> — will: <what this phase does>; won't: go live without approval`.
- Read `SHIPPING.md` before any shipping action and follow it exactly. If it is missing, stop and use `ship-setup`. Never guess a deploy command or target.
- If the request conflicts with `SHIPPING.md`, say so; do not override it silently.
- Nothing goes live without the user's explicit "approved" for this change. `SHIPPING.md` never replaces that approval.
- If it is unclear whether the user wants action or an explanation, explain or ask.

## Phases

### 1. Diagnose
Find the real cause (see `recon cause`). No band-aids; say whether each option treats the cause or the symptom.

### 2. Options
Present a table: option, what it does, gain (with figures where measurable), trade-offs, effort, risk.
- If one option is better on every axis with no real compromise, say "clear pick, no trade-off" and recommend it.
- Otherwise recommend one and say what would change the recommendation.

### 3. Stop for approval
Ask: "Approve option X?" Do not edit anything before the answer. The approval covers that option and its stated scope.

### 4. Implement and verify
- Work on a branch. Commit in small steps.
- Run `SHIPPING.md`'s pre-ship checks plus anything specific to this fix.
- Compare results to the figures promised in step 2. If checks fail, the gain is smaller than promised, or the scope grew, stop and ask again.

### 5. Ship
- Check for drift: if the pipeline or deploy files changed since `SHIPPING.md` was last updated, flag it and ask before continuing.
- Execute exactly the deploy path in `SHIPPING.md`.
- Report what ran, against which environment, the result, and how to roll back.
