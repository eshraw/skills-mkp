---
name: prd-writing
description: Generate a structured Product Requirement Document (PRD) using the Eurecia PRD template, then push it to Notion if the MCP is available.
---

# PRD Writing

## Overview

This skill generates a complete PRD following the Eurecia standard template — covering user impact, business impact, objectives, success metrics, key features, out-of-scope, UX notes, and risks. Once the PRD is generated, it can be pushed directly to a Notion page if the Notion MCP is connected, or formatted for manual copy-paste if not.

## When to Use

- When starting a new feature or initiative and you need a structured PRD
- When you want to align stakeholders around scope, objectives, and success metrics before development
- Before writing EPICs (`/EPIC-writing`) or user stories (`/US-writing`)

---

## Instructions

### Step 1: Collect Context

If the user has not provided context, use the **AskUserQuestion** tool to ask for the following in a single call. Frame it as a light intake — the PM does not need perfect answers, rough notes are fine:

> To generate your PRD, I need a few details:
>
> 1. **Feature / initiative name** — what are we building?
> 2. **User impact** — what problem(s) does this solve, and for whom? (qualitative or quantitative data welcome)
> 3. **Business impact** — what business opportunity or risk does this address?
> 4. **Objectives** — what does success look like?
> 5. **Success metrics** — how will we measure success?
> 6. **Key features & scope** — what are the main things to build? Any rough phasing or story mapping?
> 7. **Out of scope** — what are we explicitly NOT building?
> 8. **UX / mockups** — any design notes, Figma links, or UI constraints?
> 9. **Risks** — what could go wrong? Side effects? Mitigation ideas?

If the user has already provided some information in their initial message, only ask for what is missing. Do not ask for fields the user has already covered.

### Step 2: Generate the PRD

Using the collected context, produce a complete PRD in the format below. Write in the same language the PM used (French or English). Be substantive — do not leave sections empty; if the PM did not provide information for a section, write a placeholder that signals what is needed (e.g. *"À compléter — données quantitatives à ajouter"*).

---

```
# Impact utilisateur

[Describe the user problem(s) identified and the target audience(s). Ground this in qualitative and/or quantitative data.]

- [Problem / insight 1]
- [Problem / insight 2]
- [Link to detailed research — à compléter]

---

# Impact Business

[Describe how solving this problem is a business opportunity. Ground this in qualitative and/or quantitative data.]

- [Business driver 1]
- [Business driver 2]

---

# Objectifs

[Describe what success could look like.]

- [Objective 1]
- [Objective 2]

---

# Success Metrics

[Define how success will be measured.]

- [Metric 1]
- [Metric 2]

---

# Key Features & Scope

[Describe the main things to build and the high-level phases (story mapping).]

- [Feature / phase 1]
- [Feature / phase 2]

---

# Out of Scope

[Describe what will NOT be built.]

- [Exclusion 1]
- [Exclusion 2]

---

# UX & Mockups

[Add mockup links, Figma references, or UI constraints.]

- [Link / note 1]

---

# Risques

[What are the potential side effects? Can they be quantified? What should be done if they occur?]

- [Risk 1 — impact / mitigation]
- [Risk 2 — impact / mitigation]
```

---

### Step 3: Check Notion MCP Availability

After generating the PRD, attempt to call the `notion-search` MCP tool with a minimal query (e.g. an empty string or the feature name) to detect whether the Notion MCP is connected.

**If the Notion MCP is available** → proceed to Step 4.

**If the Notion MCP is NOT available** (tool call fails or tool is not listed) → proceed to Step 5.

---

### Step 4: Push to Notion (MCP path)

Use the **AskUserQuestion** tool to ask:

> Your PRD is ready. Which Notion page should I update with this content?
>
> You can provide:
> - A **Notion page URL** (e.g. `https://www.notion.so/...`)
> - Or a **page name** to search for

Once the user provides the target:

1. If a URL was given, use `notion-fetch` with that URL to retrieve the page and confirm its title matches the user's intent.
2. If a name was given, use `notion-search` to find the page. If multiple results come back, use **AskUserQuestion** to ask which one is correct.
3. Use `notion-update-page` to update the page content with the PRD.

After updating, output the Notion page URL so the PM can navigate directly to it.

If any Notion tool call fails, fall back to Step 5 and explain what went wrong.

---

### Step 5: Manual Copy Instructions (no MCP path)

If the Notion MCP is not available, output the following instructions after the PRD:

> **How to add this PRD to Notion**
>
> The Notion MCP is not connected in this environment, so the PRD cannot be pushed automatically. Here's how to do it manually:
>
> 1. Copy the PRD content above (everything between the `---` dividers).
> 2. Open the target Notion page in your browser.
> 3. Click at the top of the page body (below the title).
> 4. Paste the content — Notion will preserve the Markdown headings and bullet points.
> 5. Review and adjust formatting as needed (especially `---` dividers, which become horizontal rules in Notion).
>
> To enable automatic Notion push in the future, connect a Notion MCP server in your Claude Code settings (see: [Notion MCP setup](https://developers.notion.com/docs/mcp)).

---

## Output Format

The final output should contain exactly:

1. The complete PRD (Step 2 format)
2. Either the Notion push confirmation with a link (Step 4), or the manual copy instructions (Step 5)

Do not include intermediate reasoning or commentary between sections.

---

## Example Usage

```
/prd-writing Nouvelle fonctionnalité de gestion des notes de frais multi-devises

/prd-writing Feature: employee self-service leave request portal. Users currently email HR directly — no visibility on balance. Business impact: reduces HR tickets by ~30%. Metrics: ticket volume, adoption rate.

/prd-writing [paste rough notes from a discovery session]
```
