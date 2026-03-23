---
name: claude-md-builder
description: Generates a CLAUDE.md file for a new project by interviewing the user about their project context and recommending which skills from their personal library to activate. Use this skill whenever the user is starting a new project, opening a new folder in Cursor or Claude Code, mentions needing a CLAUDE.md, or says things like "I'm starting a new project", "help me set up this project", or "which skills should I use for X". Also trigger when the user describes a project goal and asks what Claude should know about it.
---

# CLAUDE.md Builder

Generates a tailored CLAUDE.md file for a new project based on the user's description and their available skill library.

## Skill Library

The library lives at `~/ai-projects/_skills/` and is organized into these packs:

| Pack | Skill | Description |
|------|-------|-------------|
| `career/` | interview-prep | Generates interview prep for recruiter and hiring manager screens — company snapshots, questions to ask, and tailored talking points |
| `content/` | generate-threads-content | Generates, brainstorms, edits, and refines Threads posts |
| `design/` | brand-guidelines | Applies Anthropic's official brand colors and typography to any artifact |
| `design/` | canvas-design | Creates visual art and design compositions as .png and .pdf files using design philosophy |
| `design/` | frontend-design | Creates distinctive, production-grade frontend interfaces with high design quality |
| `design/` | implement-design | Translates Figma designs into production-ready code with 1:1 visual fidelity (requires Figma MCP) |
| `design/` | theme-factory | Applies one of 10 pre-set color/font themes to any artifact, or generates a new theme on-the-fly |
| `portfolio/` | case-study-creation | Collaborative partner for planning, strategizing, and scaffolding design portfolio case studies |

## Workflow

### Step 1 — Interview the user

Ask the user the following. You can ask all at once or conversationally depending on how much they've already shared:

1. **What is this project for?** (e.g. preparing for an interview at Figma, writing a case study for a portfolio review, posting a content series on Threads)
2. **Is there a specific company, role, or audience in mind?**
3. **What's the main thing you want Claude's help with in this project?**
4. **Are there any constraints or context Claude should always keep in mind?** (e.g. tone, timeline, target role level)

Keep the interview short — 4 questions max. If the user has already described the project in enough detail, skip straight to Step 2.

### Step 2 — Read the skill library

Read the available packs and skills from the library table above, then check `~/ai-projects/_skills/` for any skills added since this document was last updated.

Build a mental map of:
- Which pack(s) are relevant to this project
- Which specific skills within those packs apply
- Whether any skills partially apply (worth including with a note)

### Step 3 — Recommend skills

Before generating the file, briefly explain your recommendations:

- Which skills you're including and why
- Any skills you're leaving out and why
- If a relevant skill doesn't exist yet, flag it as a gap

Ask the user to confirm or adjust before generating.

### Step 4 — Generate the CLAUDE.md

Output a complete `CLAUDE.md` file using this template:

---

```markdown
# [Project Name or Description]

## Project Context
[2-3 sentences describing the project, goal, and any key constraints. Written so Claude can orient itself when opening this project.]

## Active Skills
[List each skill with its full local path]
- ~/ai-projects/_skills/[pack]/[skill]/SKILL.md

## Notes for Claude
[Any additional standing instructions specific to this project — tone, priorities, things to always or never do]
```

---

### Step 5 — Deliver

Present the generated file as a code block the user can copy directly into their project folder as `CLAUDE.md`.

Remind them: drop this file at the root of their project folder, and Claude will load it automatically when they open the project in Cursor or Claude Code.
