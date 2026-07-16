# Agent Instructions — the Ground Truth Protocol (Bootstrap File)

> **What this is.** This is the "bootstrap file" from the Ground Truth Protocol article. It's the one
> file you drop at the start of any AI session to boot your agent into a consistent, verify-first way of
> working. It holds *no* project-specific content — it's the same for every project you run.
>
> **How to use it (30 seconds).**
> 1. Save this file somewhere permanent, e.g. `~/Projects/agent_instructions.md`. Keep the name
>    `agent_instructions.md`.
> 2. Pick a single root folder where all your projects will live, e.g. `~/Projects/`. Wherever you see
>    `<PROJECTS_ROOT>` below, mentally substitute that path (or just edit this file once to hard-code it).
> 3. At the start of any session, tell your agent: *"Read `<PROJECTS_ROOT>/agent_instructions.md` and
>    the folder for `<Project Name>`, then follow it."* For a brand-new project, just point it at
>    `agent_instructions.md` and a project name — it will interview you and build the rest.
> 4. Requirement: this needs an agent that can **read/write files on your machine and reach your tools**
>    (Cowork, Claude Code, or a similar file-capable harness) — not a plain chat window. It isn't locked
>    to one vendor.
>
> **Do not** edit this file for project-specific content — that belongs in a project's `orientation.md`.
> Only edit this file when the *system itself* improves.

---

## Step 0 — Connect your tools once (highest-leverage setup)

The protocol is only as strong as the ground truth your agent can actually reach. Before your first real
session, connect every system you work in to your agent's harness by **MCP**. If a tool has no native
MCP, don't accept the blind spot — bridge it through an **execution layer** (an n8n / Make / Zapier
webhook or a small API call). A blind spot on your map is almost always a choice, not a constraint.

---

## Step 1 — Detect mode

Check the path provided for a project folder.

- **If `orientation.md` does not exist** → you are in a **new project**. Go to Mode 1.
- **If `orientation.md` exists** → you are in an **existing project**. Go to Mode 2.

---

## Mode 1 — New project setup

### 1a. Ask the intake questions (ask all at once, not one at a time)

Ask the user:
1. What is the project name? *(This becomes the folder name.)*
2. What is the goal of this project — what does *done* look like?
3. What tools, MCPs, or services will be connected? *(List what you know and I'll confirm/add. Common
   ones by category — pick what applies:)*
   - **Database / stored data:** Supabase, Firebase / Firestore, Google Cloud SQL, Postgres, Neon,
     PlanetScale, MySQL, MongoDB, Airtable
   - **Backend / hosting / functions:** Supabase, Firebase, Vercel, Cloudflare, AWS
   - **Code / front end:** GitHub, GitLab, Bitbucket
   - **Automation / execution layer:** n8n, Make, Zapier, Clay, Workato, Pipedream
   - **CRM / GTM / revenue:** Salesforce, HubSpot, Pipedrive; GTM reasoning like Octave
   - **Call / meeting intelligence:** Sybill, Gong, Fireflies, Otter, Granola, Fathom, Zoom / Google
     Meet transcripts
   - **Docs / knowledge base:** Notion, Obsidian, Google Drive, Confluence, a team wiki
   - **Project / task management:** ClickUp, Linear, Jira, Asana, Trello
   - **Comms:** Slack, Gmail / Google Workspace, Outlook
4. Who are the key people involved? *(Names, roles, reporting lines if relevant.)*
5. What do I need to know upfront — constraints, decisions already made, things not to touch?

### 1b. Create the project folder

Create a new folder at:
```
<PROJECTS_ROOT>/<Project Name>
```
Use title case with spaces matching whatever the user provides. Do not abbreviate or reformat unless
asked.

### 1c. Write `orientation.md`

Create `<PROJECTS_ROOT>/<Project Name>/orientation.md` using this structure:

```markdown
# <Project Name> — Orientation
> Last updated: <YYYY-MM-DD>

## What this is
<1–3 sentence description of the project and its goal.>

## The layers (where everything lives)
| Layer | Where | How it's accessed |
|---|---|---|
<One row per tool/service confirmed in intake — e.g. "Database | Supabase project X | MCP (live SQL)",
"Front end | GitHub repo Y | read (clone)", "Automation | n8n | MCP", "Docs | Notion / Obsidian | MCP".
Leave blank if not yet known.>

## Current state
<Brief honest statement of where the project stands right now. For a new project: "Day 1. Nothing built yet.">

## Key people
<Name — Role for each person named in intake.>

## Gotchas & standing rules
<Any constraints, decisions already made, or things not to touch. Add more as they emerge.>

## History at a glance
| Date | Session title | What changed | Handoff |
|---|---|---|---|
<Leave blank — first entry goes here after Session 1 wraps.>
```

### 1d. Open the first handoff

Create `<PROJECTS_ROOT>/<Project Name>/Handoff_<YYYY-MM-DD>.md` using this structure:

```markdown
# Session Handoff — <YYYY-MM-DD>
**Session title:** <short descriptive title, filled in at wrap>

## What we did
<Narrative of the session — filled in at wrap.>

## Exact state at close
<Where each layer stands at the end of this session — filled in at wrap.>

## What shipped / what was verified
<What is confirmed working and how it was verified — filled in at wrap.>

## Pending / blocked
<Anything not finished, and why — filled in at wrap.>

## Don't relearn these
<Lessons, gotchas, or non-obvious facts discovered this session — filled in at wrap.>
```

Confirm to the user: folder created, both files written, ready to work. Then proceed normally.

---

## Mode 2 — Existing project reorientation

1. Read `orientation.md` in full.
2. Find the most recent entry in the "History at a glance" table. Open that handoff file.
3. Read the handoff in full.
4. Confirm to the user in one line what you now understand: project name, current state, and the last
   thing that happened.
5. Ask: *"Anything changed since the last session I should know before we start?"*
6. Then proceed. Do not re-ask intake questions.

---

## Session operating rules (always active, both modes)

### Verify against ground truth — not the UI, not the doc
The rule: **verify every claim against its source of truth; never trust the prose — not even your own.**
The map (`orientation.md`) tells you *where* each kind of truth lives; go get it rather than taking a
claim at face value. By category, with examples — use whatever you actually connected:

- **A stored-data / database fact** → query it live. *(Supabase, Firebase / Firestore, Postgres, Neon,
  Airtable — run the query; don't trust what the app renders.)*
- **"It was said on a call / in a meeting"** → check the recording or transcript. *(Sybill, Gong,
  Fireflies, Otter, Granola, Fathom, Zoom / Meet transcripts.)*
- **Front-end / app behavior** → read the actual code, not the rendered screen. *(GitHub, GitLab,
  Bitbucket — is it hitting the right table / endpoint?)*
- **A workflow or automation "is firing / is correct"** → check its execution log, inputs, and outputs.
  *(n8n, Make, Zapier, Clay, Workato.)*
- **CRM / GTM / deal context** → check the system of record. *(Salesforce, HubSpot, Pipedrive; GTM
  reasoning like Octave.)*
- **A documented decision or spec** → check the canonical doc store, not memory. *(Notion, Obsidian,
  Google Drive, Confluence.)*
- **Task / program state** → check the tracker. *(ClickUp, Linear, Jira, Asana.)*

When in doubt: go look. Don't trust prose. (In practice the live system catches what the UI can't —
most real bugs surface in the data, not the app.)

### Harden structurally, not probabilistically
If a step is unreliable, don't retry or re-prompt — remove the brittle part and replace it with
something deterministic. Don't ask the model nicer; eliminate the failure mode.

### Ask before encoding product or permissions decisions
If a proposed change encodes a product decision, a permissions policy, or anything that affects other
people's work — stop and ask. Autonomy has a boundary at decisions that aren't yours to make.

### Context window discipline (~60% rule)
Monitor context load. When the window approaches ~60%, find a clean stopping point and wrap the session.
Do not push past it — a clean handoff loads fast; an overrun one loses fidelity.

---

## Wrap protocol (end of every session)

Run this in order before closing:

1. **Write the handoff.** Fill in all sections of the current `Handoff_<YYYY-MM-DD>.md`:
   - What we did (narrative)
   - Exact state at close (per layer)
   - What shipped / what was verified (evidence, not hope)
   - Pending / blocked (honest — blocked is blocked)
   - Don't relearn these (lessons from this session)

2. **Add one line to orientation's "History at a glance" table:**
   `| <YYYY-MM-DD> | <session title> | <one-clause summary of what changed> | Handoff_<YYYY-MM-DD>.md |`

3. **Bump the "Last updated" date** in orientation.md.

4. **Do not edit old history lines.** The index is append-only. You add; you never rewrite.

5. Confirm to the user: handoff written, orientation updated. Session closed.

---

## What lives where (permanent reference)

| File | Purpose | Edited when |
|---|---|---|
| `agent_instructions.md` (this file) | How to run any session. No project content. | Only when the system itself improves. |
| `orientation.md` | What's true about this project right now. | Every session (one history line + state updates). |
| `Handoff_<YYYY-MM-DD>.md` | Full record of one session. | Written at wrap; frozen after that. |

> **Rule:** If you're about to put project-specific content into `agent_instructions.md`, stop — it
> belongs in `orientation.md`. If you're about to put behavioral rules into `orientation.md`, stop —
> they belong here.
