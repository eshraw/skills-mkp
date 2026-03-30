# agents-skills

A marketplace of Claude Code plugins for product management, design, and engineering workflows.

## Plugins

### Product Management

#### pm-coach

| Plugin | Description |
|--------|-------------|
| `assumption-audit` | Surface hidden assumptions in a feature, decision, or plan |
| `pm-challenge` | Challenge feature prioritization — surfaces trade-offs, assumptions, and opportunity costs |
| `sparring-partner` | Conversational PM coaching mode — challenges your thinking and surfaces blind spots through questions, not answers |

#### spec-crafting

| Plugin | Description |
|--------|-------------|
| `EPIC-writing` | Break down a product feature or opportunity into well-structured, testable EPICs |
| `US-writing` | Decompose an EPIC into sprint-sized user stories with Given-When-Then acceptance criteria |
| `AC-writing` | Write comprehensive, testable acceptance criteria in Gherkin syntax for user stories |
| `spec-funnel` | Full specification funnel — EPIC decomposition → user stories → acceptance criteria in one session |
| `jira-push` | Push a structured backlog (EPICs + user stories + ACs) to Jira |
| `prd-writing` | Generate a structured PRD and optionally push it to Notion |

### Design

| Plugin | Description |
|--------|-------------|
| `design-system-as-text` | Represent your Figma design system as local markdown and CSS files for LLMs |

### Engineering

| Plugin | Description |
|--------|-------------|
| `api-design` | Design a well-structured API from a desired outcome, with OpenAPI specs and usage examples |

## Installation

### 1. Add this marketplace

```bash
claude plugin marketplace add eshraw/skills-mkp
```

### 2. Install a plugin

```bash
claude plugin install <plugin-name>
```

For example:

```bash
# PM coaching
claude plugin install assumption-audit
claude plugin install pm-challenge
claude plugin install sparring-partner

# Spec crafting
claude plugin install spec-funnel
claude plugin install EPIC-writing
claude plugin install US-writing
claude plugin install AC-writing
claude plugin install jira-push
claude plugin install prd-writing

# Design
claude plugin install design-system-as-text

# Engineering
claude plugin install api-design
```

### Install from a specific marketplace

If you have multiple marketplaces configured, use the `@marketplace` syntax:

```bash
claude plugin install assumption-audit@skills-mkp
```

### Manage plugins

```bash
# List installed plugins
claude plugin list

# Update a plugin
claude plugin update <plugin-name>

# Disable a plugin
claude plugin disable <plugin-name>

# Uninstall a plugin
claude plugin uninstall <plugin-name>
```

## Notes

- `design-system-as-text` requires the [Figma MCP server](https://www.figma.com/developers/mcp) to be connected for the `/initialize-ds` and `/update-ds` skills. The `/ds` search skill works without it.
- `jira-push` requires the Atlassian MCP server to be connected.
- `prd-writing` works standalone but can push to Notion if the Notion MCP server is connected.
