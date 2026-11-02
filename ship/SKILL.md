---
name: ship
description: Final gate and release. Use when the user says "ship check" (read-only go/no-go before going live) or "ship go" (release after explicit approval). Follows the project's SHIPPING.md. If it is missing, stops and points to ship-setup.
---

# ship

Two modes: **check** (read-only) and **go** (release). Both follow the project's `SHIPPING.md`.

## House rules
- First line of every reply: `Mode: ship <mode> — will: <check | release per SHIPPING.md>; won't: go live without approval`.
- Read `SHIPPING.md` first. If missing, stop and use `ship-setup`. Never guess a deploy command or target.
- **Drift check**: compare `SHIPPING.md` against the current pipeline and deploy files (CI workflows, `vercel.json`, deploy scripts, package scripts). If they changed after the doc was last updated, flag it and ask before trusting it.
- If the request conflicts with `SHIPPING.md`, say so; do not override it silently.
- Going live needs the user's explicit "approved" for this specific release. `SHIPPING.md` never replaces it.

## Modes

### check (read-only)
1. Read `SHIPPING.md`; run the drift check.
2. Verify, using the project's own commands where they exist:
   - Pre-ship checks from `SHIPPING.md` (tests, build, lint, types, budgets).
   - Changelog or release notes updated.
   - Env vars present and documented for the target environment.
   - Head tags and other easy-to-miss items listed in `SHIPPING.md`.
   - No stray debug code, leftover TODOs or unintended files in the diff.
   - Rollback plan exists and is realistic.
   - Smoke-test plan: what to click or hit right after release.
3. Report a table of checks with pass or fail, then a clear **go / no-go** with the single biggest reason.
4. Do not release.

### go (release)
1. Run **check** first. Any fail means stop and report.
2. Show exactly what will happen: environment, commands, what is being released. Ask for "approved" unless the user has already given it for this exact release in this conversation.
3. Execute the deploy path from `SHIPPING.md` and nothing else.
4. Run the smoke tests.
5. Report: what ran, against which environment, result, and the rollback steps. If the smoke test fails, say so immediately and offer the rollback; do not roll back without asking unless `SHIPPING.md` says to.
