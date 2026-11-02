---
name: lab
description: Test ideas and show the data. Use when the user says "lab" or wants experiments compared side by side (e.g. video conversion settings) with metrics and an explanation of what changed and why. "lab bench" compares before/after against a budget (bundle size, load time, Lighthouse).
---

# lab

Experiments, with evidence the user can see. The project's real code and production are not touched.

## House rules
- First line of every reply: `Mode: lab <mode> — will: run experiments in a scratch folder; won't: change project source, commit, or deploy`.
- Work in a scratch folder (default `.lab/<topic>/`). If it is not gitignored, say so and propose the ignore line; do not edit `.gitignore` without asking.
- Never overwrite originals. Inputs are copied or read-only.
- Report what was measured and how. Mark estimates as estimates. Note if a result is a single run.

## Modes

### compare (default): variants side by side
1. State the question ("which encode keeps quality at the smallest size?") and the variants to test.
2. Run each variant on the same input with the same method. Keep the exact commands/settings.
3. Build a **playground**: a single self-contained `index.html` in the scratch folder showing the outputs side by side (video, image, audio, or rendered result) with a metrics table underneath (size, time, quality metric, anything relevant).
4. Add a "What changed and why" section: for each variant, what setting differed and why it caused the difference in the numbers.
5. Reply with the headline result, the one-line recommendation, and how to open the playground. Do not apply the winner to the project.

### bench: before/after against a budget
1. Ask for or infer the budget (bundle size, load time, Lighthouse score). State the assumption if inferred.
2. Measure the baseline before any change. Use several runs when noise is likely and report the spread.
3. Measure after the change on the same setup.
4. Report a table: metric, before, after, delta, budget, pass or fail.
5. Say plainly whether the change regressed anything. Do not ship or commit the change.
