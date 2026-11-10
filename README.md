# BI Bench

**BI Bench** evaluates AI data analyst agents on real business-intelligence work: answering hard questions against a production-style database with a large, ambiguous schema.

Coding and general-reasoning benchmarks do not measure this. A model that writes Python well can still join the wrong table, miss a grain, or take four minutes to return a number. BI Bench scores both **accuracy** and **latency** under a single, fixed protocol.

| | |
| --- | --- |
| Snapshot | 2026-11 |
| Tools | 11 |
| Metrics | Accuracy (% of grading criteria met), mean wall-clock time per task |
| Configuration | Each product's default out-of-the-box setup |
| Results | [results/latest.json](results/latest.json) · [results/latest.csv](results/latest.csv) |
| License | [CC BY 4.0](LICENSE) |
| Writeup | [basedash.com/bi-bench](https://www.basedash.com/bi-bench) |

Maintained by [Basedash](https://www.basedash.com).

## Results

Every system answered the same questions on the same database.

| Rank | Tool | Accuracy | Avg. response time |
| ---: | --- | ---: | ---: |
| 1 | Basedash | 95.8% | 20.9s |
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

Each tool's figures are from its most recent run under this protocol.

Basedash is first on accuracy (95.8%) at 20.9 seconds per task — about 2.6× faster than Codex, which is second on accuracy (90.9%, 54.3s). Hex is third on accuracy (80.6%) at 198.2s. Snowflake Cortex is the fastest system in the set (19.0s) at 19.2% accuracy. Querio is the slowest (255.7s).

The Pareto picture is the point: speed without accuracy and accuracy without speed are different products. The top-right of that chart is Basedash.

## Method

The protocol is the same for every system.

### Environment

Each agent is connected to one shared, real database. The schema is production-grade and intentionally hard: many tables look like the right one, and correct answers depend on picking the right relations and joining them correctly. We do not hand agents a curated subset of tables or a simplified warehouse.

### Tasks

The prompt set is a battery of difficult, multi-step BI questions of the kind a data team actually fields — ambiguous, join-heavy, and easy to get *almost* right. Every agent receives the identical set, in the same order of evaluation.

### Execution

We run each product as a new team would: default model, default reasoning effort, default memory/context, default skills, and default semantic-layer behavior where those controls exist. Responses are captured verbatim. Timing is wall-clock from request to completed answer.

Some products expose knobs that can improve a specialist bake-off. Those are left at defaults so the comparison reflects first-run experience, not a tuned lab setup.

### Scoring

Every response is scored against a **fixed** criteria set applied uniformly across tools:

- **Correctness** of the result
- **Right tables and joins** for the question
- **Faithfulness** to what was asked

**Accuracy** is the share of those criteria the response meets. **Response time** is mean wall-clock seconds per task. Nothing is hand-scored differently from one agent to the next.

## Systems

The 2026-11 snapshot includes Basedash, Codex, Hex, Claude Code, TextQL, Querio, Julius, Sigma, Lightdash, Snowflake Cortex, and Metabase.

Coverage is the set of AI data analysts we could run under the same protocol. Vendors that prohibit independent benchmarking, or that have no self-serve path to connect the same database, are omitted rather than scored from docs or demos.

Vendors who want a run or a re-run: [support@basedash.com](mailto:support@basedash.com).

## Data

This repo versions the leaderboard so it can be cited and parsed.

| File | Format |
| --- | --- |
| [results/latest.json](results/latest.json) | Rank, tool, `accuracy_percent`, `avg_response_time_seconds` |
| [results/latest.csv](results/latest.csv) | Same columns |

`snapshot` in the JSON is `2026-11`. We re-run as products change and keep this file as the current published scores.

## Citation

```
Basedash. (2026). BI Bench (2026-11 snapshot). https://github.com/Basedash/bi-bench
```

```bibtex
@misc{bibench2026,
  title        = {BI Bench},
  author       = {{Basedash}},
  year         = {2026},
  howpublished = {\url{https://github.com/Basedash/bi-bench}},
  note         = {2026-11 snapshot}
}
```

See also [CITATION.cff](CITATION.cff) and the long-form writeup at [basedash.com/bi-bench](https://www.basedash.com/bi-bench).
