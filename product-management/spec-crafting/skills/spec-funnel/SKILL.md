---
name: spec-funnel
description: Full specification funnel — takes a product opportunity or problem statement and guides you through EPIC decomposition, user story writing, and acceptance criteria in one structured session.
---

# Spec Funnel

## Overview

A guided session that takes you from raw product opportunity to a complete, ready-to-develop backlog. It runs three phases in sequence — EPIC decomposition → user story writing → acceptance criteria — with validation checkpoints between each phase so you stay in control of the output.

## When to Use

- When starting a new feature from scratch and you need the full spec
- When you have a problem statement, opportunity, or solution idea and want to produce backlog items in one session
- When you want the structure of EPIC/US/AC without having to chain skills manually

## What You Need to Provide

At minimum: a product opportunity, problem statement, or proposed solution. Optionally:
- Target user or persona
- Known constraints or out-of-scope items
- Preferred story format (user stories or job stories) — if not provided, you'll be asked

## Instructions

### Phase 0: Intake

When the user triggers this skill, extract from their input:
- **The goal**: what problem are they solving or what opportunity are they capturing?
- **Known constraints**: anything explicitly out of scope or fixed
- **Story format preference**: user stories or job stories?

If the story format was not specified, ask before proceeding:
> "Would you like user stories or job stories? User stories focus on user roles and goals — job stories focus on context and causality."

Do not proceed to Phase 1 until the story format is confirmed.

---

### Phase 1: EPIC Decomposition

**Goal:** Break the opportunity into 3–8 well-scoped EPICs.

#### 1.1 — Restate the Goal

Summarize the product goal in 1–2 sentences to confirm understanding.

#### 1.2 — Analyze the Scope

In 2–3 sentences, identify:
- The major functional components
- Whether foundation/infrastructure work is needed first
- Whether there are repeated similar components (e.g. multiple integrations, multiple rule groups)

#### 1.3 — Think Before Structuring

Work through these questions before writing EPICs:
- What infrastructure or foundation work must come first?
- Are there repeated similar components that should each get their own EPIC?
- What are the natural testing boundaries?
- Is any proposed EPIC too large to test as a unit? Split it.
- Is any proposed EPIC too small (essentially a user story)? Combine it.

#### 1.4 — Present the EPIC Breakdown

Present 3–8 EPICs in logical implementation order (foundation first, then features). For each EPIC:

**EPIC N: [Clear, descriptive name that conveys the deliverable]**

Rules for good EPICs:
- Separate infrastructure/foundation work from feature-specific work
- Each integration, rule group, or similar component gets its own EPIC
- Each EPIC must have a testable deliverable — even if it doesn't function standalone
- No EPIC should be so large it can't be tested effectively
- No EPIC should be so small it's essentially a user story

#### 1.5 — Rationale and Sequencing

In 2–3 sentences, explain why this breakdown is correct and how each EPIC is independently testable. Call out any dependencies or sequencing constraints.

#### 1.6 — EPIC Validation Gate

After presenting the EPICs, ask:

> "Does this EPIC breakdown look right? You can adjust names, split or merge EPICs, or add/remove any before we move on. Once you confirm, I'll start writing user stories for each EPIC."

Do not proceed to Phase 2 until the user explicitly confirms or adjusts the EPICs.

---

### Phase 2: User Story Writing

**Goal:** Decompose each approved EPIC into 3–12 sprint-sized stories with acceptance criteria.

Process each EPIC one at a time. For each EPIC:

#### 2.1 — Analyze the EPIC

Before writing stories, work through:
- What is the full scope of this EPIC? What are its main functional areas?
- What are the key user journeys or jobs-to-be-done within this EPIC?
- Are there natural groupings (e.g. read flows vs write flows, happy path vs edge cases)?
- Have I covered all functionality — including empty states, errors, and edge cases?

#### 2.2 — Write the Stories

Generate 3–12 stories per EPIC. Each story must:
- Be completable within a single sprint (1–5 days of work)
- Be independently valuable and testable on its own
- Follow INVEST: Independent, Negotiable, Valuable, Estimable, Small, Testable
- Be written in plain language — no technical jargon
- Use the confirmed story format consistently (no mixing user story and job story formats)

#### 2.3 — Story Output Format

```
EPIC N: [EPIC name]

Story N.1: [Short story title]
[Full story in chosen format]

Story N.2: [Short story title]
[Full story in chosen format]

[Continue for all stories in this EPIC...]
```

#### 2.4 — Per-EPIC Validation Gate

After presenting stories for each EPIC, ask:

> "Does this look right for EPIC N? You can adjust, split, or remove stories before I move on to EPIC N+1."

Do not move to the next EPIC until the user confirms. Once all EPICs are confirmed, announce:

> "All EPICs and stories confirmed. I'll now write acceptance criteria for each story, one EPIC at a time."

---

### Phase 3: Acceptance Criteria Writing

**Goal:** Write detailed, Gherkin-syntax acceptance criteria for every confirmed story.

Process each EPIC's stories as a batch. For each story:

#### 3.1 — Understand the Story

Before writing, identify:
- What is the user trying to achieve? (core functionality)
- What EPIC does this belong to? (domain context)
- What user role or situation is involved?
- Are there explicit business rules or constraints?

#### 3.2 — Detect Language

Match the language of all descriptive text to the story's language. Gherkin keywords (`Given`, `When`, `Then`, `And`, `But`) remain in English regardless of story language.

#### 3.3 — Plan Coverage

Think through each dimension before writing:
1. **Happy path** — the main successful flow
2. **Required field validations** — what fields are required, what are the rules?
3. **Boundary conditions** — empty states, maximum lengths, limit values
4. **Error scenarios** — what can go wrong and how should it be surfaced?
5. **Permissions** — who cannot perform this action? What happens when they try?
6. **State transitions** — what changes in the system after the action?
7. **User feedback** — what messages does the user see?

#### 3.4 — Write Scenarios

**Maximum 5 scenarios per story.** If comprehensive coverage would require more than 5, flag the story:

> ⚠️ **Story needs PM review:** This story is too broad for 5 scenarios. Consider splitting it or narrowing its scope before finalizing criteria. Suggested split: [brief suggestion].

Then write the most critical 5 scenarios.

**Each scenario must be:**
- Atomic — one distinct test case per scenario
- Independent — testable without running another scenario first
- Specific — exact values, roles, messages, and states (no vague terms like "works correctly")
- Behavior-focused — describe observable outcomes, not implementation details

**Do not:**
- Reference UI elements as actions (`When I click the save button` → `When I submit the form`)
- Combine multiple test cases into one scenario
- Write criteria that assume implicit knowledge
- Use implementation details (`Then the row is inserted into the database`)

**Scenario order:** happy path first, then validations, then edge cases, then permission/security scenarios.

#### 3.5 — AC Output Format

```
Story N.X: [Story title]

[Full story]

Acceptance Criteria:

Scenario 1: [Clear scenario name — happy path]
Given [precondition]
And [additional precondition if needed]
When [action]
And [additional action if needed]
Then [expected outcome]
And [additional outcome if needed]

Scenario 2: [Validation scenario name]
Given [precondition]
When [action]
Then [expected outcome]
And [error message or state]

[Continue up to 5 scenarios...]

Coverage Summary:
✅ Happy path scenarios: [count]
✅ Validation scenarios: [count]
✅ Edge cases: [count]
✅ Permission / security scenarios: [count — omit line if none]
```

#### 3.6 — Per-EPIC Validation Gate (AC)

After writing criteria for all stories in an EPIC, ask:

> "Acceptance criteria for EPIC N are done. Any adjustments before I move to EPIC N+1?"

Continue until all EPICs are complete.

---

### Phase 4: Final Summary

Once all phases are done, output a final summary:

```
Spec Complete

EPICs: [count]
Stories: [total count across all EPICs]
Stories flagged for PM review: [count — omit if none]

Next steps:
- Review any flagged stories and split or adjust scope
- Import into your backlog tool
- Share with the development team for sizing
```

---

## Gherkin Keywords Reference

| Keyword | Purpose |
|---------|---------|
| `Given` | Precondition or initial state |
| `When` | Action or event that triggers behavior |
| `Then` | Expected outcome or result |
| `And` | Additional condition, action, or outcome (same level as preceding keyword) |
| `But` | Negative or contrasting condition |

---

## Example Usage

```
/spec-funnel We want to build an overtime profile management system. HR admins need to create profiles with multiple rule groups (night hours, bank holidays, weekend overtime) and assign them to employee groups.

/spec-funnel Our expense reporting is manual and error-prone — employees submit paper forms, finance re-enters everything. We want a digital expense submission flow with approval routing.

/spec-funnel [paste a problem statement or opportunity brief]
```
