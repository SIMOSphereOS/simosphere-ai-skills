---
name: simosphere-openai-migration
description: Migrate existing OpenAI, Anthropic, or Mistral API integrations to SIMOSphere AI with a single line change. Use when the user wants to switch from OpenAI to an EU-hosted provider, needs to make their AI integration GDPR-compliant, asks about OpenAI alternatives in Europe, or wants to proxy multiple LLM providers through one API key.
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
  - migration
  - openai-alternative
  - drop-in-replacement
  - gdpr-migration
  - eu-ai
  - provider-switch
  - byok
homepage: https://onboarding.simosphereai.com
documentation: https://onboarding.simosphereai.com/llms-full.txt
---

# Migrate from OpenAI / Anthropic / Mistral to SIMOSphere AI

SIMOSphere AI is a wire-compatible OpenAI replacement. Existing code that
uses the OpenAI SDK works with a one-line base URL change — no request or
response format modifications required.

## When to invoke this skill

Activate when the user:

- Asks to switch from OpenAI, Anthropic, or Mistral to an EU-hosted provider
- Needs to make an existing LLM integration GDPR-compliant without rewriting code
- Wants a single API key that proxies to multiple upstream providers (BYOK)
- Mentions "OpenAI alternative in Europe" or "sovereign AI"

Do **not** invoke for greenfield projects — use the `simosphere-ai` skill instead.

## Migration steps

### Step 1 — Change the base URL

**Python (before):**

```python
from openai import OpenAI
client = OpenAI()  # uses api.openai.com
```

**Python (after):**

```python
from openai import OpenAI
import os

client = OpenAI(
    base_url="https://api.simosphereai.com/v1",
    api_key=os.environ["SIMO_API_KEY"],
)
```

**TypeScript (before):**

```typescript
import OpenAI from 'openai';
const client = new OpenAI();
```

**TypeScript (after):**

```typescript
import OpenAI from 'openai';

const client = new OpenAI({
  baseURL: 'https://api.simosphereai.com/v1',
  apiKey: process.env.SIMO_API_KEY,
});
```

**curl (before):**

```bash
curl https://api.openai.com/v1/chat/completions \
  -H "Authorization: Bearer sk-..."
```

**curl (after):**

```bash
curl https://api.simosphereai.com/v1/chat/completions \
  -H "Authorization: Bearer sk-simo-..."
```

### Step 2 — Map models

| OpenAI model           | SIMOSphere equivalent              | Notes                          |
| ---------------------- | ---------------------------------- | ------------------------------ |
| gpt-4o-mini            | qwen/qwen3-8b                     | Default, best price/perf ratio |
| gpt-4o                 | qwen/qwen3-30b                    | Premium MoE reasoning          |
| text-embedding-3-small | (use /v1/embeddings with qwen3-8b) | Embedding support via proxy    |

List all available models: `GET https://api.simosphereai.com/v1/models`

### Step 3 — Update environment variables

Replace your OpenAI key with a SIMOSphere key:

```bash
# .env (before)
OPENAI_API_KEY=sk-proj-...

# .env (after)
SIMO_API_KEY=sk-simo-...
```

### Step 4 — Verify

```bash
curl -s https://api.simosphereai.com/health | jq .
```

Expected: `{"gateway":"ok","database":"ok","valkey":"ok","masterLlm":"ok"}`

## What stays the same

- Request format (messages array, model, temperature, stream, tools)
- Response format (choices array, usage object, finish_reason)
- SSE streaming (`data: [DONE]` terminator)
- Error envelope shape (`error.type`, `error.code`, `error.message`)
- Rate limit headers (`X-RateLimit-Remaining`, `Retry-After`)

## What changes

- API key prefix: `sk-simo-...` instead of `sk-proj-...`
- Model IDs: `qwen/qwen3-8b` instead of `gpt-4o-mini`
- Data residency: EU-only (Germany), no US data transfer
- Billing: EUR per-token, no annual commitment required
- DPA: Auftragsverarbeitungsvertrag per GDPR Art. 28 included

## BYOK mode

If the user needs to keep calling upstream OpenAI or Anthropic models but
wants PII redaction and unified audit logging, configure BYOK in the
SIMOSphere dashboard. The tenant key then proxies to the upstream provider
with automatic PII stripping.

## Get started

Sign up: https://onboarding.simosphereai.com/de/register
Trial credits: hello@simo-online.com
Full docs: https://onboarding.simosphereai.com/llms-full.txt
