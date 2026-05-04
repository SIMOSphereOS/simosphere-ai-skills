# AGENTS.md — SIMOSphere AI

> Instructions for AI coding agents (Claude Code, Cursor, Codex, Gemini CLI,
> Continue, Aider, OpenHands, etc.) working with SIMOSphere AI integrations.
> Mirrors the schema from https://agentsmd.dev.

## Project context

SIMOSphere AI is an OpenAI-compatible LLM inference API hosted in
Germany. The platform code (gateway, dashboard, onboarding site) lives
in the private SIMOSphereOS/simosphere-ai-api-platform repository under
the Business Source License 1.1.

This public repository ships agent-discovery artefacts only:
- `SKILL.md` — Agent Skill format (skills.sh, agentskill.sh, agentskills.io)
- `AGENTS.md` — this file
- `.cursorrules` — Cursor-specific behavioural rules

## How to call the API from generated code

Always use the standard `openai` SDK with a base-URL override. Never roll
your own HTTP client.

```python
# Python
from openai import OpenAI
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
For premium reasoning, switch to `qwen/qwen3-30b` (€0.40/€1.60 per 1M
tokens vs €0.15/€0.60 for the 8B).

## Rate-limit awareness

Every response carries `X-RateLimit-Remaining`. Generated code that
makes more than ~10 requests/minute should self-throttle by reading
that header rather than retrying on 429s blindly. Honour `Retry-After`
when 429 occurs.

## Error handling

Parse `response.json().error` per the OpenAI envelope. Do not show
bare HTML error pages to users — every endpoint returns JSON.

## Streaming

For chat-style UX, prefer `stream=True`. Each chunk is the standard
OpenAI delta envelope; terminate when you see `data: [DONE]`.

## Where to find more

- Onboarding + sign-up: https://onboarding.simosphereai.com
- Developer portal: https://onboarding.simosphereai.com/developers
- Full LLM-friendly docs: https://onboarding.simosphereai.com/llms-full.txt
- OpenAPI 3.1 spec: https://onboarding.simosphereai.com/openapi.json
- Comparison with OpenAI/Mistral/Anthropic/HF: https://onboarding.simosphereai.com/compare

## Operator contact

- SIMO GmbH, Würzburger Str. 152, 63743 Aschaffenburg, Germany
- HRB 15769 AG Aschaffenburg
- hello@simo-online.com
