---
name: ship-setup
description: Draft a project's SHIPPING.md from what the repo contains. Use when the user says "ship-setup", or when ship or fix-and-ship stops because SHIPPING.md is missing. Read-only discovery, labels every line, writes the file only after the user confirms.
---

# ship-setup

Creates the project's shipping config that `ship` and `fix-and-ship` depend on. Facts come from the repo; decisions come from the user.

## House rules
- First line of every reply: `Mode: ship-setup — will: read the repo and draft SHIPPING.md; won't: deploy, touch live environments, or write the file before confirmation`.
- Read-only discovery. Never run a deploy. Never call a live environment to "check".
- Never fill a gap with a plausible guess.

## Steps
1. **Discover** (read-only): CI workflows, hosting config (`vercel.json`, `.vercel/`, `netlify.toml`, `wrangler.toml`, `fly.toml`, Dockerfile), package scripts (including any pre/post build or upload scripts), git branches, tags and commit style, README, CONTRIBUTING, `AGENTS.md`/`CLAUDE.md`, `.env.example`.
2. **Draft** `SHIPPING.md` from `SHIPPING.template.md` in this skill's folder. Label every line:
   - **Found** (with the file it came from)
   - **Inferred** (with the reasoning)
   - **Unknown, needs you**
3. **Ask** about what a repo cannot tell you: approval rules, never-do items, rollback if undocumented, which branch ships. These are the user's decisions, so always questions.
4. **Show the draft** and wait for confirmation or edits.
5. **Write** `SHIPPING.md` at the repo root only after confirmation. Do not commit it without being asked.
6. Note the date and the pipeline files it was based on at the top, so `ship` can detect drift later.
