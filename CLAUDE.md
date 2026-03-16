# _skills — Claude Skills Library

Personal library of reusable Claude skills organized into packs. Each skill is a self-contained prompt with optional reference files that can be activated in any project via CLAUDE.md.

## Repository Structure

```
_skills/
  _meta/          → Meta-skills for managing the library itself
  career/         → Career development skills (interview, performance)
  content/        → Content creation skills (social, writing)
  design/         → Design and visual skills (brand, canvas, frontend, themes)
  portfolio/      → Portfolio and case study skills
  CHANGELOG.md    → Log of all skill changes
  TODO.md         → Active task list
```

## Skill Library Map

| Pack | Skill | Path |
|------|-------|------|
| `_meta` | claude-md-builder | `_meta/claude-md-builder/claude-md-builder-SKILL.md` |
| `_meta` | library-maintenance | `_meta/library-maintenance/library-maintenance-SKILL.md` |
| `career` | interview-prep | `career/interview/interview-prep/SKILL.md` |
| `content` | generate-threads-content | `content/generate-threads-content/SKILL.md` |
| `design` | brand-guidelines | `design/brand-guidelines/SKILL.md` |
| `design` | canvas-design | `design/canvas-design/SKILL.md` |
| `design` | frontend-design | `design/frontend-design/SKILL.md` |
| `design` | implement-design | `design/implement-design/SKILL.md` |
| `design` | theme-factory | `design/theme-factory/SKILL.md` |
| `portfolio` | case-study-creation | `portfolio/case-study-creation/SKILL.md` |

## Conventions

### Folder structure

- Each pack is a top-level directory (`design/`, `content/`, etc.)
- Each skill lives in its own folder inside a pack: `pack/skill-name/SKILL.md`
  - `_meta/` skills use the naming pattern `skill-name-SKILL.md`
  - Some packs use subcategories (e.g. `career/interview/interview-prep/`)
- Reference files go in a `references/` subfolder within the skill directory
- License files (`LICENSE.txt`) and other assets live directly in the skill folder

### SKILL.md frontmatter

Every SKILL.md must include YAML frontmatter with at minimum:

```yaml
---
name: skill-name
description: What this skill does and when to trigger it.
---
```

Optional fields: `license`, `metadata`.

### Descriptions

Descriptions should be rich with natural-language trigger phrases so the skill activates reliably. Include:
- What the skill does
- When to use it
- Example phrases a user might say that should trigger the skill

---

## Workflows — Always Run on Changes

When any skill, pack, or documentation in this repo is added, edited, moved, or removed, run all three workflows below before committing.

### Workflow 1: Validate structure

- [ ] New or edited SKILL.md has valid frontmatter (`name` and `description` are present)
- [ ] Skill folder is inside a valid pack directory (`_meta/`, `career/`, `content/`, `design/`, `portfolio/`)
- [ ] Reference files are inside a `references/` subfolder, not loose in the skill root
- [ ] If a skill was moved between packs, the old location has been cleaned up (no orphaned folders)
- [ ] No empty pack subcategories left behind unless intentionally reserved

### Workflow 2: Update documentation

After validating structure, update all affected documentation:

1. **Pack README** — Update the pack's `[pack]/README.md` with an accurate skills table:

   | Skill | Description | Source |
   |-------|-------------|--------|
   | skill-name | One-line description | original / collected / remixed |

   If the README doesn't exist yet, create it following this format.

2. **CHANGELOG.md** — Append an entry in this format:

   ```
   [YYYY-MM-DD] | [Pack] | [Skill] | [Action] | [Note]
   ```

   Actions: `added`, `updated`, `removed`, `moved`, `remixed`

   If `CHANGELOG.md` doesn't exist yet, create it with a header and the first entry.

3. **claude-md-builder skill library table** — If a skill was added, removed, or moved, update the table in `_meta/claude-md-builder/claude-md-builder-SKILL.md` so it stays accurate.

4. **TODO.md** — If the change completes any task listed in `TODO.md`, mark it done (`[x]`).

### Workflow 3: Pre-commit checklist

Before creating the commit:

- [ ] No `.DS_Store` files are staged
- [ ] All new files are tracked (`git status` shows nothing untracked that should be included)
- [ ] Commit message summarizes what changed and which pack(s) were affected
- [ ] Commit message format: `[pack] action: brief description` (e.g. `[design] add: theme-factory skill`)

---

## Notes for Claude

- Always read a SKILL.md before editing it
- Don't add features or refactor skills beyond what was asked
- When creating new skills, follow the closest existing skill as a template
- Keep descriptions trigger-phrase rich for reliable activation
- When updating the Skill Library Map above, keep it sorted by pack then skill name
- If you're unsure which pack a skill belongs in, ask the user
