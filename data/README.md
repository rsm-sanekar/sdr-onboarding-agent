# Data

All data here is synthetic. It is the operational data the workflow processes; reference knowledge for retrieval lives separately in [`../rag/knowledge_base/`](../rag/README.md).

| Path | Contents |
|---|---|
| `raw/sdr_profiles.csv` | New-hire records (territory, vertical, experience level, start date) |
| `raw/ae_profiles.csv` | Account Executives who can mentor a new hire |
| `raw/summaries/` | One Markdown summary per hire, read by the onboarding planner |
| `raw/sim_personas.json` | Prospect personas for the cold-call simulator |
| `raw/sample_transcripts/`, `raw/sample_audio/` | Demo inputs for Coaching Notes |
| `raw/cast_of_characters.md` | Who's who across the synthetic dataset |
| `sdr_records/` | 7-SDR certification cohort: simulation transcripts, exam answers, coaching notes, cached gap analyses |
| `decision_log.json` | Every human approve / edit / reject / escalate decision |
| `gap_tracker.json` | Rolling counts that feed the dashboard |
| `chroma_db/` | Persisted ChromaDB index used by the AI Tutor |
| `working/` | Per-run envelopes and artifacts (gitignored) |

Re-seed the certification cohort with `uv run python skills/score-certification/scripts/seed_synthetic_cohort.py`.
