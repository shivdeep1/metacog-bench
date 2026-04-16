# MetaCog-Bench: Behavioral Metacognitive Dissociation Across Frontier Language Models

**Author:** Shivdeep Singh, Independent AI Researcher, India

---

## 1. Introduction

**What this benchmark reveals that single-turn evaluations cannot:** stated and behavioral metacognition are distinct constructs. A model's calibration and error-detection scores do not predict whether it uses a verification tool when offered one.

MetaCog-Bench is a 200-task benchmark for how frontier language models monitor uncertainty, detect blind spots, and decide when to switch strategy or seek help. Across two protocol layers — stated-metacognition scoring on 14 models (v6) and a behavioral probe extension on 17 models (v7) — our central descriptive finding is an apparent dissociation between stated and behavioral metacognition: a composite of calibration, error-detection, and strategy-switching items does not predict whether a model uses a Python probe tool when offered (Pearson r = -0.02, one-tailed p = 0.52, N = 14; CI wide). Instead, probe usage clusters by training lineage, and within families smaller models tend to probe more than larger siblings. We call this pattern **behavioral metacognitive dissociation**: what models say about uncertainty and what they do about it appear to be distinct constructs at this sample size.

Following the DeepMind Cognitive Taxonomy (Burnell et al., 2026), we decompose metacognition into knowledge, monitoring, and control. MetaCog-Bench operationalizes all three; the v7 extension adds a behavioral layer to ask whether stated performance survives contact with a tool-use environment.

## 2. Benchmark Design

**Six categories, 200 tasks.** Calibrated Confidence (30, Brier-scored with falsification condition); Knowing Limits (38; real + fabricated + near-miss + info-asymmetry); Error Detection (41; paired self/other attribution); Strategy Switching (31; evaluator + multi-turn); Difficulty Estimation (30; predict-before-attempt with adversarial complexity); Help Seeking (30; answer/clarify/refuse/request-info with false premises).

**Two-level structure.** Validated Core (ED + SS + KL, 110 tasks) has strongest psychometric properties; Exploratory Suite (CC + DE + HS, 90 tasks) probes alignment-sensitive behaviors at lower maturity.

**v7 behavioral extension.** A preregistered within-subjects experiment (locked April 14, 2026) comparing single-turn Baseline vs 5-turn ReAct Treatment with a Python probe tool. Four confirmatory models plus descriptive extension to 17.

**Contamination defenses.** Canary GUID, fabricated entities in KL, adversarial items designed to collapse surface heuristics.

## 3. Validation

Validation is triangulated across psychometric item analysis, LLM-as-judge review, construct divergence testing, and behavioral probing.

**Psychometric reliability.** Cronbach's alpha: CC 0.866, KL 0.884, ED 0.777, SS 0.790, DE 0.895 (all above 0.7). HS 0.618 falls below threshold and is reported as exploratory. Face validity 93.3% across 30 sampled items; ground truth accuracy 96.7%. LLM-judge headline score 82.1/100.

**Construct independence.** Spearman rho = 0.537 (p = 0.048, N = 14) between MetaCog composites and general ability rankings: a moderate correlation, leaving roughly 70% of MetaCog composite variance unexplained by general ability — consistent with partial construct distinctiveness, not full independence.

**Iterative hardening v2-v5:** strategy switching +127%, face validity +33pp; intended regressions in KL (-11%) and DE (-14%) suggest earlier scores were inflated by surface heuristics.

## 4. Results

### 4.1 Family clustering dominates (descriptive, N = 17)

Mean Treatment probe rates by family (multi-model families aggregated; single-model shown as point estimate):

- Gemma (2 models): **67.8%** (4B: 90.0%, 27B: 45.6%)
- Kimi (1 model, point estimate): 60.0%
- Qwen (2 models): **49.4%** (Instruct: 58.9%, Thinking: 40.0%)
- Claude (3 models): 32.6% (Haiku: 50.0%, Opus: 25.6%, Sonnet: 22.4%)
- Gemini (4 models): 21.5% (2.5 Flash: 31.1%, 2.5 Pro: 24.7%, 3.1 Flash-Lite: 24.4%, 3.1 Pro: 5.6%)
- GPT (5 models): **6.2%** (Nano: 15.6%, OSS-120B: 11.1%, OSS-20B: 4.4%, 5.4 Mini: 0.0%, 5.4: 0.0%)

The gap between the lowest and highest multi-model family means is roughly 11x (Gemma 67.8% / GPT 6.2%). All five GPT variants cluster between 0% and 15.6% — a family-level pattern, not a single-model anomaly.

![Family probe rate clustering across 17 models](https://raw.githubusercontent.com/shivdeep1/metacog-bench/master/figures/family_probe_rate_v7.png)

### 4.2 Inverse scaling within families

In every multi-model family except Qwen (analyzed separately below), smaller variants probe at least as often as larger siblings. Gemma 4B 90.0% > 27B 45.6%; Claude Haiku 50.0% > Sonnet 22.4% / Opus 25.6%; Gemini 2.5 Flash 31.1% > 2.5 Pro 24.7% > 3.1 Pro 5.6%; GPT Nano 15.6% > OSS variants > 5.4 and Mini 0.0%. Suggestive of behavioral probing being shaped by training curriculum rather than capability scaling.

### 4.3 Preregistered hypotheses: one underpowered, one null

**H1 (probe rate tracks stated metacognition).** The confirmatory test on the four preregistered models gave r = +0.61 with p = 0.195 (one-tailed, N = 4) — underpowered and well above the Bonferroni-corrected alpha of 0.0125. The extended-N descriptive correlation on the 14 models with v6 composites is **r = -0.02 (one-tailed p = 0.52; two-tailed p = 0.96, N = 14)**. v6 stated-metacognition composites do not predict v7 behavioral probing.

**H2 (probe access lifts accuracy).** Confirmatory 340 pairs: mean_diff = 0.000, p = 0.50, d = 0.00. Extended 1,510 pairs: mean_diff = -0.011, p ≈ 0.91, d = -0.03.

We report these outcomes honestly. They fail to support the simplest reading of v6's "monitoring-control tradeoff": tool access does not visibly activate or redistribute latent metacognitive capacity along the axes v6 measured.

![Stated metacognition vs behavioral probe rate (N=14, r = -0.02)](https://raw.githubusercontent.com/shivdeep1/metacog-bench/master/figures/behavioral_vs_stated_v7.png)

### 4.4 Two informative within-family comparisons

**Qwen Instruct vs Thinking (same-base ablation).** Instruct probes 58.9% vs Thinking 40.0%. In v6 the same pair showed Thinking +0.217 on calibration and -0.133 on help-seeking. Consistent with post-training choices — not capability — being associated with opposing shifts in stated and behavioral profiles.

**GPT family (observational, not controlled).** Five GPT-lineage models spanning proprietary and open-weight all cluster at 0-16%. Post-training variation does not visibly lift any variant out of the low-probing regime.

### 4.5 Format compliance

All 17 models produced parseable output across 3,060 trials. Sampled probe executions produced usable stdout. Probe-rate variance reflects **decisions to probe**, not parser artifacts.

## 5. Why This Matters

**For benchmark design.** Stated-metacognition benchmarks (including v6) can rank models reliably while being largely decoupled, in our sample, from the behavior practitioners care about under tool access. Benchmarks measuring "what models say about uncertainty" should not be treated as proxies for "what models do when uncertainty has consequences." v6 still ranks models on a real psychometric construct — but that construct is not probe-using behavior.

**For AI safety.** A deployed assistant that rarely self-verifies may confidently push through ambiguous queries. The order-of-magnitude family spread indicates deployment-relevant heterogeneity that single-score leaderboards obscure. Concretely: a code-review agent on GPT-5.4 cannot rely on spontaneous verifier-calling; the same wrapper on Gemma-3-4B verifies ~9 times out of 10.

**For metacognition research.** Our data suggest stated and behavioral metacognition are distinct constructs; combining them into a single composite likely conflates signals that training interventions push in opposing directions. Ackerman's ICLR 2026 distinction between monitoring signals and action policies is consistent with this interpretation.

## 6. Limitations

1. **Preregistered hypotheses null or underpowered.** H1 confirmatory was underpowered (N = 4, p = 0.195). H1 descriptive extension on 14 models was also null (r = -0.02). H2 extended was null (mean_diff ≈ 0). Section 4.1-4.2 findings are descriptive and post-hoc at 17-model scale.
2. **Probing as a proxy.** Probe rate conflates willingness to use tools, tool-use training, and metacognitive judgment. A different probe interface, task distribution, or time budget could yield different family rankings.
3. **Help Seeking reliability.** Alpha 0.618 below 0.7; HS is exploratory.
4. **Shortcut vulnerability.** Judge flagged 60% of sampled items as potentially shortcuttable, concentrated in DE and CC.
5. **Strategy switching construct gap.** 25 of 31 SS items are evaluator-mode; only 6 are multi-turn self-evaluation.
6. **Model sample.** Family aggregates rest on 1-5 models each. Gemini 3.1 Pro / Flash-Lite are preview snapshots (excluding them raises Gemini family mean to 27.9%). Several candidate models were non-functional and excluded; this is not a random draw. Model access via Kaggle Community Benchmarks runtime (proprietary + open-weight models exposed through the `@kbench.task` SDK) and NVIDIA NIMS (integrate.api.nvidia.com; Kimi-K2 routed through this endpoint). No other inference providers were used.
7. **Single behavioral run.** v7 is one protocol round; H2 extended uses 1,510 of 1,530 possible pairs (20 excluded for missing trials).
8. **Single-turn stated items.** Most v6 tasks measure meta-judgment rather than live attempt-monitor-adjust behavior.
9. **No human baseline.** DeepMind's cognitive taxonomy calls for human-baseline anchoring. MetaCog-Bench has LLM-as-judge validation and psychometric reliability analysis, but lacks human performance data on the same 200 tasks. This is the primary direction for v8.

## 7. Future Work

**Human baseline collection.** A 5-10 person human pilot on the 40-item high-confidence core would directly address the DeepMind taxonomy's human-anchoring criterion and allow normalized AI-vs-human scoring.

**Embodied multi-agent extension.** Parallel work ("Metacognitive Orchestration in Multi-Agent Systems", [proposal](https://github.com/shivdeep1/metacog-bench/blob/master/research_proposal/metacognitive_orchestration_proposal.pdf)) extends this framework to population-level meta-learning in open-ended environments — from "does the model self-verify?" to "does the system self-correct at the population level?"

**Benchmark URL:** https://www.kaggle.com/code/shivdeepsingh1/metacog-bench-v6
**Code + figures + proposal:** https://github.com/shivdeep1/metacog-bench

## 8. References

- Ackerman, R. et al. (2025). *arXiv:2509.21545* (ICLR 2026).
- Burnell, R. et al. (2026). Rethinking Machine Intelligence. *DeepMind Tech Report*.
- Kamruzzaman, M. et al. (2025). Self-Correction Bench. *arXiv:2507.02778*.
- Feng, S. et al. (2025). AbstentionBench. *arXiv:2506.09038*.
- Jin, Y. et al. (2025). Metacognitive Tradeoffs. *arXiv:2505.13763*.
- Kadavath, S. et al. (2022). *arXiv:2207.05221*.
- Brier, G. W. (1950). *Monthly Weather Review*, 78(1), 1-3.
- Steyvers, M. & Peters, M. (2025). *Trends in Cognitive Sciences*.
