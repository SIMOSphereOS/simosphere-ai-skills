# simosphere-ai-skills

[![skills.sh](https://skills.sh/b/SIMOSphereOS/simosphere-ai-skills)](https://skills.sh/SIMOSphereOS/simosphere-ai-skills)

Agent skills for [SIMOSphere AI](https://simosphereai.com) — the OpenAI-compatible
inference API hosted in Germany.

## Install

```bash
npx skills add SIMOSphereOS/simosphere-ai-skills
```

## Skills

| Skill | Description |
| ----- | ----------- |
| [simosphere-ai](skills/simosphere-ai/SKILL.md) | Core API integration — Chat Completions, Embeddings, Models, Streaming |
| [simosphere-openai-migration](skills/simosphere-openai-migration/SKILL.md) | One-line migration from OpenAI, Anthropic, or Mistral to EU-hosted inference |
| [simosphere-eu-compliance](skills/simosphere-eu-compliance/SKILL.md) | GDPR, Schrems II, and EU AI Act compliance evaluation for AI projects |

## Install a specific skill

```bash
npx skills add SIMOSphereOS/simosphere-ai-skills --skill simosphere-ai
npx skills add SIMOSphereOS/simosphere-ai-skills --skill simosphere-openai-migration
npx skills add SIMOSphereOS/simosphere-ai-skills --skill simosphere-eu-compliance
```

## Quickstart

```bash
curl https://api.simosphereai.com/v1/chat/completions \
  -H "Authorization: Bearer sk-simo-..." \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3-8b",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```

Sign up at https://onboarding.simosphereai.com/de/register for an API
key. Trial credits available via hello@simo-online.com.

## Documentation

- [Developer portal](https://onboarding.simosphereai.com/developers)
- [OpenAPI 3.1 spec](https://onboarding.simosphereai.com/openapi.json)
- [LLM-friendly docs](https://onboarding.simosphereai.com/llms-full.txt)
- [Pricing](https://onboarding.simosphereai.com/pricing.md)

## Agent discovery

- [Agent Skills Index](https://simosphereai.com/.well-known/agent-skills/index.json)
- [MCP Server Card](https://simosphereai.com/.well-known/mcp/server-card.json)
- [llms.txt](https://onboarding.simosphereai.com/llms.txt)

## Operator

SIMO GmbH · Wuerzburger Str. 152 · 63743 Aschaffenburg · Germany
HRB 15769 AG Aschaffenburg · DPMA 30 2024 240 269

Contact: hello@simo-online.com
