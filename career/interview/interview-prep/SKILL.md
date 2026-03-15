---
name: interview-prep
description: "Generates interview prep content for initial recruiter or hiring manager screens and places it directly into the user's Notion job tracker. Creates a company snapshot, 4-5 interview questions to ask, and 2-3 talking points connecting the user's experience to the role. If the company doesn't have a page in the tracker yet, it creates one from the user's template. Use this skill whenever the user mentions preparing for an interview, prepping for a recruiter call, getting ready for a hiring manager screen, or wants questions to ask a company. Also trigger when the user shares a job posting URL, company website link, or recruiter email and wants help preparing. Even casual phrasing like 'I have a call with [company] tomorrow' or 'help me prep for this interview' should trigger this skill."
---

# Interview Prep Skill

Generate a polished interview prep document (.docx) for initial recruiter or hiring manager conversations. The document helps the user walk into every first call feeling prepared, informed, and strategic.

## Inputs

The user will typically provide some combination of:

1. **Company website URLs** — career pages, about pages, blog posts, product pages, or job listings. Fetch each URL with `web_fetch` to pull context about the company's mission, product, stage, and culture.
2. **Recruiter/hiring manager context** — this can come from several places:
   - **Gmail** — proactively search Gmail for relevant emails from the recruiter or company. Search for the company name, recruiter name, or role title. Try queries like `from:recruiter@company.com` or `subject:company-name designer` or simply the company name. Read the full thread to get all context.
   - **LinkedIn messages** — these can't be searched automatically. If the user hasn't pasted a LinkedIn message, ask if there's a LinkedIn message or thread they'd like to paste in. Many recruiter conversations start on LinkedIn, so always ask.
   - **Pasted directly** — the user may paste email or message content into the conversation themselves.
3. **Job description** — sometimes provided as a link or pasted text.

The user may not provide all three every time. Work with whatever they give you. The default behavior when the user provides a company/role should be:
1. Search Gmail for any relevant emails
2. Ask the user: "I found [X] in your email. Was there also a LinkedIn message with any additional context you can paste in?" (or if nothing was found in Gmail: "I didn't find anything in your email — do you have a LinkedIn message or other context you can paste in?")
3. Use `web_search` to fill remaining gaps

## Career Summary (from Notion)

The user keeps a living career summary in Notion. **Always fetch this page at the start of every prep session:**

```
Notion page: "About Me as a Designer"
URL: https://www.notion.so/About-Me-as-a-Designer-720423acad484e8eb807b1623fe4dd78
```

Use the Notion fetch tool to pull the latest version. This page contains:
- Quick pitch and career path
- Design philosophy and values
- Current role and responsibilities
- What they're looking for in a next role
- Strengths and weaknesses
- Growth areas

This is the foundation for generating personalized questions and talking points. Every question and talking point should feel like it could only come from *this specific person* — not generic interview advice.

## Output — Notion Page in Job Tracker

All output goes into the user's **Interviews & Job Applications** database in Notion. No .docx — everything lives where the user already tracks interviews.

### Database details

```
Database: "Interviews & Job Applications"
URL: https://www.notion.so/5f3b3030f852446a86307ad842044900
Data source ID: 14f7256f-62e9-45b9-98d6-5330afc3ad87
Template ID: 06f7faab-2da9-4374-aaad-e31cb8580c25
Template name: "{Company Name} + {Role}"
```

### Step 1: Find or create the page

Search the database for an existing page that matches the company and role. Use `notion-search` with the company name scoped to the database's data source.

**If a page exists:** Use it. Don't create a duplicate.

**If no page exists:** Create one from the template. Set these properties:
- `Opportunity`: "{Company Name}, {Role Title}" (e.g., "Datadog, Senior Design Manager")
- `Status / Stage`: "Scheduled"
- `Company URL`: the company's main URL if known
- `Job Req`: the job listing URL if provided
- `date:Date:start`: today's date
- `Application Type`: "Recruiter" or "Hiring Manager" based on context

Note: When using a template, don't provide `content` — the template fills it in. The template creates Round 1, 2, and 3 sections with Background, My Questions, and Notes subsections.

After creating from template, wait a moment (template application is async), then fetch the page to confirm the content is populated before editing.

### Step 2: Insert prep content into the page

Use `notion-update-page` to insert content into the existing Round 1 structure. The template creates this structure under `# 1️⃣ Round 1`:

**Background section** — Replace the placeholder text "Drop any info from initial messages for context" with:

A **2-column table** (no header row labels needed — just label and value columns) with a compact company snapshot. Include rows for:
- Company name and ticker
- What they do (one line)
- Stage and funding
- Founded (year and founders)
- Headcount and key offices
- Culture (one-line summary)
- Design team context (if discoverable)
- Recent notable moves

Use Notion markdown table syntax:
```
| | |
|---|---|
| **Company** | Acme Corp (NASDAQ: ACME) |
| **What they do** | Cloud platform for ... |
```

After the table, if there's important strategic context (e.g., competitive overlap, domain relevance, something the user should be careful about), add a callout block:
```
::: callout {icon="⚠️" color="yellow_bg"}
**Key context:** [the strategic note here]
:::
```
Only include this callout when there's something genuinely worth flagging — don't force it.

**My Questions section** — Replace the default placeholder questions with 4-5 personalized interview questions. Format each question as a **toggle** (Notion `<details>` block) — the question is the toggle summary, and the signal note is hidden inside. This keeps the page scannable while preserving context when needed.

```
<details>
<summary>The interview question goes here?</summary>

*The signal note explaining why this question matters and what to listen for.*
</details>
```

Each question should:
- Feel **strategic** — show homework on the company
- Feel **authentic** — reflect what the user genuinely cares about (reference their "What I'm Looking For" from the career summary)
- Feel **conversational** — natural to say out loud, not stiff

Ground questions in specifics from company research AND the user's values. Adapt tone:
- **Recruiter screen** → exploratory, culture/team focused
- **Hiring manager screen** → strategic, craft/process focused
- **Unknown** → mix that works for either

**After the questions, add a new "Talking Points" subsection** (`### Talking Points`) with 2-3 bridges connecting the user's experience to the role:

- Lead with the role's need
- Connect to a specific example from their career
- Land on the distinctive value they bring

Keep each to 3-4 sentences — prompts to weave into conversation, not scripts.

## Workflow Summary

1. Fetch the career summary from Notion
2. Fetch any company URLs the user provides (use `web_fetch`)
3. If the user mentions an email from a recruiter/HM, search Gmail for it and read the relevant thread
4. Ask the user if there's a LinkedIn message they can paste in
5. If needed, run `web_search` to fill gaps (funding, team size, recent news)
6. Search the Interviews & Job Applications database for an existing page for this company/role
7. If no page exists, create one from the `{Company Name} + {Role}` template
8. Insert the company snapshot, questions, and talking points into the Round 1 section
9. Share the Notion page link with the user

## Important Reminders

- Always fetch the Notion career summary fresh — the user updates it over time
- Don't generate generic interview questions you'd find on a blog. Every question should be grounded in the intersection of the user's values and this specific company/role
- The talking points should feel like genuine connections, not forced. If there isn't a natural bridge, don't manufacture one — it's better to have 2 strong talking points than 3 weak ones
- If the user provides minimal context (just a company name), do your research to compensate — but flag what you couldn't find so they know where gaps exist
- When creating a page from the template, remember the template populates asynchronously — fetch the page after a brief pause before trying to edit its content
- Don't duplicate pages in the tracker — always search first
- The Round 1 structure from the template has specific sections (Background, My Questions, Notes). Insert content into the right places — don't overwrite the full page or break the Round 2/3 sections
