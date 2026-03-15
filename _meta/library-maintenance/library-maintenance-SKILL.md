---
name: library-maintenance
description: Updates the skills library documentation whenever changes are made — auto-generates pack README updates and appends a changelog entry based on what the user describes. Use this skill whenever the user says they've added, updated, remixed, or removed a skill, mentions making changes to their claude-skills library, says things like "I just added a skill", "I updated the interview pack", "I collected this skill from someone", or "help me document this change". Also trigger when the user shares a new SKILL.md and wants to log it properly.
---

# Library Maintenance

Keeps the skills library documentation up to date by auto-generating README updates and changelog entries based on what the user tells you changed.

## Workflow

### Step 1 — Gather the change details

Ask the user (or extract from what they've already shared):

1. **What changed?** (added a new skill / updated an existing skill / remixed a skill from someone else / removed a skill)
2. **Which pack does it belong to?** (career / design / portfolio / content / other)
3. **What is the skill called?** (folder name)
4. **One-line description** — what does it do?
5. **Source** — is this original, collected from someone else, or remixed? If collected or remixed, who/where from?
6. **Any notes worth capturing?** (e.g. what you changed in a remix, why you removed something)

If the user has already provided enough detail, skip straight to generating the updates.

### Step 2 — Generate the README update

Read the current pack README at `~/ai-projects/_skills/[pack]/README.md`.

Generate an updated skills table with the new entry added (or existing entry modified/removed). Present it clearly so the user can see exactly what changed.

Format for the skills table:

| Skill | Description | Source |
|-------|-------------|--------|
| skill-name | One-line description | Original / Collected (credit) / Remixed (credit) |

### Step 3 — Generate the changelog entry

Append a new entry to `~/ai-projects/_skills/CHANGELOG.md` at the top of the changelog section.

Format:
```
[YYYY-MM-DD] | [Pack] | [Skill] | [added/updated/remixed/removed] | [Brief note]
```

Use today's date. Keep the note to one sentence — just enough context to understand the change later.

### Step 4 — Deliver both updates

Present both outputs clearly:

1. **Updated README table** — the full updated table they can paste into the pack README
2. **Changelog entry** — the single line to prepend to CHANGELOG.md

Remind the user to:
- Paste the README table into `~/ai-projects/_skills/[pack]/README.md`
- Prepend the changelog entry under `## Changelog` in `~/ai-projects/_skills/CHANGELOG.md`
- Update the skill library table in `~/ai-projects/_skills/_meta/claude-md-builder/SKILL.md` to reflect the change
- Then commit and push: `git add . && git commit -m "[change summary]" && git push`
