# skills

Personal agent skills for development work. Each folder is one skill (`SKILL.md` with `name` and `description` frontmatter).

## Install
```
npx skills add <your-user>/skills --list          # preview
npx skills add <your-user>/skills -g --all        # install everywhere
npx skills update -g                              # after pushing changes
```
Private repo: the CLI uses your existing git credentials, `gh` login or SSH.

## The set

| Skill | Modes | Touches code? | Can go live? |
|---|---|---|---|
| `recon` | options (default), explain, cause | no | no |
| `audit` | gaps, consistency, design, leftovers, all | no | no |
| `cost-report` | n/a | no | no |
| `lab` | compare (default), bench | scratch folder only | no |
| `dark-run` | build (default), tidy | yes, on a branch | no |
| `swarm` | plan, work, ladder, wrap-up | yes, lane branches | no |
| `fix-and-ship` | n/a | yes | only after approval |
| `ship` | check, go | no | `go` only after approval |
| `ship-setup` | n/a | writes `SHIPPING.md` after confirmation | no |

## Shared rules
1. The first line of every reply declares the mode: what it will and won't touch.
2. Nothing goes live without an explicit "approved" for that specific change.
3. Shipping skills read the project's `SHIPPING.md` first. If it is missing, they stop and use `ship-setup`.
4. A skill's own limits beat `SHIPPING.md`. A read-only skill never ships, even if the config allows it.
5. If it is unclear whether a message is a command or a question, explain or ask; do not implement.
6. Problems found outside the current scope are reported, not fixed.

## Typical flow
`recon explain` (understand) → `recon` (options) → `fix-and-ship` (approve and release), or `dark-run` → `ship check` → `ship go`.
