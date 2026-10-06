# BEAM 100K: Assertion vs Hindsight

**Assertion scores 0.811 on BEAM 100K, vs 0.779 for Hindsight, with the same answer model, prompt and judge (3 answering runs each), while giving the answer model 12.2k memory tokens per question against Hindsight's 17.7k.**

Write-up: [assertion-ai.com/benchmark](https://assertion-ai.com/benchmark) · Install: [assertion-ai.com/install](https://assertion-ai.com/install)

| System | Runs | Accuracy per run | Mean | Memory tokens / question |
|---|---|---|---|---|
| Assertion | 3 | 0.813 · 0.807 · 0.814 | **0.811** | 12,212 |
| Hindsight | 3 | 0.778 · 0.771 · 0.789 | **0.779** | 17,655 |

## Method

We ran the [Agent Memory Benchmark](https://github.com/vectorize-io/agent-memory-benchmark) BEAM 100K split (commit `5d5e8dbe`): 20 long conversations and 400 questions across 10 question types. Each system's memory was built once per conversation. For every question, the system's memory text was given to the same answer model (`gemini-3.1-pro-preview`) with AMB's BEAM prompt, and the answer was scored by AMB's BEAM judge (`gemini-3.5-flash`). For Hindsight we used the retrieved context from its published AMB results unchanged, and answered and judged it exactly as we did our own. Each run repeats answering and judging from the same memory text. Full settings are in [`config.json`](config.json).

## What's here

The engine is closed source, but everything needed to check the scores is public: every answer, every score and the exact memory text the answer model saw.

- `summary/overall.json`: accuracy per run, mean, and mean memory tokens for each system.
- `summary/per_conversation.csv`: the same, per conversation.
- `data/<system>/conv_NN.jsonl`: one line per question with `query_id`, `category`, `question`, `memory` (the exact text given to the answer model), `memory_tokens` (cl100k), and `runs` (answer and score per run).

Questions and gold answers come from the public BEAM dataset; join on `query_id` (`<conversation>_<category>_<index>`).
