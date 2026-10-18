# Scripts

| Script | Purpose |
|---|---|
| `orchestrator.py` | CLI driver for the 3-step pre-boarding chain. Runs each step as a subprocess with a shared `workflow_run_id`, parses the JSON envelope, follows `next_action`, and stops on `done`, an error, or a step that needs review. |
| `scrape_salesforce_kb.py` | Pulls the public Wikipedia reference pages into `rag/knowledge_base/scraped/` as Markdown. |

```bash
uv run python scripts/orchestrator.py --hire-id HIRE-001
```

For an offline run, set `MOCK_LLM_RESPONSE` first; every subprocess inherits it. The same chain is exposed over HTTP by [`../workflow_server.py`](../workflow_server.py), which is what the UI calls.
