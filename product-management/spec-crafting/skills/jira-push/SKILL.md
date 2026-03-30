---
name: jira-push
description: Push a structured backlog (EPICs + user stories + acceptance criteria) to Jira. Creates one EPIC issue per EPIC and one Story sub-issue per user story, then returns links to all created EPICs.
---

# Jira Push

## Prérequis

- A **Jira MCP server** must be configured and connected in your Claude Code environment.
- You must have write access to the target Jira project.

---

## Overview

Takes a structured backlog — EPICs with their user stories and acceptance criteria — and creates the corresponding issues in Jira. Each EPIC becomes a Jira Epic issue; each story becomes a Story sub-issue linked to its parent EPIC.

Use this after `/spec-funnel` (or any other source that produces EPICs and stories), once the spec is fully reviewed and approved.

## When to Use

- After `/spec-funnel` has produced a complete, validated backlog
- When you have a reviewed spec (from any source) and want to populate Jira in one operation
- When manually creating 20+ linked issues would be error-prone or time-consuming

---

## Instructions

### Step 1: Receive the Backlog

Accept the backlog as input. The expected structure is:
- A list of named EPICs
- Each EPIC contains a list of stories
- Each story has a title, full story text, and acceptance criteria

If the input is missing stories or acceptance criteria, use the **AskUserQuestion** tool to ask whether to proceed with partial data or wait for the full spec. Do not proceed until you have an explicit answer.

### Step 2: Collect Missing Jira Details

Before creating anything, check whether the user has provided:

| Field | Required | Notes |
|-------|----------|-------|
| **Project key** | Yes | e.g. `OVT`, `EXP` — the Jira project where issues will be created |
| **Component** (`composant`) | No | Ask if the project uses components and none was specified |
| **Fix Version / Sprint** | No | Ask only if the user mentions a target version or sprint |
| **Assignee** | No | Leave unassigned by default unless specified |

If any required fields are missing, use the **AskUserQuestion** tool to collect them. Ask for all missing required fields in a single call — do not ask field by field. Do not ask for optional fields unless the user has indicated they matter.

### Step 3: Explicit Confirmation Gate

Before creating any Jira issue, use the **AskUserQuestion** tool to present a summary and ask for explicit confirmation:

> **Ready to create in Jira — please confirm**
>
> - Project: `[PROJECT KEY]`
> - Component: `[component name or "none"]`
> - EPICs to create: [count]
> - Stories to create: [total count]
>
> This will create [N] issues in Jira. Confirm? (yes / no)

Do **not** proceed until the user explicitly confirms via AskUserQuestion. If they say no or ask for changes, return to the previous step.

### Step 4: Create EPICs

For each EPIC, create a Jira issue with:
- **Issue type:** Epic
- **Summary:** the EPIC name
- **Description:** a brief restatement of the EPIC's scope (1–2 sentences derived from the backlog context)
- **Project:** as confirmed
- **Component:** as confirmed (if provided)
- **Epic Name field:** same as Summary (required by most Jira configurations for Epic type)

Create EPICs sequentially. Capture the Jira issue key and URL for each created EPIC — you will need these to link stories.

If an EPIC creation fails, stop and report the error before continuing. Do not attempt to create stories for a failed EPIC.

### Step 5: Create Stories as Sub-issues

For each EPIC (in order), create its stories as sub-issues:

For each story, create a Jira issue with:
- **Issue type:** Story
- **Summary:** the story title
- **Description:** the full story text followed by the acceptance criteria, formatted as:

```
[Full story text]

---

Acceptance Criteria:

Scenario 1: [name]
Given ...
When ...
Then ...

Scenario 2: [name]
...
```

- **Parent:** the Jira key of the EPIC this story belongs to (sub-issue link)
- **Project:** same as EPICs
- **Component:** same as EPICs (if provided)

Create all stories for one EPIC before moving to the next.

If a story creation fails, log the failure and continue with remaining stories. Report all failures at the end — do not stop the entire operation for a single story failure.

### Step 6: Return Links

Once all issues are created, output a summary:

```
Backlog created in Jira ✓

EPICs:
- EPIC 1: [EPIC name] → [Jira URL]
- EPIC 2: [EPIC name] → [Jira URL]
- EPIC 3: [EPIC name] → [Jira URL]
[...]

Stories created: [total count]
Stories failed: [count — omit if none]
```

If any stories failed to create, list them by title after the summary so the PM can create them manually.

---

## Error Handling

| Situation | Behavior |
|-----------|----------|
| EPIC creation fails | Stop, report error, do not create stories for that EPIC |
| Story creation fails | Log and continue, report all failures at the end |
| Project key not found | Stop, use AskUserQuestion to ask the user to verify the project key |
| MCP tool unavailable | Stop, remind the user to check their Jira MCP server configuration |
| Partial backlog input | Use AskUserQuestion to ask whether to proceed with partial data or wait |

---

## Example Usage

```
/jira-push [paste spec-funnel output]

/jira-push Project: OVT — [paste backlog]

/jira-push Here's the backlog from our session. Project is EXP, component is "Note de frais".
```
