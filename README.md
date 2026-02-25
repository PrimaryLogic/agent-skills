# Primary Logic Agent Skills

Production-ready [Agent Skills](https://agentskills.io/) for Primary Logic workflows.

These skills help AI agents query Primary Logic's external investment intelligence API safely and consistently, with explicit input/output contracts and reusable references.

## Installation

### Install from GitHub (tested)

```bash
npx skills add PrimaryLogic/agent-skills
```

### Install directly into Claude Code (tested)

```bash
npx skills add PrimaryLogic/agent-skills --agent claude-code --skill '*' -y --copy
```

This installs skills under:

```text
./.claude/skills/
```

### Verify available skills before install

```bash
npx skills add PrimaryLogic/agent-skills -l
```

## Claude Code Plugin Compatibility

This repository follows the Agent Skills standard and is compatible with Claude Code skill installation through the `skills` CLI.

If your Claude build has plugin marketplace commands enabled, you can also add this repo via Claude plugin flows similar to:

```text
/plugin marketplace add PrimaryLogic/agent-skills
```

## Available Skills

### `primary-logic-external-api`

Query the Primary Logic External API (`/v1`) for real-time, continuously refreshed investment
intelligence sourced from numerous monitored channels.

Use this skill when you need:

- ticker-specific bull or bear evidence
- catalyst/risk signal scans
- source coverage diagnostics
- per-content ticker attribution
- API usage and access diagnostics

Primary references included:

- `references/use-cases.md`
- `references/api-recipes.md`
- `references/response-contracts.md`
- `references/validation.md`

## Example Usage Prompts

- `Build a bull and bear case for NVDA from the last 7 days with the highest-impact evidence first.`
- `Show contradictory evidence for MSFT with relevance >= 0.6 and abs impact >= 5.`
- `Check whether my org has source coverage gaps for AMD-related content.`
- `Diagnose why my external API key is not returning ticker signals.`

## Repository Structure

```text
agent-skills/
├── README.md
└── skills/
    └── primary-logic-external-api/
        ├── SKILL.md
        └── references/
            ├── api-recipes.md
            ├── response-contracts.md
            ├── use-cases.md
            └── validation.md
```

## Validation

Validate a skill locally with `skills-ref`:

```bash
skills-ref validate ./skills/primary-logic-external-api
```

Or quickly check repository discoverability:

```bash
npx skills add PrimaryLogic/agent-skills -l
```
