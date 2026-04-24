# codex-os-harness

Thin local harness wrapper for launching Codex Open Source against the approved
OpenAI-compatible harness target.

## Local Environment

This repo must use its own ignored `.env`. Do not rely on `C:\Users\keith\dev\.env`
for harness routing because that shared file can contain real OpenAI credentials.

Expected local keys:

```dotenv
OPENAI_API_KEY=
OPENAI_BASE_URL=https://openrouter.ai/api/v1
OPENAI_MODEL=openai/gpt-oss-120b:free

OPENROUTER_API_KEY=
OPENROUTER_BASE_URL=https://openrouter.ai/api/v1
OPENROUTER_MODEL=openai/gpt-oss-120b:free

HARNESS_OPENROUTER_API_KEY=
HARNESS_OPENROUTER_BASE_URL=https://openrouter.ai/api/v1
HARNESS_OPENROUTER_MODEL=openai/gpt-oss-120b:free
```

For now, OpenRouter is the only callable harness LLM engine. The `OPENAI_*`
keys are local OpenAI-compatible harness target keys, not permission to call
the real OpenAI account from the shared dev environment.

## Wrapper

Use `codexopen.py` or `codexopen.cmd` to launch Codex with the local OpenRouter
target. The wrapper reads this repo's local `.env`, locks the configured model,
and disables Codex features that are incompatible with this OpenRouter route.
