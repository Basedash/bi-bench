# BI Bench

Aggregated results from [BI Bench](https://www.basedash.com/bi-bench), Basedash's first-party benchmark of AI data analyst agents on hard business-intelligence questions against a real, messy production-style database.

Most AI-agent benchmarks measure code generation or general reasoning. BI Bench measures something narrower: can an agent sit down in front of a complicated schema and return a correct answer to a difficult BI question, in a reasonable amount of time?

This repository is a citable snapshot of the **published scores**. It does not include the questions, the database, transcripts, or the grading rubric.

- Narrative writeup: https://www.basedash.com/bi-bench
- License: [CC BY 4.0](LICENSE)
- Machine-readable results: [results/latest.json](results/latest.json), [results/latest.csv](results/latest.csv)

Basedash builds one of the products in this comparison. Treat this as a first-party benchmark, not an independent bake-off.

## Current snapshot (2026-08)

11 tools, same database, same questions, default settings for each product.

| Rank | Tool | Accuracy | Avg. response time |
| ---: | --- | ---: | ---: |
| 1 | Basedash | 92.1% | 28.6s |
| 2 | Codex | 90.9% | 54.3s |
| 3 | Hex | 80.6% | 198.2s |
| 4 | Claude Code | 78.0% | 118.5s |
| 5 | TextQL | 64.7% | 134.5s |
| 6 | Querio | 54.9% | 255.7s |
| 7 | Julius | 46.1% | 68.1s |
| 8 | Sigma | 35.2% | 42.6s |
| 9 | Lightdash | 23.8% | 82.1s |
| 10 | Snowflake Cortex | 19.2% | 19.0s |
| 11 | Metabase | 12.4% | 40.9s |

Basedash ranked first: 92.1% accuracy at 28.6 seconds per task, nearly twice as fast as Codex (90.9%, 54.3s), the next most accurate agent. Snowflake Cortex was the fastest overall (19.0s) with 19.2% accuracy.

Numbers are a snapshot, not a final ranking. Tools change; we re-run as they evolve.

## How the run works

High-level only, matching the public writeup.

1. **Connect.** Each agent is connected to the same real database with a large, complicated schema. The schema is not simplified. Several tables look plausible; the right answer depends on using the correct ones and joining them correctly.
2. **Run.** Every agent gets the same set of difficult, multi-step BI questions. Responses are captured verbatim, with wall-clock time.
3. **Evaluate.** Every response is graded against a fixed set of criteria covering correctness, use of the right tables and joins, and whether the answer matches the question. Accuracy is the share of those criteria met. Response time is mean wall-clock time per task.

Each tool is run with its default user experience (default model, reasoning effort, memory, context, skills, semantic layer behavior, and anything else that ships out of the box). This is not a tuned bake-off.

This is not a complete map of the category. Some tools disallow benchmarking in their terms. Others do not have self-serve onboarding that lets us run the same setup independently.

## What is not in this repo

- Question text or prompts
- Database schema, dumps, or ERDs
- Per-question or per-criterion scores
- Agent transcripts
- The grading rubric beyond the summary above

## Include another tool

If you build one of these products and want a run or re-run, email [support@basedash.com](mailto:support@basedash.com).

## Cite

```
Basedash. BI Bench (2026-08 snapshot). https://github.com/Basedash/bi-bench
Also: https://www.basedash.com/bi-bench
```

```bibtex
@misc{bibench2026,
  title        = {BI Bench},
  author       = {{Basedash}},
  year         = {2026},
  howpublished = {\url{https://github.com/Basedash/bi-bench}},
  note         = {2026-08 snapshot of aggregated AI data analyst results. Writeup: https://www.basedash.com/bi-bench}
}
```
