# Signal today

**Checked 18 Nov 2026.** Live product + source. This is the inventory behind the proposals.

## Counts

| Page | Count |
|---|---|
| Model configurations | **95** |
| Signals | **88** (81 scored + 7 display-only) |
| Sources | **22** |
| Arena matches | **22** |
| Human votes | **422,843** |
| Dimensions | **15** across 3 groups |
| Presets | **8** |
| Voices | **4** |
| Harness plans | **19** across 13 harnesses |
| Compare slots | **4** models |
| Chart tabs | **7** |
| Sitemap | **101** URLs |

**Live:** <https://signal-leaderboard.vercel.app/>
**Data:** <https://signal-leaderboard.vercel.app/data>
**Method:** <https://signal-leaderboard.vercel.app/method>

## Scoring model

1. Orient every metric (higher/lower is better).
2. Convert to a **cohort percentile** (midrank).
3. Average inside each dimension.
4. Combine dimensions with the index weights.
5. Charge for gaps: `missingPenalty = rawScore × (coveragePenalty/100) × (1 − coverage)`; `score = max(0, raw − penalty)`.
6. Label confidence: Strong ≥85%, Good 65–85%, Thin 45–65%, Sparse <45%.

Weights are a three-level hierarchy: group → dimension → benchmark. The flat benchmark mix is also available. Totals must reach 100; nothing is silently renormalized.

**Source:** `src/lib/scoring.ts`, `src/lib/profiles.ts`, `src/pages/Method.tsx`.

## Dimensions and groups

- **Capability:** reasoning, coding, agentic, knowledge, science, spatial, cyber.
- **Human:** human, writing, design, trust, style.
- **Practical:** speed, cost, context.

15 total. Each has a question and a description.

**Source:** `src/lib/benchmarks.ts` (`DIMENSIONS`).

## Presets

Balanced, Ship code, Security desk, 3D studio, Research desk, Lean builder, Everyday copilot, No compromise. Each has a kicker, description, dimension weights, coverage penalty, and voice.

**Source:** `src/lib/profiles.ts` (`PROFILE_PRESETS`).

## Voices

Balanced, Crisp & precise, Warm & human, Creative spark. Voice reweights style/persona sub-metrics only; it does not change the overall quality score.

**Source:** `src/lib/profiles.ts` (`VOICE_OPTIONS`).

## Guided builder

Four steps: context (six use cases with weights), trade-off (quality/balanced/fast/lean), benchmark strategy (recommended/custom), voice + open-only + long-context. Previews the resulting dimension weights.

**Source:** `src/components/ProfileStudio.tsx`, `src/lib/profiles.ts` (`ASSISTANT_USE_CASES`, `ASSISTANT_TRADEOFFS`, `buildAssistedProfile`).

## Private-only scoring

Nine source types; private kinds are controlled, independent, provider, modeled. Private-only keeps those and drops public, human, price, spec from the score. Dimensions with no private evidence drop; remaining weights renormalize; no private evidence pauses scores.

**Source:** `src/lib/benchmarks.ts`, `src/lib/profiles.ts`, `src/lib/scoring.ts`.

## Rank stability

120 simulations, ±36% log-normal jitter, 10th–90th percentile rank bands, current rank, median, all models, deterministic seed.

**Source:** `src/lib/scoring.ts` (`simulateRankStability`), `src/components/charts.tsx` (`RankStabilityChart`).

## Benchmark checks

- Agreement: Pearson correlation between dimension scores, min 5 shared models, redundant/complementary pairs.
- Coverage: model × dimension heatmap, % of inputs reported.
- Human gap: Arena percentile vs benchmark percentile, diagonal, outliers.

**Source:** `src/pages/Data.tsx`, `src/components/charts.tsx`, `src/pages/Method.tsx`.

## Task clock

```
T = TTFT × (1 + calls + commands)
  + (R + A) ÷ s
  + calls × t_tool
  + commands × t_cmd
  + ρ × subtotal
```

Defaults: 4,000 reasoning tokens, 1,000 answer tokens, 4 tool calls × 6s, 2 commands × 3s, 10% retry. Editable on the model page; compares to the published AA clock.

**Source:** `src/lib/operations.ts`, `src/pages/ModelPage.tsx` (`TimeCalculator`).

## Provider lottery

Endpoint-level log-log scatter of task time vs cost per task; per-model ranges; fastest/cheapest; provider table; spread stats; “one endpoint is not the model.”

**Source:** `src/components/charts.tsx` (`ProviderLottery`), `src/pages/ModelPage.tsx` (`ProviderSection`), `src/lib/operations.ts`.

## Monthly usage tiers

Light 2M/0.5M, Standard 10M/2.5M, Heavy 50M/10M input/output tokens. Monthly cost = input × input price + output × output price. No cache discounts, retries, taxes, or plan minimums.

**Source:** `src/lib/operations.ts` (`USAGE_TIERS`, `monthlyCost`).

## Availability

Measured endpoints, first-party endpoint, self-hostable, max provider context, modalities, label/detail.

**Source:** `src/lib/operations.ts` (`modelAvailability`).

## Coding-tool plan costs

19 plans across 13 harnesses. Effective cost = `apiTaskCost × planPrice / includedApiValue`; break-even = `includedApiValue / apiTaskCost`. Confidence: published/modeled/BYOK/none. Coding stacks: harness + model + effort, 330 trials, separate from model-level scores.

**Source:** `src/lib/harnesses.ts`, `src/pages/Harnesses.tsx`.

## Model compare

Up to 4 models: head-to-head, shape radar, dimension breakdown, practicalities, benchmark table, trade-off cards, popular starting points.

**Source:** `src/pages/Compare.tsx`.

## Alternate boards

All-round, best value, fastest, cheapest, human-rated, open weights; top 5 each; same evidence.

**Source:** `src/pages/Leaderboard.tsx` (`AlternateBoards`).

## Score breakdown

Model page “Why this rank”: per-dimension weight share, score, contribution, missing penalty, final score, formula.

**Source:** `src/pages/ModelPage.tsx` (`receipt-panel`).

## Charts

- Ternary: Smart / Cheap / Fast, adjustable triangle weights.
- Volume field: weighted geometric mean of capability, cost, time; field weights only.
- Cost/performance Pareto: frontier, effort lines, bubble size, open rings, trimming.
- Time/performance Pareto.
- Human gap.
- Rank stability.
- Provider lottery.
- Radar, usage stream, metric gallery, custom formula.

**Source:** `src/components/charts.tsx`, `docs/charts.md`.

## Benchmark metadata

- Tiers: flagship, core, specialist, display.
- Source types: public, controlled, independent, human, provider, price, spec, composite, modeled.
- Display-only metrics: `scored: false`.
- Composite guard: AA Cyber Index scored once; sub-benchmarks shown but not double-counted.
- Data audit page: sources, coverage, agreement, catalog passports, model coverage, operating methods, exports, mappings.

**Source:** `src/lib/benchmarks.ts`, `src/pages/Data.tsx`, `src/pages/Method.tsx`.
