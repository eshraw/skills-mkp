---
name: EPIC-writing
description: Break down a product feature or opportunity into well-structured, testable EPICs following agile best practices.
---

# EPIC Writing

## Overview

An EPIC is a large body of work broken into smaller, testable units. This skill helps you decompose product features into 3–8 EPICs that are logically separated, appropriately sized, and independently testable — even when they depend on other EPICs to function end-to-end.

## When to Use

- When starting a new feature and you need to plan the delivery
- When a feature feels "too big" to ship as one block
- When you need to split work across multiple sprints or teams
- Before writing user stories, to establish the right containers
- When estimating scope for roadmap planning

## Instructions

When the user provides a product feature or opportunity, follow this process:

### Step 1: Restate the Goal

Summarize the product goal in 1–2 sentences to confirm understanding.

### Step 2: Analyze the Scope

In 2–3 sentences, identify:
- The major functional components
- Whether foundation/infrastructure work is needed
- Whether there are repeated similar components (e.g., multiple rule groups, multiple integrations)

### Step 3: Think Before Structuring

Before writing EPICs, work through these questions:
- What infrastructure or foundation work must come first?
- Are there repeated similar components that should each get their own EPIC?
- What are the natural testing boundaries?
- Is any proposed EPIC too large to test as a unit? Split it.
- Is any proposed EPIC too small (essentially a user story)? Combine it.

### Step 4: Break Down into EPICs

Present 3–8 EPICs in logical implementation order (foundation first, then features). For each EPIC:

**EPIC N: [Clear, descriptive name that conveys the deliverable]**

Name EPICs so a developer immediately understands the scope.

Rules for good EPICs:
- Separate infrastructure/foundation work from feature-specific work
- Each integration, rule group, or similar component gets its own EPIC
- Each EPIC must have a testable deliverable — even if it doesn't function standalone
- No EPIC should be so large it can't be tested effectively
- No EPIC should be so small it's essentially a user story

### Step 5: Provide Rationale

In 2–3 sentences, explain:
- Why this breakdown follows best practices
- How each EPIC is independently testable

### Step 6: Implementation Order Notes (if relevant)

Call out any dependencies or sequencing constraints between EPICs.

## Output Format

```
Product Goal: [Restated input]

Analysis:
[2–3 sentences on scope and key components]

EPIC Breakdown:
EPIC 1: [Name]
EPIC 2: [Name]
EPIC 3: [Name]
[...]

Rationale:
[2–3 sentences on why this breakdown is correct]

Implementation Order Notes:
[Any dependency or sequencing notes — omit if not relevant]
```

## Good vs Bad Breakdowns

**Good:** Foundation work (CRUD, backend skeleton, listing pages) is its own EPIC. Similar components (rule groups, integrations) each get their own EPIC. Every EPIC is testable in isolation.

**Bad:** All similar components combined into one EPIC ("all rule groups"). Everything crammed into a single massive EPIC. EPICs so vague the scope is unclear.

## Example Usage

```
/EPIC-writing overtime profiles with 4 rule groups: night hours, bank holidays, weekend overtime, special times
/EPIC-writing multi-currency expense reporting system
/EPIC-writing payroll integrations with ADP, Gusto, and BambooHR
/EPIC-writing employee self-service portal with leave requests, payslip access, and profile management
```
