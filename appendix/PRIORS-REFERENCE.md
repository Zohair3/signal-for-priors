# Priors today

**Checked 18 Nov 2026.** Live product + public `adamholter/priors` source and docs.

This is the reference for what Priors already has. If something here is wrong, record the evidence in `appendix/VERIFICATION.md`.

## Counts

| Page | Count |
|---|---|
| Benchmark catalog | **356** current benchmarks, **130** publishers, up to **447** models on one benchmark |
| Support page | **777** models, **372** benchmarks |
| Explore | **1,000+** rankings made, **119** published |
| Open API | **438** benchmark entries including older versions |
| Daily snapshots | Since **5 Sep 2026** |
| MCP | **35** tools |

The pages count different things (current vs all versions, models vs configurations) and the data changes daily. Do not treat the counts as a reconciled total.

**Live:** <https://mypriors.com/benchmarks>, <https://mypriors.com/support>, <https://mypriors.com/explore>, <https://mypriors.com/tools>

## Builder

- Flat benchmark weights, 0–70% share per benchmark. Sliders show share of the index, not raw weight.
- Search and browse by topic or source; family variants behind a gear; “Popular,” “All benchmarks,” “Older and niche.”
- Required benchmarks (hard per-benchmark gate).
- Strictness 0–100: a model is ranked only when measured results cover at least that share of the index weight.
- Effort matching: exact, calibrated, or nearest; “estimate from measured effort differences” or “use exact effort results only.”
- Missing-data handling: peer estimates from similar models; otherwise optional missing values are left out and remaining weights renormalized.
- Ranking variants: best effort or all efforts.
- Pareto variants: best or all.
- Exclude models; release-age filter.
- Cost source and time source: AA or T3 Code; subscription or API basis.
- Highlights; custom formula for chart metrics.
- Undo/redo, clear all, last valid mix.
- “Inspect a calculation”: per-benchmark raw, source, contribution, measured share, cost, speed, Pareto, other efforts, excluded variants.

**Source:** `WeightsPanel.tsx`, `CalculationSettings.tsx`, `Builder.tsx`, `ModelDetail.tsx`, `src/engine/index.ts`, `docs/charts.md`.

## Rank flow

- Put models in order, or rank in pairs.
- Focus: Capabilities, Knowledge, Problem solving, General.
- “Find my index” fits a benchmark mix to the order.
- Reports exact vs approximate fit, remaining disagreements, estimated share, strictness, effort matching, benchmark count.
- Library seeding from precomputed mixes; exact verification against the live snapshot.
- Does not exclude models; an unlisted model must never land in the top 5.

**Source:** `src/onboarding/` (`Onboarding.tsx`, `optimizer.ts`, `library.ts`), `docs/onboarding.md`.

## Model pages

- For GPT-6.2 Astra: **95 benchmarks** measured across five efforts.
- Per-effort ranks; best-at-effort.
- Category standings: 132 results across every current benchmark, average standing among ranked models.
- Cost and speed: output speed, time to first token, output tokens, token price, subscription cost per task, API cost.
- “This ranking’s benchmarks”: per-benchmark all-effort table with rank and leader.
- All 95 benchmarks with “show more.”
- Links to sources and methodology.

**Live:** <https://mypriors.com/models/gpt-6.2-astra>

## Benchmark pages

- Description, version selector, publisher, model/result counts, data date, source link.
- Leaderboard with effort labels.
- Score vs subscription cost per task.
- “More from this benchmark”: published sub-measures (sub-scores, splits, token counts), breakdown table.
- All results table: rank, model, effort, score, subscription $/task, API $/task, harness.
- Category tags.

**Live:** <https://mypriors.com/benchmarks/aa-terminalbench-v4-0>

## Compare

- Compares **two rankings**, not models.
- Spearman order agreement, shared top-N, biggest split, “why they differ,” stacked weight bars, slope chart.
- No model-vs-model head-to-head.

**Live:** <https://mypriors.com/compare>

## Explore and profiles

- Public profiles, published pages, remix, “also” variants, update notices.
- 1,000+ rankings made; 119 published.
- Page sections: rankings, Pareto, speed, benchmark, history, gallery, text, links.

**Live:** <https://mypriors.com/explore>, <https://mypriors.com/adamholter>

## Tools

- MCP server at `https://mypriors.com/mcp` with 35 tools.
- CLI `priors`; `priors rank`, `priors model`, `priors bench`, `--json`.
- HTTP API: `/api/benchmarks`, `/api/snapshot`, `/api/library`.
- Import a custom benchmark (browser-only or signed-in page).
- Export PNG/SVG/CSV/JSON; daily snapshots since 5 Sep 2026.
- Agent skill; agent token for writes.

**Live:** <https://mypriors.com/tools>, <https://mypriors.com/skill>

## Quality score

A 0–100 score for how useful a benchmark is for telling current models apart:

- Headroom and spread: 30%
- Recency: 20%
- Objectivity: 20%
- Breadth: 15%
- Frontier coverage: 15%
- +15 for preferred benchmarks
- −25 for older versions with a clear replacement
- −20 if last updated before 22 Sep 2026

“Recommended” sort: `quality + 12 × log2(1 + pages using it)`.

**Live:** <https://mypriors.com/benchmarks/methodology>

## Cost model

- Cost per task is measured cost, never token price alone.
- Subscription pricing: measured cost × the model’s share of API price on a subscription plan.
- Median plan per model until the user picks one.
- Plan data from Real API Pricing; first-party plans first, reseller/harness plans as fallback.
- Plan changes, plan multiples, budget plans, time-of-day rates, student offers, free tiers.
- Limit resets and banked resets, off by default.
- Speed tiers (Standard, Flex, Fast, Ultrafast), with plan coverage.
- API pricing toggle.
- Cost and time sources: AA or T3 Code.

**Source:** `docs/data.md` (“Subscription cost”), `src/data/subscription.ts`, `docs/charts.md`.

## Missing data

- Strictness gate; a model is ranked only above the measured coverage threshold.
- Effort estimates from measured effort differences.
- Peer estimates from similar models, with donors and a likely range.
- Otherwise missing values are left out and remaining weights renormalized.
- “A missing result is not a zero, and an estimate is not a measurement.”
- Per-row confidence intervals where published.
- Measured share shown in the calculation inspector.

**Source:** `CalculationSettings.tsx`, `src/engine/index.ts`, blog post “I built Priors…”

## Provider data

- OpenRouter source: uptime, providers, throughput, latency, tool-call errors; `defaultWeight: 0`.
- A `docs/provider-data.md` plan for a richer provider/price/region view (97 providers, 3,367 offers), not yet a public endpoint-level view.
- No endpoint-level cost/time lottery or provider table.

**Source:** `docs/provider-data.md`, `docs/data.md` (`openrouter`).

## Harness data

- A `harness` field on benchmark observations (e.g., mini-SWE-agent, Codex CLI, Claude Code).
- Harness shown in all-results tables.
- Some harness/reseller plans used as fallback for subscription token price (OpenCode Go, Command Code, Droid, Ollama).
- No plan comparison page, no break-even tasks, no coding-agent stack view.

**Source:** `docs/data.md`, benchmark pages.

## Charts and views

- Pareto scatter: score vs subscription cost; frontier; effort lines; subscription/API toggle.
- 3D Pareto cube: orbit/zoom/pan, selectable axes, frontier surface, closest to best corner, all efforts.
- Strengths radar: benchmark or category spokes, descriptions, range scaling, bars toggle.
- Usage stream: daily share/volume, window averages.
- Metric gallery: cost, time, speed, latency, tokens, release date, uptime, usage.
- Custom formula.
- No ternary, volume field, human gap, stability, or provider lottery.

**Live:** <https://mypriors.com/builder>, <https://mypriors.com/3d>
**Source:** `docs/charts.md`, `src/components/threed/`.

## Do not propose

- Flat benchmark weights, required benchmarks, exclusion filters.
- Rank-by-model-order or pairwise elicitation.
- Model finder.
- Public profiles, remixing, published pages.
- MCP/CLI/API, import/export, snapshots.
- Benchmark quality score, recommended sort.
- Cost per task, subscription-adjusted cost, median plans, speed tiers, free tiers, API pricing.
- Exact effort matching, variant-level scoring, no invented scores.
- Missing-data strictness, effort estimates, peer estimates, renormalization.
- Model and benchmark pages with per-effort rows, harness, tokens, leaders.
- Ranking-vs-ranking compare with Spearman, shared top-N, biggest split.
- Open/closed filters, measured coverage, confidence intervals.
- 3D Pareto cube, radar, usage stream, custom formula.
