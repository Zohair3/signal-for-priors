# How it fits Priors

A merge map, not an implementation plan.

## Reuse

| Priors piece | Use |
|---|---|
| Scoring engine | All scores; hierarchy and private-only derive inputs |
| Index/profile config | Weights, strictness, required benchmarks, effort matching, estimates |
| Benchmark catalog | Source types, tiers, display-only, coverage |
| Cost/time/plan data | Task clock, monthly tiers, plan comparison |
| Model and benchmark pages | Results, sources, per-effort rows |
| API/MCP | New fields and modes |
| Design system | Existing components and tokens |

## Additive fields

All new fields are nullable or defaulted. Existing configs and links keep working.

| Addition | Field / object | Default |
|---|---|---|
| Source types | `Benchmark.sourceType` | `public` |
| Tiers | `Benchmark.tier` | `core` |
| Display-only | `Benchmark.scored`, `Benchmark.compositeOf` | `true`, none |
| Private-only | `IndexConfig.privateOnly` | `false` |
| Hierarchy | `IndexConfig.shares` | flat mix |
| Stability | derived rank bands | not stored |
| Benchmark checks | derived matrices/points | not stored |
| Task clock | `TaskProfile` | stated defaults |
| Providers | `ProviderEndpoint` | no rows |
| Monthly tiers | `UsageTier` | stated defaults |
| Coding plans | `CodingPlan`, `CodingStack` | no rows |
| Compare | local slots | empty |
| Charts | chart-local weights | equal weights |

## Where each fits

| Addition | Existing surface | New surface | Score impact | Default |
|---|---|---|---|---|
| Private-only | Calculation settings, mix | Toggle + `IGNORED` rows | Only when on | off |
| Hierarchy | Builder | Optional mode | None when flat | flat |
| Guided builder | Builder | Optional path | None until applied | off |
| Presets/voice | Builder | Cards/control | None until applied | off |
| Rank stability | Chart area | Tab | None | off |
| Benchmark checks | Data/methodology | Section/tab | None | off |
| Cost/time/providers | Model page, cost settings | Operating section | None | off |
| Coding plans | — | Tools page | None | off |
| Model compare | `/compare` | Models tab | None | off |
| Alternate boards | Board | Tabs/section | None | off |
| Score breakdown | Model page | Panel | None | off |
| Nearest neighbours | Model page | List | None | off |
| Ternary/volume/time Pareto | Chart tabs | New tabs | None | off |

## Compatibility

1. **Score:** only private-only changes the score, and only while enabled. Everything else is a view or an input.
2. **Flat mix:** remains the engine input. Hierarchy derives a flat mix; it does not replace it.
3. **Missing data:** unchanged. No zero-fill, no new penalty.
4. **Plans:** reuse Priors’ plan data. Do not replace it with modeled multipliers.
5. **API/MCP:** add fields; do not remove or rename existing ones.
6. **Old links/configs:** new fields default; old links still resolve.
7. **Unknown source type:** `public`. Unknown tier: `core`.
8. **Rollback:** every addition is default-off or additive; disabling it restores prior behavior.

## Migration

- Add nullable fields with defaults.
- Backfill only from explicit source metadata; do not guess private/controlled.
- Keep unknown values visible as unknown/public.
- Do not remove or rewrite existing benchmark, model, plan, or score rows.

## What not to merge

- A second scoring engine.
- A coverage penalty as a correction to strictness.
- A replacement for Priors’ plan data.
- A visual redesign, theme, onboarding gate, or marketing copy.
- Duplicate cost Pareto, radar, usage stream, 3D cube, or custom formula.
