# Automations

Deterministic steps with no LLM call. They use the same CLI flags and JSON envelope as the skills, so the orchestrator runs every step the same way.

| Automation | What it does |
|---|---|
| `rank-trail-guides` | Scores every AE mentor on a transparent 5-component, 0 to 100 scale (territory, vertical, tenure, performance, capacity) and returns a ranked top-N for the hire |
| `welcome-new-hire` | Slot-fills a welcome email from the hire profile and the chosen mentor, with a paragraph variant per experience level |

Rule of thumb used in this project: if a step is a lookup, join, score, or template fill, it is an automation. LLM calls are reserved for steps that need judgment.
