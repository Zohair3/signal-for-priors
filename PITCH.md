# Signal → Priors

A pitch in three parts:

1. **Signal, in detail** — what it is, how it works, what it measures.
2. **What is similar** — where Priors already does the same or more.
3. **What Priors could take** — the additions that are genuinely different.

---

# Part 1 — Signal, in detail

## 1.1 What Signal is

Signal is a model leaderboard that shows its work.

It does not run benchmarks. It takes published evidence from 22 sources, normalizes it, labels where it came from, and lets the reader set the weights. Every score opens to its inputs, formula, coverage, and caveats.

Current shape:

| Item | Count |
|---|---|
| Model configurations | 95 |
| Signals | 88 (81 scored + 7 display-only) |
| Sources | 22 |
| Arena matches | 22 |
| Human votes | 422,843 |
| Dimensions | 15, in 3 groups |
| Presets | 8 |
| Voices | 4 |
| Coding-tool plans | 19, across 13 harnesses |
| Compare slots | 4 models |
| Chart tabs | 7 |
| Indexed URLs | 101 |

The core claim: **there is no best model, only the best model for the work.** The product is a lens over evidence, not another benchmark.

It is for people who want to set the terms: a builder choosing a coding model, a researcher checking whether benchmarks agree, an operator comparing provider endpoints, a buyer comparing coding-tool plans.

## 1.2 The thesis

Signal is built on four rules:

1. **A score is a claim.** Show the formula, the inputs, the source, the sample, and the date.
2. **Missing is not zero.** A missing result reduces coverage; it does not become a bad score.
3. **An estimate is not a measurement.** Modeled values are labeled and kept separate.
4. **The weights are yours.** The same evidence can produce different rankings under different priorities.

Those rules explain most of the product.

## 1.3 The data

Signal uses 81 scored metrics from 88 catalogued signals.

**Sources include:** Artificial Analysis (Intelligence Index, expanded suite, Cyber Index, provider benchmarks), LMArena, DesignArena, GDPx, AfterQuery, HealthBench, Terminal-Bench Science, GameFeel, LiveBench, FrontierMemory, RWE-bench, Vending-Bench 2, MCP Atlas, LisanBench, and others.

**The ranked unit is a configuration:** model + reasoning effort. GPT-6.2 Astra at max and at low are different rows. Signal does not substitute a sibling, predecessor, or average when an exact effort is missing.

**Each metric carries:**

- a source type: public, controlled, independent, human, provider, price, spec, composite, modeled;
- a tier: flagship, core, specialist, display;
- a sample note;
- a source link;
- a caveat;
- a coverage count;
- a scored/display-only flag.

**Display-only metrics** are shown for inspection but not scored by default, usually because they overlap another metric. **Composites** are scored once; their sub-benchmarks are shown but not double-counted.

## 1.4 The scoring

Signal scores in cohort percentiles, not raw points.

1. Orient every metric so higher is better.
2. Convert the value to a percentile within the 95-configuration cohort.
3. Average the percentiles inside each dimension.
4. Combine dimensions using the current index weights.
5. Charge for missing evidence:

```
raw = Σ(weight share × dimension percentile)
penalty = raw × (coverage penalty / 100) × (1 − coverage)
score = max(0, raw − penalty)
```

6. Label confidence:

| Label | Coverage |
|---|---|
| Strong | ≥85% |
| Good | 65–85% |
| Thin | 45–65% |
| Sparse | <45% |

**Defaults:** coverage penalty 12%, flat benchmark mix, best effort per model, exact effort matching.

The board is deterministic. The only randomness in the product is the seeded rank-stability simulation.

## 1.5 The lens

Signal has two weighting modes.

### Category & parameter

Three groups:

- **Capability:** reasoning, coding, agentic, knowledge, science, spatial, cyber.
- **Human:** human, writing, design, trust, style.
- **Practical:** speed, cost, context.

Each group splits into 15 dimensions; each dimension splits into benchmarks. Every level has shares that total 100. If a level does not total 100, scores pause and a resolver offers `Even` or `Scale`. Nothing is silently renormalized.

### Benchmark mix

One global benchmark mix. The hierarchy is derived from it. This is the precision mode.

### Guided builder

Four steps:

1. **Context:** six use cases, each with a weight. Build software, research, visual work, security, writing, mixed.
2. **Trade-off:** quality at any cost, balanced, fast, or lean.
3. **Benchmarks:** recommended flagship-first weights, or tune every benchmark.
4. **Voice:** Balanced, Crisp & precise, Warm & human, Creative spark; plus open-weights-only and long-context.

The result is an editable flat mix.

### Presets and voice

Eight presets: Balanced, Ship code, Security desk, 3D studio, Research desk, Lean builder, Everyday copilot, No compromise.

Four voices. Voice changes style/persona sub-metrics only; it does not change the overall quality score.

### Private-only

A mode that scores only `controlled`, `independent`, `provider`, and `modeled` evidence. Public benchmarks, human votes, list prices, and specs stay visible but are marked `IGNORED`. Dimensions with no private evidence drop out; the rest renormalize. If nothing private remains, scores pause.

## 1.6 The views

### Board

- Lens summary: name, group shares, private-only toggle.
- Ranked board: score, human rating, task time, cost per task, monthly cost, context, access.
- Quick picks: top, human favourite, shortest task clock, widest provider gap.
- Alternate boards: all-round, best value, fastest, cheapest, human-rated, open weights.
- Chart tabs: volume, ternary, cost, time, human gap, stability, provider lottery.

### Model page

- Score breakdown: parameter, weight share, percentile, contribution, missing penalty, final score, formula.
- Capability fingerprint: strongest evidence, evidence gaps.
- Operating data: task clock, subscription equivalent, availability.
- Provider transparency: endpoint count, spread, fastest, cheapest, endpoint table.
- Human signal: Arena rating, votes, category breakdown.
- Nearest neighbours: models close on the current lens.
- Benchmark table: every result, with source and caveat.

### Benchmark and data pages

- Benchmark page: leaderboard, score vs subscription cost, published sub-measures, all results with harness and cost.
- Data page: source cards, coverage heatmap, agreement matrix, catalog passports, model coverage, operating methods, exports, mappings, limitations.

### Method page

- Formula, worked example, evidence classes, private-only, no borrowed scores, no zero-fill, no double counting.
- Task-time formula and assumptions.
- Subscription equivalent at three usage tiers.
- Availability and latency ranges.
- Human signal: what it does and refuses to claim.
- Limits and reproducibility.

### Compare

Up to four models:

- head-to-head;
- shape radar;
- dimension-by-dimension score breakdown;
- cost and time;
- benchmark table;
- trade-off summary, not a winner.

### Harness page

- 19 plans across 13 coding tools.
- Monthly price, billing model, included API value, effective cost per task, break-even tasks, confidence.
- Model selector and modeled-multiplier control.
- Fit notes: first-party, editor-native, BYOK, routing.
- Coding stacks: harness + model + effort, 330 trials, separate from model scores.

## 1.7 The charts

| Chart | Question it answers | Mechanics |
|---|---|---|
| Volume field | Which model has the best combined capability, cost, and time? | Weighted geometric mean; field weights change the chart only |
| Ternary | Is this model smart, cheap, or fast? | Barycentric position from three weighted scores |
| Cost/performance | What is the best score at each price? | Score vs cost, frontier, effort lines |
| Time/performance | What is the best score at each task time? | Score vs modeled clock, frontier |
| Human gap | Do benchmarks and human preference agree? | Arena percentile vs benchmark percentile |
| Rank stability | Does the rank survive a weight change? | 120 perturbations, ±36% log-normal, 10th–90th percentile band |
| Provider lottery | How much does the endpoint change the result? | Endpoint-level task time vs cost, per-model ranges |

## 1.8 The technical shape

- Static client-side scoring; one snapshot; no server round-trip for a score.
- 101 indexed URLs; route-level titles, descriptions, canonical links, JSON-LD.
- Share cards and link previews.
- Local persistence for the lens and compare slots.
- No account required.
- Deterministic scoring; seeded stability.
- Source-qualified rows; no fuzzy inheritance.
- Display-only metrics and composites kept separate from scored inputs.

## 1.9 What Signal is not

- Not a benchmark runner.
- Not a data platform with 356 benchmarks.
- Not a social network with public profiles.
- Not an API/MCP/CLI product.
- Not a plan-cost database.

Those are Priors’ strengths.

---

# Part 2 — What is similar

Priors and Signal overlap at the center: both are model leaderboards with per-effort variants, benchmark weights, cost/time, missing-data discipline, model pages, benchmark pages, and comparison views.

The difference is where each goes deeper.

| Capability | Priors | Signal | Verdict |
|---|---|---|---|
| Catalog | 356 benchmarks, 130 publishers, up to 447 models | 88 signals, 22 sources, 95 configurations | Priors deeper |
| Ranked unit | Model + effort; exact matching | Model + effort; exact matching | Same |
| Scores | Published values; no stretching | Published values; no invented scores | Same rule |
| Cost per task | Measured cost; subscription-adjusted; API; speed tiers | Modeled task cost; subscription and plan effective cost | Priors deeper |
| Custom weights | Flat benchmark mix | Three-level hierarchy + flat mix | Signal different |
| Missing data | Strictness, estimates, renormalization | Coverage penalty, confidence labels, private-only | Different method |
| Model pages | 95 benchmarks for Astra; per-effort ranks | Breakdown, calculator, providers, neighbours | Priors deeper on data; Signal different on receipts |
| Benchmark pages | Leaderboard, sub-measures, all results | Catalog passports | Priors deeper |
| Compare | Rankings side by side | Up to 4 models head-to-head | Different object |
| Public profiles | 1,000+ rankings, 119 published, remix | Local lens, share links | Priors deeper |
| API/MCP/CLI | 35-tool MCP, CLI, HTTP API | None | Priors deeper |
| Quality score | 0–100 per benchmark, recommended sort | Tiers and source types, no quality score | Priors deeper |
| Rank flow | Order/pairs, focus, fit | Guided job/trade-off builder | Signal different |
| Private-only | No source-type filter | Source types + private-only score | Signal new |
| Hierarchy | Flat sliders | Group/dimension/benchmark shares | Signal new |
| Rank stability | None | 120 perturbations, rank bands | Signal new |
| Benchmark checks | Quality per benchmark | Agreement, coverage, human gap | Signal new |
| Task calculator | Time per task | Editable clock | Signal new |
| Provider spread | OpenRouter uptime/provider metrics | Endpoint cost/time lottery | Signal new |
| Monthly tiers | Cost per task | Light/standard/heavy | Signal new view |
| Harness plans | Plan data, no comparison page | 19 plans, break-even, stacks | Signal new page |
| Model compare | Ranking compare only | Up to 4 models | Signal new |
| Alternate boards | One board + model finder | Six question boards | Signal new view |
| Charts | Pareto, 3D cube, radar, usage, formula | Volume, ternary, time Pareto, human gap, stability, provider lottery | Mixed |

## What Priors already does better

- Data breadth: 356 vs 88; 130 publishers vs 22.
- Depth per model and benchmark: per-effort rows, harness, tokens, leaders.
- Subscription cost: plan resets, free tiers, time-of-day rates, student offers, budget plans.
- Customization and distribution: flat mix, rank flow, model finder, public profiles, 35-tool API, imports/exports.
- Benchmark quality: 0–100 score, recommended sort, version notices.
- 3D Pareto cube, radar, usage stream, custom formula.

## What Signal does differently

- It starts from work and constraints, not a model order.
- It treats source type as a first-class filter.
- It shows uncertainty in the rank, not only in the data.
- It checks the benchmark set for redundancy and gaps.
- It models the task, the endpoint, and the coding-tool plan, not only the model.
- It compares models directly, not only rankings.

---

# Part 3 — What Priors could take

These are the additions that are not already in Priors. Each is optional and additive.

## 1. Private-only scoring

**What it is:** a mode that scores only trusted source types: controlled, independent, provider, modeled. Public benchmarks, human votes, prices, and specs stay visible but excluded.

**Why it fits Priors:** Priors can weight an imported benchmark, but it cannot say “keep the public evidence on the page and out of the score.” This is a different question, not a different weight.

**Reuses:** benchmark catalog, weights, scoring engine.

**Adds:** source-type field, `privateOnly` flag, `IGNORED` state, paused state when no private evidence remains.

**Caveat:** specialist audience; only useful to users with controlled or held-out evidence.

## 2. Capability/parameter hierarchy

**What it is:** weights at three levels — Capability/Human/Practical → 15 parameters → benchmarks — with totals and a resolver.

**Why it fits Priors:** the flat mix is precise but makes users think in benchmark names. Most people think in capabilities.

**Reuses:** flat mix, scoring engine.

**Adds:** `shares` object, hierarchy mode, totals, `Even`/`Scale` resolver, derived flat mix.

**Caveat:** complexity. The flat mix remains the default.

## 3. Guided builder, presets, voice

**What it is:** job → trade-off → benchmark strategy → voice, producing an editable flat mix. Eight presets, four voices.

**Why it fits Priors:** the rank flow derives weights from a model order. This derives them from work and constraints.

**Reuses:** hierarchy, presets as data.

**Adds:** four-step path, preset cards, voice control, open-weights and long-context constraints.

**Caveat:** the rank flow is more precise for experts; this is the novice/portfolio path.

## 4. Rank stability

**What it is:** 120 re-ranks with ±36% log-normal weight jitter; 10th–90th percentile rank bands.

**Why it fits Priors:** Priors shows coverage and fit quality, but not whether the order survives a small change in priorities.

**Reuses:** scoring engine.

**Adds:** seeded simulation, stability chart, current/median/band markers.

**Caveat:** weight sensitivity only; not benchmark noise or statistical confidence.

## 5. Benchmark checks

**What it is:** agreement matrix, coverage heatmap, human gap.

**Why it fits Priors:** the quality score is per benchmark. It does not show when two benchmarks are the same signal, where the cohort’s holes are, or whether the set agrees with human preference.

**Reuses:** parameter scores, coverage, Arena rows.

**Adds:** Pearson agreement, redundant/complementary pairs, model × parameter coverage, Arena vs benchmark gap.

**Caveat:** descriptive, not causal. Shared inputs inflate correlation.

## 6. Task clock, provider spread, monthly tiers, availability

**What it is:** an editable task clock; endpoint-level time/cost; light/standard/heavy monthly cost; measured endpoints, first-party, self-hostable, context.

**Why it fits Priors:** Priors has time per task, cost per task, and provider metrics, but not the calculator, endpoint spread, monthly bill, or availability model.

**Reuses:** time/cost data, OpenRouter metrics.

**Adds:** task profile, breakdown, 100-task projection, provider table, usage tiers, availability facts.

**Caveat:** assumptions need a label; no invented endpoint rows.

## 7. Coding-tool plans and stacks

**What it is:** a tools page comparing Cursor, Copilot, Claude Code, Kiro, etc. by included credits, effective cost per task, break-even tasks, and confidence; plus harness + model + effort stacks.

**Why it fits Priors:** Priors answers “what does this model cost under its lab’s plan?” It does not answer “what does this coding tool cost per task?”

**Reuses:** Priors’ plan data.

**Adds:** plan table, effective cost, break-even, fit notes, stacks.

**Caveat:** highest maintenance; do not replace Priors’ plan data with modeled multipliers.

## 8. Model-vs-model compare

**What it is:** up to four models, head-to-head, dimension and benchmark wins, cost/time, trade-off summary.

**Why it fits Priors:** Priors compares rankings, not models. Users compare models.

**Reuses:** active index, model pages.

**Adds:** compare slots, dimension breakdown, benchmark table, trade-offs.

**Caveat:** keep separate from ranking compare.

## 9. Alternate boards, score breakdown, nearest neighbours

**What it is:** six question boards; a “why this rank” panel; a “close on this index” list.

**Why it fits Priors:** the main board answers one question. These answer the next ones without rebuilding the index.

**Reuses:** existing scores, costs, task clocks, Arena rows, open-weight flags.

**Adds:** value/fastest/cheapest/human/open boards; per-parameter breakdown; nearest models.

**Caveat:** views, not new measurements.

## 10. Charts

**What it is:** ternary, volume field, time Pareto; human gap, rank stability, and provider lottery are already part of the checks above.

**Why it fits Priors:** Priors has Pareto and a 3D cube. These answer different questions: three-way trade-off, weighted volume, time frontier, human divergence, rank fragility, endpoint spread.

**Reuses:** existing dimension scores, cost, time, provider rows.

**Adds:** three new chart tabs plus the charts inside the checks.

**Caveat:** do not duplicate the cost Pareto, radar, usage stream, 3D cube, or custom formula.

---

## What this pitch does not ask for

- A new leaderboard.
- A new scoring model.
- A new data source.
- A redesign, theme, onboarding gate, or marketing copy.
- A coverage penalty as a correction to Priors’ strictness.
- A replacement for Priors’ plan data.
- Any feature Priors already has.

## Closing

Priors is the platform. Signal is the lens.

The useful additions are the ones that change what a user can ask: which evidence to trust, how to set priorities, whether the rank is stable, whether the benchmarks are redundant, what the task actually costs, and which tool plan makes sense.

The rest is already there.

---

**Appendix:** `appendix/SIGNAL-REFERENCE.md` · `appendix/PRIORS-REFERENCE.md` · `appendix/OVERLAP.md` · `appendix/INTEGRATION.md` · `appendix/VERIFICATION.md` · `evidence/README.md`
