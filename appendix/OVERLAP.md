# Overlap map

**Checked 18 Nov 2026.** Priors vs Signal, capability by capability.

**Verdicts**

- **Same** — both do it; no contribution.
- **Priors deeper** — both do it; Priors has more data or control.
- **Signal new** — Priors has no public equivalent.
- **Signal different** — Priors has an equivalent, but the approach is materially different.
- **Different object** — same word, different thing (e.g., compare).
- **Skip** — already present.

| Capability | Priors | Signal | Verdict |
|---|---|---|---|
| Benchmark catalog | 356 current, 130 publishers, up to 447 models; categories, quality, recommended | 88 signals, 22 sources, 95 configurations | **Priors deeper** |
| Ranked unit | Model + reasoning effort; exact matching | Model + effort; exact matching | **Same** |
| Scores | Published values; no stretching; missing stays missing | Published values; no invented scores; unrated blank | **Same** |
| Cost per task | Measured cost; subscription-adjusted; API; speed tiers; free tiers | Modeled task cost; subscription/harness effective cost | **Same job, different objects** |
| Custom weights | Flat benchmark mix, 0–70% share; strictness; required; estimates | 3-level hierarchy; presets; voice; coverage penalty; private-only | **Signal different** |
| Missing data | Strictness/coverage floor; effort/peer estimates; renormalization | Coverage penalty; confidence labels; private-only | **Same philosophy, different method** |
| Effort matching | Exact/calibrated/nearest; variant-level | Exact matching; variant-level | **Same** |
| Model pages | 95 benchmarks for Astra; per-effort ranks; category standings; cost/speed; leaders | Model benchmark table; breakdown; calculator; provider section; nearest neighbours | **Priors deeper on data; Signal different on breakdowns** |
| Benchmark pages | Leaderboard; cost; published sub-measures; all results with harness | Benchmark table; catalog passport | **Priors deeper** |
| Compare | Rankings side by side: Spearman, shared top-N, biggest split | Up to 4 models head-to-head: breakdown, practicalities, benchmark table | **Different object** |
| Public profiles | 1,000+ rankings, 119 published, remix | Local index; share links | **Priors deeper** |
| API/MCP/CLI | 35-tool MCP, CLI, HTTP API, import/export, snapshots | None | **Priors deeper** |
| Quality score | 0–100 per benchmark; recommended sort | Tiers/provenance; no quality score | **Priors deeper** |
| Benchmark versioning | Version selector, update notices | Versioned sources; no update notices | **Priors deeper** |
| Model finder | `/model-finder` | Index onboarding | **Priors deeper** |
| Rank flow | Order/pairs, focus, fit, disagreements, estimated share | Guided use-case/trade-off builder | **Signal different** |
| Private-only | No source-type filter; can weight an imported benchmark | Source types; private-only score; visible-but-ignored | **Signal new** |
| Hierarchy | Flat benchmark sliders | Group/dimension/benchmark shares; two modes; resolver | **Signal new** |
| Presets/voice | Focus options; flat weights | 8 job presets; 4 voices | **Signal different** |
| Rank stability | None | 120 jittered re-ranks; 10th–90th bands | **Signal new** |
| Agreement matrix | Quality per benchmark; no pairwise correlation | Pearson matrix; redundant/complementary | **Signal new** |
| Coverage heatmap | Measured share per model; no matrix | Model × dimension matrix | **Signal new** |
| Human gap | Human preference benchmarks; no divergence chart | Arena vs benchmark scatter | **Signal new** |
| Task calculator | Time per task; no editable assumptions | Editable clock with breakdown | **Signal new** |
| Provider lottery | OpenRouter uptime/provider metrics; no endpoint cost/time spread | Endpoint log-log scatter; ranges; table | **Signal new** |
| Monthly tiers | Cost per task; no monthly tier view | Light/standard/heavy monthly equivalent | **Signal new (view)** |
| Availability | Uptime; open/closed | Endpoints, first-party, self-host, max context | **Signal new** |
| Harness plans | Sophisticated plan data, some harness fallbacks; no comparison page | 19 plans/13 harnesses; effective cost; break-even; stacks | **Signal new view** |
| Model compare | Ranking compare only | Up to 4 models | **Signal new** |
| Alternate boards | One board + model finder | 6 question boards | **Signal new (view)** |
| Score breakdown | Inspect a calculation per benchmark | Model-page breakdown | **Signal different** |
| Tiers/source types | Quality score; no source-type field | 4 tiers, 9 source types | **Signal new** |
| Display-only/composite guard | Some defaultWeight 0; no explicit guard | Display-only class; composite rule | **Signal different** |
| Data audit page | Benchmark pages + methodology | Consolidated `/data` | **Signal different** |
| Pareto | Score vs subscription cost; frontier; effort lines; 3D cube | Cost/time Paretos; volume; ternary; provider lottery | **Mixed** |
| Radar | Strengths radar | Strengths radar | **Same** |
| Usage stream | Usage stream | Usage stream | **Same** |
| Custom formula | Yes | Yes | **Same** |
| 3D | True 3D Pareto cube | Volume field (weighted cubes) | **Signal different** |
| Ternary | No | Smart/cheap/fast triangle | **Signal new** |
| Human gap | No | Arena vs benchmark | **Signal new** |
| Stability | No | Rank bands | **Signal new** |
| Provider lottery | No | Endpoint scatter | **Signal new** |

## The short version

- **Priors is the superset** of data, customization, distribution, and plan economics.
- **Signal adds the checks and comparisons Priors does not have**: source types, intent-level index construction, uncertainty, benchmark checks, operating data, and tool-plan costs.
- The only safe proposals are the ones where Priors has **no public equivalent** or a **materially different execution**. Everything else is already there.
