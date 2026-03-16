---
name: generate-threads-content
description: Generates, brainstorms, edits, and refines Threads posts for a senior enterprise product designer. Use this skill whenever the user wants to write something for Threads, find something to post about, edit a draft, brainstorm post ideas, or get feedback on social content. Also trigger when the user mentions Rivian, design opinions, career takes, or anything they want to share publicly. Even vague signals like "I want to post something about X" or "help me write a Threads post" should trigger this skill.
---

# Threads Content Skill

This skill runs two workflows for creating and refining Threads posts:
- **Workflow 1 — Discovery**: Finding what to post about from a loose signal or nothing at all
- **Workflow 2 — Editing**: Developing a draft or chosen angle into a polished, ready-to-post piece

## Setup — always do this first

Before doing anything else, read both reference files. They govern every step of both workflows:

1. Read `references/VOICE.md` — the voice profile, topic areas, tone, hard rules, and review rubric
2. Read `references/WORKFLOW.md` — the step-by-step instructions for both workflows

Do not generate ideas, write drafts, or give feedback until you've read both files.

## Which workflow to run

- User wants to find something to post → **Workflow 1**
- User has a draft or has picked an angle → **Workflow 2**
- User picked an angle from Workflow 1 → hand directly to **Workflow 2**

## One standing rule

Never show output that hasn't already passed the review rubric in VOICE.md. Generate, critique internally, revise, then present. The user should only ever see work that's already been reviewed.
