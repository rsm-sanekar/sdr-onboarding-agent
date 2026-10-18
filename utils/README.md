# Utils

| Module | Purpose |
|---|---|
| `connect.py` | `ask()` and `ask_json()` for every LLM call, against any OpenAI-compatible gateway (`LLM_API_BASE`, `LLM_API_KEY`). `ask_json()` validates against a pydantic schema and strips stray code fences. Model choice is one argument. |
| `oauth_gpt.py` | Optional route that uses a ChatGPT/Codex OAuth login instead of an API key (`model="oauth-gpt"`). |
| `sdr_common.py` | Shared step infrastructure: the standard CLI parser, envelope builders, error envelopes, per-run working directories, idempotency checks, and the `needs_human_review()` confidence threshold. |
| `transcribe.py` | Local audio transcription for Coaching Notes (Apple Silicon, opt-in via `uv sync --group audio`). |

```python
from utils.connect import ask, ask_json

reply = ask("Explain MEDDIC in one sentence.")
plan = ask_json(prompt, schema=OnboardingPlan, model="claude-sonnet-4-6")
```
