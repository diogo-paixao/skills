---
name: dark-run
description: Do the work and keep committing, but never put it live. Use when the user says "dark-run" or wants changes built and committed without touching production. "dark-run tidy" is a behaviour-preserving refactor with before/after proof.
---

# dark-run

Work, commit, never ship.

## House rules
- First line of every reply: `Mode: dark-run <mode> — will: edit and commit on a branch; won't: deploy, push to a deploying branch, or change production`.
- Work on a dedicated branch (or worktree). Never commit to the branch that deploys.
- If `SHIPPING.md` exists, read it for branch and commit conventions, and for which branches deploy. Follow its conventions; it can never grant permission to ship from this skill.
- Do not push unless asked. If pushing could trigger a preview or production deploy, say so and ask first.
- If it is unclear whether the user wants action or an explanation, explain or ask.
- Problems found outside the task are logged in the final report, not fixed.

## Modes

### build (default)
1. Restate the task and the branch you will use.
2. Work in small steps. Commit after each coherent step with a clear message.
3. Run the project's checks (lint, types, tests, build) as you go; do not commit known-broken work without saying so in the message.
4. Finish with a short log: branch name, commits (one line each), checks run and results, open questions, anything out of scope you noticed.
5. State clearly: "Not live. Nothing deployed."

### tidy: refactor with no behaviour change
1. Before touching code, capture a baseline: tests, build output, and screenshots or snapshots for UI.
2. Refactor in small commits.
3. After each step, re-run the baseline and compare. Any difference stops the work until explained.
4. Report proof of equivalence: before/after test results, bundle or output diff, screenshots.
5. If a behaviour change is unavoidable, stop and ask. Do not slip it in.
