# Verification log

**Date:** 18 Nov 2026. **Scope:** live products + public source. No private data, no credentials, no account access.

## Live checks

| Page | Observation |
|---|---|
| `mypriors.com/benchmarks` | **356** benchmarks, **130** publishers, up to **447** models each; categories, quality/recommended sorts |
| `mypriors.com/support` | **777** models, **372** benchmarks; $96/month supporter-funded; no ads |
| `mypriors.com/explore` | **1,000+** rankings made, **119** published; public profiles, remix |
| `mypriors.com/builder` | Flat benchmark weights; strictness; required; estimates; effort matching; variants; cost/time sources |
| `mypriors.com/rank` | Order/pairs, focus, fit, disagreements, estimated share |
| `mypriors.com/compare` | “Choose two rankings” — ranking compare, not model compare |
| `mypriors.com/models/gpt-6.2-astra` | 95 benchmarks, five efforts, category standings, cost/speed, all results |
| `mypriors.com/benchmarks/aa-terminalbench-v4-0` | Leaderboard, subscription cost, published measures, all results with harness |
| `mypriors.com/benchmarks/methodology` | Quality formula, cost per task, speed/time, recommended sort |
| `mypriors.com/tools` | 35-tool MCP, CLI, HTTP API, import/export, snapshots |
| `mypriors.com/skill` | Agent skill; custom theme files |
| `mypriors.com/3d` | True 3D Pareto cube, selectable axes, frontier surface |
| `signal-leaderboard.vercel.app/data` | **95** configurations, **88** signals, **22** sources, **22** Arena matches, **422,843** votes |
| `signal-leaderboard.vercel.app/method` | **81** scored metrics from **88** catalogued; provenance; private-only; task clock; operating data; limits |
| `signal-leaderboard.vercel.app/lens` | Hierarchy, guided builder, presets, voice, private-only |
| `signal-leaderboard.vercel.app/harnesses` | 19 plans, 13 harnesses, effective cost, break-even, stacks |
| `signal-leaderboard.vercel.app/compare` | Up to 4 models, breakdown, practicalities, benchmark table, trade-offs |

## Source checks

### Priors

- `WeightsPanel.tsx` — flat benchmark sliders, 0–70% share, search/grouping, required markers; no category/dimension sliders.
- `CalculationSettings.tsx` — strictness, required, effort estimates, peer estimates; no private-only, no stability, no task calculator.
- `src/engine/index.ts` — shares, coverage floor, effort matching, peer estimation, Pareto; no stability.
- `src/lib/compare.ts` — Spearman ranking compare; no model compare.
- `src/data/subscription.ts` — plan share, resets, free tiers, time-of-day, student offers; no harness plan comparison page.
- `docs/data.md` — subscription cost; harness/reseller plans as fallback; provider data plan.
- `docs/provider-data.md` — 97 providers, 3,367 offers planned; only OpenRouter operational metrics today.
- `docs/charts.md` — Pareto, 3D, radar, usage stream, custom formula; no ternary/volume/human gap/stability/provider lottery.
- `src/data/types.ts` — no provenance/private fields.
- `src/onboarding/quality.ts` — per-benchmark quality; no agreement/coverage matrix/human gap.

### Signal

- `src/lib/benchmarks.ts` — 15 dimensions, 9 provenance classes, 4 tiers, `scored: false`, private kinds.
- `src/lib/profiles.ts` — 8 presets, 4 voices, hierarchy, guided builder, private-only, coverage penalty.
- `src/lib/scoring.ts` — cohort percentiles, coverage penalty, confidence labels, rank stability (120, 0.36).
- `src/pages/Data.tsx` — agreement matrix, coverage heatmap, catalog, operating methods.
- `src/components/charts.tsx` — volume field, ternary, cost/time Pareto, human gap, stability, provider lottery.
- `src/pages/ModelPage.tsx` — task calculator, provider section, breakdown, nearest neighbours.
- `src/lib/harnesses.ts` — 19 plans, 13 harnesses, effective cost, break-even, fit, stacks.
- `src/pages/Compare.tsx` — up to 4 models, breakdown, practicalities, benchmark table, trade-offs.
- `src/pages/Leaderboard.tsx` — alternate boards and chart tabs.

## Adam Holter on X

- `@AdamHoltererer`; **25.6K** followers, **16.9K** posts, **640** following; joined June 2023; Apex, NC; bio “taking dominion of AI”; link `mypriors.com/adamholter`.
- Pinned: Terminal-Bench 4.1 is on Priors.
- Posts: benchmark saturation (~a quarter of percent-scored benchmarks), slight mix changes swing rankings, 1% means different things at 90 vs 50, “Priors is complicated,” LisanBench/FrontierPhysics additions.

**Live:** <https://x.com/AdamHoltererer>

## Caveats

- Counts change daily. The catalog, support page, and API count different things.
- “No public feature” means no public product or source feature found on 18 Nov 2026. It does not prove there is no internal plan.
- Priors’ plan data is deeper than Signal’s; the harness proposal is a **page**, not a data replacement.
- Priors tracks privately authored benchmarks as data sources; that is not a private-only scoring mode.
- Priors has OpenRouter provider metrics; it does not have an endpoint-level cost/time lottery.
- Signal’s coverage penalty is a different philosophy from Priors’ strictness. Do not present it as a correction.
- Signal’s `docs/charts.md` mentions a `ChartExpand.tsx` button, but the live UI and current source do not expose it. It is excluded from this proposal as a stale doc note.

## Commands used

- `gh auth status` — GitHub account `Zohair3`.
- `curl.exe -s --compressed https://mypriors.com/api/benchmarks` — 438 benchmark entries including older versions.
- `git clone --depth 1 --filter=blob:none --sparse https://github.com/adamholter/priors.git` — docs + source.
- Browser checks on the live URLs above.
