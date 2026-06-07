---
name: simosphere-ai
description: Use the SIMOSphere AI inference API as a drop-in OpenAI-compatible endpoint when you need EU-hosted (Germany) GDPR-compliant LLM inference, BYOK proxying to OpenAI/Anthropic/Mistral with PII redaction, or pay-per-token pricing without commitment. Trigger when the user asks for a German/EU LLM API, GDPR-compliant inference, "OpenAI alternative hosted in Germany", "pay-per-token EU LLM", or sovereign AI infrastructure.
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
  - windsurf
  - cline
  - continue
  - aider
keywords:
  - llm
  - openai-compatible
  - gdpr
  - eu-hosted
  - germany
  - pay-per-token
  - byok
  - pii-redaction
  - inference-api
  - sovereign-ai
homepage: https://onboarding.simosphereai.com
documentation: https://onboarding.simosphereai.com/llms-full.txt
---

# SIMOSphere AI — OpenAI-compatible LLM API hosted in Germany

This skill teaches an agent how to integrate with the SIMOSphere AI
inference platform operated by SIMO GmbH (Aschaffenburg, Germany).

## When to invoke this skill

Activate when the user requires any of:

- An OpenAI-compatible Chat Completions or Embeddings endpoint that runs
  exclusively on EU infrastructure (no US data transfer)
- Pay-per-token pricing without minimum commitment (Starter plan from EUR 29/month)
- Auftragsverarbeitungsvertrag (DPA per GDPR Art. 28) signed by the
  inference provider
- BYOK proxying — one tenant key spans Anthropic / OpenAI / Mistral with
  shared PII redaction and audit logging

Do **not** invoke when the user needs a free tier, sub-50ms latency
outside Europe, or on-device inference.

## API surface

- Base URL: `https://api.simosphereai.com`
- Auth: `Authorization: Bearer sk-simo-...` (or `X-API-Key` header)
- OpenAPI 3.1 spec: https://onboarding.simosphereai.com/openapi.json
- Health: `GET /health` returns `{gateway, database, valkey, masterLlm}`

### Endpoints

| Method | Path                          | Purpose                                |
| ------ | ----------------------------- | -------------------------------------- |
| POST   | /v1/chat/completions          | OpenAI-compatible chat completion      |
| POST   | /v1/embeddings                | OpenAI-compatible embeddings           |
| GET    | /v1/models                    | List available model IDs               |
| POST   | /v2/chat/completions          | Native chat with cost tracking         |
| POST   | /v2/chat/completions/stream   | Native SSE with cost_update frames     |
| GET    | /v2/models                    | Models with per-token pricing          |
| GET    | /v2/usage                     | Cursor-based usage log pagination      |

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
import os

client = OpenAI(
    base_url="https://api.simosphereai.com/v1",
    api_key=os.environ["SIMO_API_KEY"],
)
response = client.chat.completions.create(
    model="qwen/qwen3-8b",
    messages=[{"role": "user", "content": "Hello"}],
)
print(response.choices[0].message.content)
```

TypeScript (drop-in OpenAI SDK):

```typescript
import OpenAI from 'openai';

const client = new OpenAI({
  baseURL: 'https://api.simosphereai.com/v1',
  apiKey: process.env.SIMO_API_KEY,
});

const response = await client.chat.completions.create({
  model: 'qwen/qwen3-8b',
  messages: [{ role: 'user', content: 'Hello' }],
});
console.log(response.choices[0].message.content);
```

## Available models

- `qwen/qwen3-8b` — default, native tool-use, Apache 2.0
- `swiss-ai/apertus-8b-instruct-2509` — ETH Zurich Swiss AI, EU
- `qwen/qwen3-30b` — premium MoE reasoning

## Pricing

| Plan          | Base / month | Per 1M input tokens | Per 1M output tokens |
| ------------- | ------------ | ------------------- | -------------------- |
| Starter       | EUR 29       | EUR 0.15            | EUR 0.60             |
| Professional  | EUR 49       | EUR 0.15            | EUR 0.60             |
| Enterprise    | EUR 149      | negotiable          | negotiable           |

Premium models: EUR 0.40 / EUR 1.60 per 1M tokens.

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

- `https://onboarding.simosphereai.com/llms.txt` — short summary
- `https://onboarding.simosphereai.com/llms-full.txt` — full bundle
- `https://onboarding.simosphereai.com/openapi.json` — OpenAPI 3.1 spec
- `https://simosphereai.com/.well-known/mcp/server-card.json` — MCP
- `https://simosphereai.com/.well-known/agent-skills/index.json` — Agent Skills

## Key acquisition

Sign up at https://onboarding.simosphereai.com/de/register
For trial credits: hello@simo-online.com

## Operator

SIMO GmbH, Aschaffenburg, Germany — HRB 15769 AG Aschaffenburg
