---
name: AC-writing
description: Write comprehensive, testable acceptance criteria in Gherkin Given-When-Then syntax for user stories or job stories, covering happy paths, validations, edge cases, and permissions.
---

# Acceptance Criteria Writing

## Overview

This skill transforms user stories or job stories into detailed, unambiguous acceptance criteria using Gherkin syntax. Output is ready for QA engineers to translate directly into test cases — no clarification needed.

## When to Use

- After running `/US-writing` to add acceptance criteria to your stories
- When reviewing or completing existing stories that lack criteria
- When a story's current criteria are too vague to be testable
- Before sprint planning, to ensure stories are truly ready

## Gherkin Syntax Rules

**Keywords are always in English:**

| Keyword | Purpose |
|---------|---------|
| `Given` | Precondition or initial state |
| `When` | Action or event that triggers behavior |
| `Then` | Expected outcome or result |
| `And` | Additional condition, action, or outcome (same level as preceding keyword) |
| `But` | Negative or contrasting condition |

**Descriptive text follows the user's language** — detect it from the story itself. If the story is in French, write descriptions in French. If English, in English. Never translate the keywords.

## Instructions

### Step 1: Understand the Story

Before writing anything, identify:
- What is the user trying to achieve? (core functionality)
- What EPIC does this belong to? (domain context)
- What user role or situation is involved?
- Are there any explicit business rules or constraints mentioned?

### Step 2: Detect Language

Read the story text and match the language for all descriptions. Keywords (`Given`, `When`, `Then`, `And`, `But`) remain in English regardless of story language.

### Step 3: Plan Coverage

Think through each of these dimensions before writing scenarios:

1. **Happy path** — the main successful flow
2. **Required field validations** — what fields are required, what are the rules?
3. **Boundary conditions** — empty states, maximum lengths, limit values
4. **Error scenarios** — what can go wrong and how should it be surfaced?
5. **Permissions** — who cannot perform this action? What happens when they try?
6. **State transitions** — what changes in the system after the action?
7. **User feedback** — what messages does the user see?

### Step 4: Write Scenarios

**Maximum 5 scenarios per story.** If comprehensive coverage would require more than 5 scenarios, do not write all of them — instead flag the story:

> ⚠️ **Story needs PM review:** This story is too broad for 5 scenarios. Consider splitting it or narrowing its scope before finalizing criteria. Suggested split: [brief suggestion].

Then write the most critical 5 scenarios you can.

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

### Step 5: Order Scenarios

Always start with the happy path, then validations, then edge cases, then permission/security scenarios.

### Step 6: Write the Coverage Summary

After all scenarios, output a brief coverage summary (see format below).

## Output Format

```
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

If the story requires more than 5 scenarios, add before the coverage summary:

```
⚠️ Story needs PM review: [reason + suggested split or scope change]
```

## Good vs Bad Criteria

**Bad — too vague:**
```
Given the page
When they fill out the form correctly
Then it works
```
Not testable. No user role, no specific action, no concrete outcome.

**Bad — implementation detail:**
```
Given the database connection is established
When the INSERT query executes with valid parameters
Then the row is added to the overtime_profiles table
```
Describes internal mechanics, not observable behavior.

**Bad — combined scenarios:**
```
Given I am logged in
When I submit with a valid name or invalid name or no name
Then I see success or an error
```
Three test cases forced into one. Each must be a separate scenario.

**Good:**
```
Given I am logged in as a HR administrator
And I am on the create overtime profile page
When I enter "Night Shift" as the profile name
And I submit the form
Then a new overtime profile is created with the name "Night Shift"
And I see a success message "Overtime profile created successfully"
```
Specific role, explicit action, concrete outcome. Directly testable.

## Example Usage

```
/CA-writing As a HR administrator, I want to create a new overtime profile with a name and description, so that I can start configuring overtime rules for different employee groups.

/CA-writing [paste a story from /US-writing output]

/CA-writing En tant qu'administrateur RH, je veux archiver un profil d'heures supplémentaires, afin qu'il ne soit plus proposé à la configuration.
```
