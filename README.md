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
OPENROUTER_MODEL_LIST=openai/gpt-oss-120b:free,qwen/qwen3.6-plus,openrouter/auto

HARNESS_OPENROUTER_API_KEY=
HARNESS_OPENROUTER_BASE_URL=https://openrouter.ai/api/v1
HARNESS_OPENROUTER_MODEL=openai/gpt-oss-120b:free
HARNESS_OPENROUTER_MODEL_LIST=openai/gpt-oss-120b:free,qwen/qwen3.6-plus,openrouter/auto
```

For now, OpenRouter is the only callable harness LLM engine. The `OPENAI_*`
keys are local OpenAI-compatible harness target keys, not permission to call
the real OpenAI account from the shared dev environment.

## Wrapper

Use `codexopen.py` or `codexopen.cmd` to launch Codex with the local OpenRouter
target. The wrapper reads this repo's local `.env`, accepts full OpenRouter model
IDs, and disables Codex features that are incompatible with this OpenRouter route.

List available OpenRouter model IDs:

```powershell
codexopen --list-models
```

Launch with an explicit OpenRouter model ID:

```powershell
codexopen --model qwen/qwen3.6-plus
codexopen --model openai/gpt-oss-120b:free
```

The native Codex `/model` command still shows Codex's internal model catalog.
Use `codexopen --list-models` before launch and `codexopen --model <id>` to
select an OpenRouter-hosted model for this harness.
