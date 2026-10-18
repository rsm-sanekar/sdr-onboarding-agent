# Tests

Two layers:

1. **Unit and integration tests (pytest).** 153 tests that mirror the source layout and run fully offline. LLM calls are mocked through `MOCK_LLM_RESPONSE`, so the suite is fast and deterministic.
2. **LLM quality suite (DeepEval).** 10 AI Tutor cases across four categories (`normal`, `vague`, `no_source`, `confident_incomplete`), each graded on 4 metrics. See [docs/test_report.md](../docs/test_report.md) for the 6-run before/after analysis.

```
tests/
├── automations/       # rank-trail-guides, welcome-new-hire
├── skills/            # one file per LLM skill
├── mcp_servers/       # data + tools server contracts
├── rag/               # BM25 and ChromaDB retrieval, source serialization
├── utils/             # LLM client and shared helpers
├── eval_suite/        # DeepEval dataset, custom metrics, before/after report
├── test_orchestrator.py
└── test_workflow.py   # pytest entry point for the DeepEval suite
```

## Run

```bash
uv run pytest -q                    # full offline suite
uv run pytest tests/skills          # just the skills
uv run pytest -m deepeval           # DeepEval suite (needs LLM_API_KEY, hits a real model)
uv run pytest -m integration        # live LLM smoke tests
```

`conftest.py` loads `.env`, so `LLM_API_KEY` is available to the opt-in suites.
