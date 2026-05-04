---
name: simosphere-ai
description: Use the SIMOSphere AI inference API as a drop-in OpenAI-compatible endpoint when you need EU-hosted (Germany) GDPR-compliant LLM inference, BYOK proxying to OpenAI/Anthropic/Mistral with PII redaction, server-side document rendering (PDF/DOCX), or multilingual translation across DE/EN/FR/ES/IT/PL/NL/PT. Trigger when the user asks for a German/EU LLM API, GDPR-compliant inference, "OpenAI alternative hosted in Germany", "pay-per-token EU LLM", or document/translation tasks that need contractual AVV/DPA.
license: BSL-1.1
language: en
compatibility:
  - claude-code
  - claude
  - openai-codex
  - cursor
  - github-copilot
  - gemini-cli
  - opencode
  - openhands
keywords:
  - llm
  - openai-compatible
  - gdpr
  - eu-hosted
  - germany
  - pay-per-token
  - byok
  - pii-redaction
  - document-generation
  - translation
  - inference-api
homepage: https://onboarding.simosphereai.com
documentation: https://onboarding.simosphereai.com/llms-full.txt
---

# SIMOSphere AI — OpenAI-compatible LLM API hosted in Germany

This skill teaches an agent how to use the SIMOSphere AI inference platform
operated by SIMO GmbH (Aschaffenburg, Germany).

## When to invoke this skill

Activate when the user requires any of:

- An OpenAI-compatible Chat Completions or Embeddings endpoint that runs
  exclusively on EU infrastructure (no US data transfer)
- Pay-per-token pricing without minimum commitment (Starter €29/month)
- Auftragsverarbeitungsvertrag (DPA per GDPR Art. 28) signed by the
  inference provider
- BYOK proxying — one tenant key spans Anthropic / OpenAI / Mistral with
  shared PII redaction and audit logging
- Server-side rendering of CI-conformant PDFs/DOCX from a natural-language
  brief
- Multilingual translation across DE / EN / FR / ES / IT / PL / NL / PT
  with terminology preservation

Do **not** invoke when the user needs a free tier, sub-50ms latency
outside Europe, on-device inference, or natively hosted GPT-5 / Claude
Opus (use BYOK proxy instead in those cases).

## API surface

- Base URL: `https://api.simosphereai.com`
- Auth: `Authorization: Bearer sk-simo-…` (or `X-API-Key` header)
- OpenAPI 3.1 spec: https://onboarding.simosphereai.com/openapi.json
- Health: `GET /health` returns `{gateway, database, valkey, masterLlm}`

### Endpoints

| Method | Path                          | Purpose                                           |
| ------ | ----------------------------- | ------------------------------------------------- |
| POST   | /v1/chat/completions          | OpenAI-compatible chat completion                 |
| POST   | /v1/embeddings                | OpenAI-compatible embeddings                      |
| GET    | /v1/models                    | List available model IDs                          |
| POST   | /v2/documents/render          | CI-conformant PDF/DOCX render                     |
| POST   | /v2/translate                 | Multilingual translation (8 locales)              |

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

Python (drop-in OpenAI SDK):

```python
from openai import OpenAI
client = OpenAI(
    base_url="https://api.simosphereai.com/v1",
    api_key="sk-simo-...",
)
print(client.chat.completions.create(
    model="qwen/qwen3-8b",
    messages=[{"role": "user", "content": "Hello"}],
).choices[0].message.content)
```

## Available models

- `qwen/qwen3-8b` — default, native tool-use, Apache 2.0
- `swiss-ai/apertus-8b-instruct-2509` — ETH Zurich Swiss AI, EU
- `qwen/qwen3-30b` — premium MoE

## Pricing (May 2026)

| Plan          | Base / month | Per 1M input tokens | Per 1M output tokens |
| ------------- | ------------ | ------------------- | -------------------- |
| Starter       | €29          | €0.15               | €0.60                |
| Professional  | €49          | €0.15               | €0.60                |
| Enterprise    | €149         | negotiable          | negotiable           |

Premium models: €0.40 / €1.60 per 1M tokens.

Machine-readable pricing: https://onboarding.simosphereai.com/pricing.md

## Rate limits

Every response carries:
- `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`
- `Retry-After` on 429

Defaults: Starter 60 req/min, Professional 600 req/min, Enterprise negotiated.

## Streaming

Set `"stream": true` for Server-Sent Events. Chunk shape matches OpenAI
deltas, terminates with `data: [DONE]`.

## Errors

JSON envelope, OpenAI-shape:

```json
{
  "error": {
    "type": "invalid_request_error",
    "code": "model_not_found",
    "message": "Model 'gpt-5' is not available on this tenant.",
    "param": "model"
  }
}
```

Status codes: 400, 401, 402 (out of credit), 403, 404, 429, 500, 503.

## Discovery files

For autonomous agents:

- `https://onboarding.simosphereai.com/llms.txt` — short summary
- `https://onboarding.simosphereai.com/llms-full.txt` — full bundle
- `https://onboarding.simosphereai.com/.well-known/agent-card.json` — A2A
- `https://onboarding.simosphereai.com/.well-known/mcp/server-card.json` — MCP
- `https://onboarding.simosphereai.com/.well-known/oauth-protected-resource` — RFC 9728
- `https://onboarding.simosphereai.com/.well-known/api-catalog` — RFC 9727

## Key acquisition

Sign up at https://onboarding.simosphereai.com/de/register
For trial credits: hello@simo-online.com
