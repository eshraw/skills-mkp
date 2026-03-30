---
name: US-writing
description: Decompose an EPIC into well-structured, sprint-sized user stories or job stories, each with detailed Given-When-Then acceptance criteria.
---

# User Story Writing

## Overview

This skill takes one or more EPICs and produces a ready-to-use backlog: properly sized stories in your chosen format (user stories or job stories), each accompanied by detailed, testable acceptance criteria.

## When to Use

- After running `/EPIC-writing` to break a feature into EPICs
- When you need to populate a sprint backlog
- When refining an EPIC before development starts
- When stories need acceptance criteria written or reviewed

## Story Formats

**User Story** — focuses on user roles and desired outcomes.
> As a [type of user], I want [goal] so that [benefit].

Best for: feature-driven work where user roles are clear and distinct.

**Job Story** — focuses on context and causality rather than user type.
> When [situation], I want to [motivation], so I can [expected outcome].

Best for: behavior-driven work where context matters more than who the user is.

## Instructions

### Step 1: Clarify Format

If the user has not specified a format, ask:
> "Would you like user stories or job stories for this EPIC?"

Do not proceed until the format is confirmed.

### Step 2: Analyze the EPIC

Before writing stories, work through these questions:
- What is the full scope of this EPIC? What are its main functional areas?
- What are the key user journeys or job-to-be-done within this EPIC?
- Are there natural groupings (e.g., read flows vs write flows, happy path vs edge cases)?
- Have I covered all functionality — including empty states, errors, and edge cases?

### Step 3: Write the Stories

Generate 3–12 stories per EPIC depending on complexity. Each story must:

- Be completable within a single sprint (1–5 days of work)
- Be independently valuable and testable on its own
- Follow INVEST: Independent, Negotiable, Valuable, Estimable, Small, Testable
- Be written in plain language — no technical jargon

**Too large (epic-sized):** "As an HR admin, I want to manage all overtime profiles including creating, editing, deleting, and configuring all rule groups." → Split it.

**Too small (task-sized):** "As an HR admin, I want the create button to be blue." → Not a story, it's an implementation detail. Combine or remove.

Do not mix user story and job story formats in the same output without explicit user consent.

### Step 4: Write Acceptance Criteria for Each Story

For every story, generate detailed acceptance criteria using **Given-When-Then** scenarios. Each story should have:

**Functional scenarios** (happy path):
- Given [initial context], When [action], Then [expected result]

**Edge cases and error states:**
- Given [error condition], When [action], Then [expected error behavior]

**Business rules** (if applicable):
- Specific constraints, validations, or thresholds that must hold

Criteria must be specific and testable — a QA engineer should be able to write a test from them without asking for clarification. Criteria must match the story's scope: don't add criteria for out-of-scope functionality.

### Step 5: Handle Multiple EPICs

When multiple EPICs are provided:
- Generate stories for each EPIC separately, clearly labeled
- Pause after each EPIC and ask the user to validate before moving to the next
- Do not batch all EPICs in one pass without checkpoints

### Step 6: Final Review

Before presenting output:
- Is every story properly sized?
- Does every story have acceptance criteria?
- Is the output ready for a development team to use immediately?

## Output Format

```
EPIC: [EPIC name]

Story Format: [User Stories / Job Stories]

---

Story 1: [Short story title]

[Full story in chosen format]

Acceptance Criteria:
- Given [...], When [...], Then [...]
- Given [...], When [...], Then [...]
- [Additional scenarios as needed]

---

Story 2: [Short story title]

[Full story in chosen format]

Acceptance Criteria:
- Given [...], When [...], Then [...]
- [...]

---

[Continue for all stories...]

Summary:
- Total Stories: [number]
- EPIC(s) Covered: [list]
- Estimated Complexity: [Low / Medium / High based on story count and scope]
```

## Example Usage

```
/US-writing EPIC: Overtime profile listing, backend and skeleton detail page + CRUD
/US-writing EPIC: Multi-currency expense entry form — use job stories
/US-writing [paste EPIC breakdown from /EPIC-writing output]
```
