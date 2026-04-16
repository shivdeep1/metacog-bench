# MetaCog-Bench

**Behavioral Metacognitive Dissociation Across Frontier Language Models**

A 200-task benchmark measuring stated vs behavioral metacognition in frontier LLMs, submitted to the DeepMind / Kaggle *Measuring Progress Toward AGI — Cognitive Abilities* Hackathon 2026 (Metacognition track).

**Author:** Shivdeep Singh, Independent AI Researcher, India

---

## TL;DR

- **6 metacognitive sub-abilities** (DeepMind taxonomy): Calibrated Confidence, Knowing Limits, Error Detection, Strategy Switching, Difficulty Estimation, Help Seeking
- **200 tasks** with psychometric validation (Cronbach alpha > 0.7 on 5 of 6 categories) and LLM-as-judge review (82.1/100)
- **14 frontier models** scored on stated metacognition; **17 models** tested in a behavioral probe extension (Python verification tool, preregistered April 14, 2026)
- **Central finding:** stated metacognition does NOT predict tool-use behavior (Pearson r = -0.02, N = 14). Family clustering (11x spread across GPT/Gemma/Claude/Gemini/Qwen) and within-family inverse scaling dominate instead.

---

## Contents

| Path | Description |
|---|---|
| `writeup.md` | Full benchmark writeup (<=1,500 words, final submission version) |
| `figures/` | Four v7 result figures embedded in the writeup |
| `research_proposal/` | Companion future-work proposal: population-level metacognitive orchestration in multi-agent systems |

## Kaggle Artifacts

- **Benchmark notebook:** https://www.kaggle.com/code/shivdeepsingh1/metacog-bench-v6

## Infrastructure

Model access via Kaggle Community Benchmarks runtime (`@kbench.task` SDK) and NVIDIA NIMS (`integrate.api.nvidia.com`, used for Kimi-K2). No other inference providers were used.

## Citation

If you use MetaCog-Bench, please cite:

```
Singh, S. (2026). MetaCog-Bench: Behavioral Metacognitive Dissociation Across
Frontier Language Models. DeepMind / Kaggle Measuring Progress Toward AGI
Hackathon 2026, Metacognition Track.
```

## License

Apache 2.0 for code; CC BY 4.0 for writeup and figures.
