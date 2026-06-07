<div align="center">

# simosphere-ai-skills

**Agent-discovery artefacts for the SIMOSphere AI inference platform.**

[![skills.sh](https://skills.sh/b/SIMOSphereOS/simosphere-ai-skills)](https://skills.sh/b/SIMOSphereOS/simosphere-ai-skills)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

[English](#english) | [Deutsch](#deutsch)

</div>

---

## English

### Overview

Agent skills for [SIMOSphere AI](https://simosphereai.com) -- the OpenAI-compatible inference API hosted in Germany. These skill definitions enable AI coding agents (Cursor, Windsurf, Claude Code, and others) to integrate SIMOSphere AI capabilities directly into their workflows.

Built by [SIMO GmbH](https://simo-online.com). EU-hosted, GDPR-compliant.

### Install

```bash
npx skills add SIMOSphereOS/simosphere-ai-skills
```

### Skills

| Skill | Description |
| ----- | ----------- |
| [simosphere-ai](skills/simosphere-ai/SKILL.md) | Core API integration -- Chat Completions, Embeddings, Models, Streaming |
| [simosphere-openai-migration](skills/simosphere-openai-migration/SKILL.md) | One-line migration from OpenAI, Anthropic, or Mistral to EU-hosted inference |
| [simosphere-eu-compliance](skills/simosphere-eu-compliance/SKILL.md) | GDPR, Schrems II, and EU AI Act compliance evaluation for AI projects |

### Install a Specific Skill

```bash
npx skills add SIMOSphereOS/simosphere-ai-skills --skill simosphere-ai
npx skills add SIMOSphereOS/simosphere-ai-skills --skill simosphere-openai-migration
npx skills add SIMOSphereOS/simosphere-ai-skills --skill simosphere-eu-compliance
```

### Quickstart

```bash
curl https://api.simosphereai.com/v1/chat/completions \
  -H "Authorization: Bearer sk-simo-..." \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3-8b",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```

Sign up at [onboarding.simosphereai.com/de/register](https://onboarding.simosphereai.com/de/register) for an API key. Trial credits available via hello@simo-online.com.

### Documentation

- [Developer Portal](https://onboarding.simosphereai.com/developers)
- [OpenAPI 3.1 Spec](https://onboarding.simosphereai.com/openapi.json)
- [LLM-Friendly Docs](https://onboarding.simosphereai.com/llms-full.txt)
- [Pricing](https://onboarding.simosphereai.com/pricing.md)

### Agent Discovery

- [Agent Skills Index](https://simosphereai.com/.well-known/agent-skills/index.json)
- [MCP Server Card](https://simosphereai.com/.well-known/mcp/server-card.json)
- [llms.txt](https://onboarding.simosphereai.com/llms.txt)

---

## Deutsch

### Ueberblick

Agent-Skills fuer [SIMOSphere AI](https://simosphereai.com) -- die OpenAI-kompatible Inferenz-API mit Hosting in Deutschland. Diese Skill-Definitionen ermoeglichen es KI-gesteuerten Coding-Agenten (Cursor, Windsurf, Claude Code u.a.), SIMOSphere-AI-Funktionen direkt in ihre Arbeitsablaeufe zu integrieren.

Entwickelt von [SIMO GmbH](https://simo-online.com). EU-Hosting, DSGVO-konform.

### Installation

```bash
npx skills add SIMOSphereOS/simosphere-ai-skills
```

### Verfuegbare Skills

| Skill | Beschreibung |
| ----- | ------------ |
| [simosphere-ai](skills/simosphere-ai/SKILL.md) | Kern-API-Integration -- Chat Completions, Embeddings, Modelle, Streaming |
| [simosphere-openai-migration](skills/simosphere-openai-migration/SKILL.md) | Migration von OpenAI, Anthropic oder Mistral zu EU-Inferenz in einer Zeile |
| [simosphere-eu-compliance](skills/simosphere-eu-compliance/SKILL.md) | DSGVO-, Schrems-II- und EU-AI-Act-Konformitaetspruefung fuer KI-Projekte |

### Einzelnen Skill installieren

```bash
npx skills add SIMOSphereOS/simosphere-ai-skills --skill simosphere-ai
npx skills add SIMOSphereOS/simosphere-ai-skills --skill simosphere-openai-migration
npx skills add SIMOSphereOS/simosphere-ai-skills --skill simosphere-eu-compliance
```

### Schnelleinstieg

```bash
curl https://api.simosphereai.com/v1/chat/completions \
  -H "Authorization: Bearer sk-simo-..." \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3-8b",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```

Registrieren Sie sich unter [onboarding.simosphereai.com/de/register](https://onboarding.simosphereai.com/de/register) fuer einen API-Schluessel. Test-Guthaben erhalten Sie ueber hello@simo-online.com.

### Dokumentation

- [Entwicklerportal](https://onboarding.simosphereai.com/developers)
- [OpenAPI-3.1-Spezifikation](https://onboarding.simosphereai.com/openapi.json)
- [LLM-optimierte Dokumentation](https://onboarding.simosphereai.com/llms-full.txt)
- [Preise](https://onboarding.simosphereai.com/pricing.md)

### Agent-Erkennung

- [Agent Skills Index](https://simosphereai.com/.well-known/agent-skills/index.json)
- [MCP Server Card](https://simosphereai.com/.well-known/mcp/server-card.json)
- [llms.txt](https://onboarding.simosphereai.com/llms.txt)

---

## Operator / Betreiber

SIMO GmbH · Wuerzburger Str. 152 · 63743 Aschaffenburg · Germany
HRB 15769 AG Aschaffenburg · DPMA 30 2024 240 269

Contact / Kontakt: hello@simo-online.com
