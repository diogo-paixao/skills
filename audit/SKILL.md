---
name: audit
description: Read-only project checks. Use when the user says "audit" or asks whether anything is missing (gaps), whether things are consistent or normalized (consistency), whether the build matches the design (design), or whether leftovers should be cleaned (leftovers). "audit all" runs all four. Reports, never fixes.
---

# audit

One skill, four lenses. Reports findings; does not change anything.

## House rules
- First line of every reply: `Mode: audit <mode> — will: read and report; won't: edit, commit, deploy`.
- Read-only. Fixes are offered as a list the user can approve, never applied.
- Be honest about coverage: end every report with "Not checked" listing what was skipped and why.
- Do not pad. A clean area gets one line, not a paragraph.

## Output format (all modes)
A table: `# | Severity (high/med/low) | Where (file:line or URL) | Finding | Suggested fix`.
Then "Not checked", then a one-line verdict. Keep evidence concrete: quote the line or state the measured value.

## Modes

### gaps: are we missing anything?
- Backlog: is it actually done? Check TODOs, open issues or notes the user points to.
- Easy-to-miss items: head tags (title, description, canonical, Open Graph, favicon), 404 page, sitemap and robots, alt text, lang attribute, env vars documented.
- Test practice: are new behaviours covered? Are tests being skipped or loosened?
- Things that should not ship: console.logs, debug flags, commented-out code, hard-coded URLs or secrets, stray TODOs, large unintended files.

### consistency: are things normalized?
- Design rules: tokens, spacing, type and colour used consistently; no one-off values where a token exists.
- Code: naming, structure, patterns and error handling consistent across the project.
- Docs: updated for the latest changes, or does not need updating (say which).
- Practices: maintainability, duplication, and band-aids (silenced errors, `any`, `// eslint-disable`, retries hiding a real bug).

### design: does the build match the design?
- Compare implementation to the design source the user provides (Figma export, screenshot, spec): spacing, type, colour, states (hover, focus, disabled, empty, error), responsive behaviour.
- If no design source is provided, ask for one; do not guess a reference.

### leftovers: sweep for debris
- Dead code, unused exports and dependencies, unused assets or media sources.
- Leftover logging, commented-out blocks, stale feature flags, orphaned files, large files that should not be committed.

### all
Run the four in order and merge into one report, grouped by severity.
