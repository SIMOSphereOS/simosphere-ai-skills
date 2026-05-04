# simosphere-ai-skills

> Agent-discovery artefacts for the [SIMOSphere AI](https://onboarding.simosphereai.com)
> inference platform. Companion to the private platform repository.

This repository exists so that AI agents can discover SIMOSphere AI through
public-facing files in the formats most coding-agent ecosystems consume:

- **`SKILL.md`** — Agent Skill (skills.sh, agentskill.sh, agentskills.io)
- **`AGENTS.md`** — Agent-platform integration rules ([agentsmd.dev](https://agentsmd.dev))
- **`.cursorrules`** — Cursor-specific guidance

The platform code itself (gateway, dashboard, onboarding site) is
proprietary and licensed under the Business Source License 1.1. The
files in **this** repository are documentation / metadata only and are
released under the same BSL-1.1 for consistency.

## Install as a Claude Code / OpenHands / Cursor skill

```bash
npx skills add SIMOSphereOS/simosphere-ai-skills
```

## Start using SIMOSphere AI

```bash
curl https://api.simosphereai.com/v1/chat/completions \
  -H "Authorization: Bearer sk-simo-..." \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3-8b",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```

Sign up at <https://onboarding.simosphereai.com/de/register> for an API
key. Trial credits available via `hello@simo-online.com`.

## Documentation

- [Developer portal](https://onboarding.simosphereai.com/developers)
- [API reference + OpenAPI 3.1 spec](https://onboarding.simosphereai.com/openapi.json)
- [LLM-friendly bundle](https://onboarding.simosphereai.com/llms-full.txt)
- [Comparison vs OpenAI / Mistral / Anthropic / HF](https://onboarding.simosphereai.com/compare)
- [Pricing (machine-readable)](https://onboarding.simosphereai.com/pricing.md)

## Operator

SIMO GmbH · Würzburger Str. 152 · 63743 Aschaffenburg · Germany
HRB 15769 AG Aschaffenburg · DPMA 30 2024 240 269

Contact: <hello@simo-online.com>
