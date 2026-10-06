# Assertion benchmark results

Published results for Assertion's memory engine on public long-term memory benchmarks. The engine is closed source; each benchmark folder holds the exact memory text the answer model saw, every answer and every score, so the numbers can be checked question by question.

| Benchmark | Assertion | Compared with | Folder |
|---|---|---|---|
| BEAM 100K (400 questions, 20 conversations) | **0.811** | Hindsight 0.779 (same answer model, prompt and judge; 3 runs each) | [`beam-100k/`](beam-100k/) |

Write-up: [assertion-ai.com/benchmark](https://assertion-ai.com/benchmark) · Install: [assertion-ai.com/install](https://assertion-ai.com/install)
