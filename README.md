# codex-os-harness

Thin local harness repo for Codex Open Source. Wrapper implementation now lives
in the canonical `C:\Users\keith\dev\cli-harness` checkout; files in this repo
are compatibility shims for older paths.

## Local Environment

This repo must use its own ignored `.env`. Do not rely on `C:\Users\keith\dev\.env`
for harness routing because that shared file can contain real OpenAI credentials.

Expected local keys:

```dotenv
OPENROUTER_API_KEY=
OPENROUTER_BASE_URL=https://openrouter.ai/api/v1
OPENROUTER_MODEL=openai/gpt-oss-120b:free
OPENROUTER_MODEL_LIST=openai/gpt-oss-120b:free,qwen/qwen3.6-plus,openrouter/auto

HARNESS_OPENROUTER_API_KEY=
HARNESS_OPENROUTER_BASE_URL=https://openrouter.ai/api/v1
HARNESS_OPENROUTER_MODEL=openai/gpt-oss-120b:free
HARNESS_OPENROUTER_MODEL_LIST=openai/gpt-oss-120b:free,qwen/qwen3.6-plus,openrouter/auto
```

For now, OpenRouter is the only callable harness LLM engine. Do not put
`OPENAI_MODEL` or `OPENAI_BASE_URL` in the shared `C:\Users\keith\dev\.env`;
use the local harness `.env` keys above or process-scoped overrides.

## Wrapper

Use `C:\Users\keith\dev\cli-harness\codex-os.cmd` for new launches. The legacy
`codexopen.py` and `codexopen.cmd` files in this repo forward to that canonical
wrapper and accept the same options.

List available OpenRouter model IDs:

```powershell
codex-os --list-models
```

Launch with an explicit OpenRouter model ID:

```powershell
codex-os --model qwen/qwen3.6-plus
codex-os --model openai/gpt-oss-120b:free
```

The native Codex `/model` command still shows Codex's internal model catalog.
Use `codex-os --list-models` before launch and `codex-os --model <id>` to
select an OpenRouter-hosted model for this harness.
