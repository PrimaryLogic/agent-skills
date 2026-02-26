# Primary Logic Agent Skills

Production-ready [Agent Skills](https://agentskills.io/) for Primary Logic workflows.

These skills help AI agents query Primary Logic's external investment intelligence API safely and consistently, with explicit input/output contracts and reusable references.

## Installation

### Prerequisites

Before installing and using these skills:

1. Log in at [primarylogic.com](https://www.primarylogic.com).
2. Open the Primary Logic dashboard and create an API key from **Settings -> API Keys**.
3. Ensure the API key creator has an active API-tier subscription (user-level entitlement).
4. Keep that key available to set `Authorization: Bearer <PRIMARYLOGIC_API_KEY>` in your agent runtime.

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

### Install from a local checkout (monorepo)

From the Primary Logic monorepo root:

```bash
npx skills add ./external/agent-skills --agent claude-code --skill '*' -y --copy
```

### Verify available skills before install

```bash
npx skills add PrimaryLogic/agent-skills -l
```

## Claude Code Note

This repository is currently distributed as an **Agent Skills** package.
Use the `skills` CLI install commands above.

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
