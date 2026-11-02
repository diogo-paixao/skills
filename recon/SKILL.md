---
name: recon
description: Read-only investigation. Use when the user says "recon", wants ideas or options explored for a problem, wants to be walked through an issue before anything changes ("recon explain", "walk me through"), or wants the real cause of a bug ("recon cause"). Never edits, commits or deploys.
---

# recon

Understand first, act never. Recon changes nothing.

## House rules
- First line of every reply: `Mode: recon <mode> — will: read and analyse; won't: edit, commit, deploy`.
- Read-only means read-only: reading code, logs, git history and running non-mutating commands is fine. No edits, no commits, no installs, no deploys.
- If a message sounds like a command but could be a question, treat it as a question.
- Problems found outside the topic are reported, not fixed.

## Modes
Default is **options**. Pick another when the user says so (`recon explain`, `recon cause`) or the request clearly asks for it.

### options (default): explore ideas, document findings
1. Restate the problem in one or two sentences.
2. Explore at least two real approaches. Check the code and, if useful, run small read-only experiments.
3. For each: what it does, gain, trade-off, effort, risk. Use figures when they can be measured; say "estimate" when they can't.
4. If one option has no real downside, say it is the clear pick.
5. Recommend one, and say what would change that recommendation.
6. Write the findings to `docs/recon/<topic>.md` only if the user asks for a file; otherwise reply in chat.
7. End with: "Say `fix-and-ship` (or `dark-run`) on option X to proceed." Do nothing further.

### explain: walk me through it
Used when the user wants context, not a solution.
1. Treat the message as a question, never a command.
2. Explain what is happening and why, in plain terms, with evidence (file and line, commit, observed behaviour).
3. Tie it to recent work: relevant recent commits, decisions and files we have been touching.
4. Surface expectation gaps: where the behaviour differs from what the user likely expected, and where an earlier interpretation or implementation may have diverged from their intent.
5. End with "What I would do if you say go": a short plan. Do not start it.

### cause: find the real cause, no band-aids
1. Reproduce or locate the failure; show the evidence.
2. Trace to the cause, not the first place the symptom appears.
3. Say plainly whether a proposed fix treats the cause or only the symptom.
4. List what else the same cause could be breaking.
5. Stop at the diagnosis. Fixing is a separate, explicit request.
