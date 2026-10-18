# Skills

Each skill is a step that needs LLM judgment: drafting, scoring, summarizing, or role-play. Deterministic steps live in [`../automations/`](../automations/README.md).

| Skill | What it does | Retrieval |
|---|---|---|
| `generate-onboarding-plan` | Drafts a personalized 1 to 4 week Trailhead plan from the hire profile, then validates every module ID against an allow-list | BM25 |
| `answer-sdr-question` | AI Tutor. Answers free-form SDR questions with inline `[n]` citations and refuses when sources don't cover the question | ChromaDB |
| `score-cold-call` | Scores a call transcript on the coaching rubric and drafts a structured coaching note | BM25 |
| `simulate-cold-call` | Plays a prospect persona turn by turn so a trainee can practice | none |
| `debrief-cold-call` | Scores a finished simulation and writes a debrief | BM25 |
| `score-certification` | Scores an SDR on a 5-dimension certification rubric with quoted evidence per dimension; the server recomputes the band | BM25 |
| `generate-handoff-doc` | Turns a newly certified SDR's answers to [QUESTIONS.md](generate-handoff-doc/QUESTIONS.md) into a manager-facing program debrief | none |

## Layout

```
skills/<name>/
├── SKILL.md            # agent contract: when to invoke, inputs, outputs
├── README.md           # human docs (where present)
└── scripts/<name>.py   # the executable; all LLM calls go through utils.connect
```

`bash install.sh` symlinks every `SKILL.md` into `.claude/skills/` so Claude Code can load them as agent skills.

## Shared CLI and envelope

Every skill and automation is built on `utils/sdr_common.make_skill_parser()` and accepts the same flags (`--hire-id`, `--data-dir`, `--out-dir`, `--workflow-run-id`, `--step-id`, `--json`). With `--json` it prints one envelope:

```json
{
  "status": "ok",
  "skill_name": "generate-onboarding-plan",
  "workflow_run_id": "wf-...",
  "step_id": "...",
  "next_action": "rank-trail-guides",
  "confidence": 0.91,
  "review_required": false,
  "artifact_refs": ["working/<run_id>/01_onboarding_plan.md"],
  "outputs": {"sources": ["..."]},
  "error": null
}
```

The orchestrator follows `next_action`; `review_required` (set when confidence is below 0.60) pauses the run at a human gate. Errors use the same shape with `status="error"` and a non-zero exit code.

## Offline mode

Set `MOCK_LLM_RESPONSE` to a JSON string and every skill returns it instead of calling the model. The test suite uses this to run fully offline.
