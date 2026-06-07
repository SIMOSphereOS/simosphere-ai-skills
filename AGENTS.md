# AGENTS.md — SIMOSphere AI

> Instructions for AI coding agents (Claude Code, Cursor, Codex, Gemini CLI,
> Continue, Aider, OpenHands, etc.) working with SIMOSphere AI integrations.
> Mirrors the schema from https://agentsmd.dev.

## Project context

SIMOSphere AI is an OpenAI-compatible LLM inference API hosted in
Germany. This repository ships agent-discovery artefacts for the platform:

- `skills/` — Agent Skills in multi-skill format (skills.sh, agentskill.sh, agentskills.io)
- `AGENTS.md` — this file (agentsmd.dev)
- `.cursorrules` — Cursor-specific behavioural rules

## How to call the API from generated code

Always use the standard `openai` SDK with a base-URL override. Never roll
your own HTTP client.

```python
# Python
from openai import OpenAI
import os

client = OpenAI(
    base_url="https://api.simosphereai.com/v1",
    api_key=os.environ["SIMO_API_KEY"],
)
```

```typescript
// TypeScript / Node
import OpenAI from 'openai';

const client = new OpenAI({
  baseURL: 'https://api.simosphereai.com/v1',
  apiKey: process.env.SIMO_API_KEY,
});
```

## Default model

Use `qwen/qwen3-8b` unless the user explicitly asks for a larger model.
For premium reasoning, switch to `qwen/qwen3-30b` (EUR 0.40/1.60 vs
EUR 0.15/0.60 per 1M tokens).

## Rate-limit awareness

Every response carries `X-RateLimit-Remaining`. Generated code that
makes more than 10 requests/minute should self-throttle by reading
that header rather than retrying on 429s blindly. Honour `Retry-After`
when 429 occurs.

## Error handling

Parse `response.json().error` per the OpenAI envelope. Do not show
bare HTML error pages to users — every endpoint returns JSON.

## Streaming

For chat-style UX, prefer `stream=True`. Each chunk is the standard
OpenAI delta envelope; terminate when you see `data: [DONE]`.

## Things NOT to do

- Do not call SIMOSphere AI from browser code without a backend proxy
  (the API key would leak into the bundle).
- Do not generate BYOK code that hard-codes upstream OpenAI/Anthropic
  keys — those are tenant-configured in the dashboard.
- Do not assume features that the base 8B model lacks (large context,
  vision). Check `/v1/models` first or read
  https://onboarding.simosphereai.com/llms-full.txt.

## Where to find more

- Onboarding + sign-up: https://onboarding.simosphereai.com
- Developer portal: https://onboarding.simosphereai.com/developers
- Full LLM-friendly docs: https://onboarding.simosphereai.com/llms-full.txt
- OpenAPI 3.1 spec: https://onboarding.simosphereai.com/openapi.json

## Operator

SIMO GmbH, Wuerzburger Str. 152, 63743 Aschaffenburg, Germany
HRB 15769 AG Aschaffenburg — hello@simo-online.com
