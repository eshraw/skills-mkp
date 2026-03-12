# agents-skills

A marketplace of Claude Code plugins for product management, design, and engineering workflows.

## Plugins

| Plugin | Category | Description |
|--------|----------|-------------|
| `assumption-audit` | Product Management | Surface hidden assumptions in a feature, decision, or plan |
| `pm-challenge` | Product Management | Challenge feature prioritization — surfaces trade-offs, assumptions, and opportunity costs |
| `design-system-as-text` | Design | Represent your Figma design system as local markdown and CSS files for LLMs |
| `api-design` | Engineering | Design a well-structured API from a desired outcome, with OpenAPI specs and usage examples |

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
claude plugin install assumption-audit
claude plugin install pm-challenge
claude plugin install design-system-as-text
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
