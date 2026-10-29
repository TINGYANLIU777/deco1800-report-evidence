# Section 4.3 — Technical Problem & Supporting Evidence

**Out & About Brisbane · Team JETZ · Tingyan Liu**  
DECO1800 Design Computing Studio 1: Interactive Technology  
Evidence compiled: 29 October 2026

[Read Section 4.3](REPORT-SECTION-4.3.md) · [Claim-to-evidence guide](#claim-to-evidence-guide) · [Evidence index](#3-evidence-index) · [References](REFERENCES.md)

This supplementary page follows Section 4.3 in three steps: **the first-match problem → the weighted-rule solution → the regression result and remaining limitations**. Read the section first, then use the guide below to check individual claims.

## Claim-to-evidence guide

| Report paragraph | Claim to check | Supporting material and reading cue |
|---|---|---|
| 1 — Problem | The application derives its own social-level estimates. | [E08: References](REFERENCES.md) distinguishes Council listing data from project-defined ratings. |
| 1 — Problem | “At your own pace” could make the earlier Zumba example L1. | [E01: Earlier code](source-before.txt), lines 76–87; [E03: Case Z1](controlled-cases.json), input and V13 output. |
| 2 — Solution | Titles and categories generally outweigh descriptions. | [E02: Weighted code](source-after.txt), lines 39–44 for default weights and 114–124 for evidence scoring. |
| 2 — Solution | Users can inspect the clues and evidence strength. | [Figure 1](#figure-1--showing-the-reasons-for-an-estimate): matched clues and “Some evidence”. |
| 2 — Uncertainty | Weak or unresolved conflicting evidence receives provisional L2. | [E02](source-after.txt), lines 125–141; [Figure 2](#figure-2--making-uncertainty-visible): “A guess”. |
| 2 — Matching | Unknown social evidence is excluded from the internal score. | [E09: Matching excerpt](source-matching.txt): `estimate.known`, `known` and `assessedWeight`. Applies to the later inspected GitHub version. |
| 3 — Result | Both tested descriptions produce L3 after the change. | [Comparison table](#controlled-comparison) and [E03](controlled-cases.json); [E04](test-results.txt), check 3. |
| 3 — Limitation | Real-world accuracy still needs human evaluation. | [Scope and limitations](#4-scope-and-remaining-limitations); [E07: Provenance](PROVENANCE.md). Automated tests do not establish attendee experience. |

## At a glance

| Question | Finding |
|---|---|
| What problem was addressed? | The original keyword order could label a Zumba class L1 (“Independent”) because its description said “at your own pace”. |
| Why did it matter? | Someone seeking limited interaction could receive a misleading indication of the activity format. This is a design risk, not an observed participant outcome. |
| What changed? | The later model weighs evidence from separate listing fields, explains matched clues and labels uncertain estimates. |
| What was verified? | Two controlled examples become consistent; 15 automated checks passed. The screenshots show the explanation and uncertainty states. |
| What remains unverified? | Accuracy in actual sessions and whether intended users understand or benefit from the estimates. |

**Reading route:** review the comparison below, inspect Figures 1–2, then use the evidence index to check the implementation and test log. Everything needed to inspect these materials is public; no application installation is required.

## 1. Problem, decision and technical result

The V13 estimator combined listing fields and returned the first keyword match. The later implementation instead evaluates each field separately: titles and structured categories generally carry more weight than description text. It sums evidence for each level and returns matched clues and an evidence-strength label. Insufficient or closely conflicting evidence produces a provisional L2.

This makes the decision inspectable and reduces the influence of incidental wording. It remains a project-defined heuristic: Council provides the listings, **not the social-level ratings**. The evidence-strength label is not a measured probability of correctness.

### Controlled comparison

Both synthetic inputs use the title **Zumba Gold®** and activity type **Dancing**; only the description changes.

| Case | Description | Earlier V13 | Weighted model |
|---|---|---|---|
| Z1 | Work at your own pace in a friendly class. | L1 — Independent | L3 — Guided together |
| Z2 | A fun low-impact class. | L3 — Guided together | L3 — Guided together |

**Interpretation:** this reproduces the inconsistency and verifies the specific fix. It does not establish accuracy across real activities. Check the [inputs and outputs (E03)](controlled-cases.json), [earlier code (E01)](source-before.txt) and [weighted code (E02)](source-after.txt).

## 2. Interface evidence

Both figures are local captures of the supplied release, using actual records from its 14 October 2026 Council snapshot. They show the implemented explanation interface. They are not captures of the live Team Zone application or the latest GitHub layout.

### Figure 1 — Showing the reasons for an estimate

![Zumba Gold explanation: L3 Light chat, Some evidence, with title and activity-type clues](figure-zumba.png)

**What to look for:** the L3 result, “Some evidence” label and matched title/category clues. These expose the basis of the estimate to the user. This complete Council record differs from the isolated synthetic inputs above.

**Label note:** the captured interface calls L3 “Light chat”; the model's internal level name is “Guided together”. Both refer to numeric level 3. The report uses L3 to avoid conflating these labels.

[Open full-size Figure 1 (E05)](figure-zumba.png)

### Figure 2 — Making uncertainty visible

![Mobile library explanation: provisional L2, A guess, and insufficient listing evidence](figure-uncertainty.png)

**What to look for:** “A guess” and the explanation that the listing lacks activity-format clues. L2 is a fallback; it does not establish the actual interaction requirements of the Bellbowrie mobile library session.

**Matching clarification:** “no social-match points” means unknown social evidence earns no confirmed contribution. In the later inspected GitHub implementation, it is also removed from the assessed-weight denominator, so it does not act as a zero-score penalty. [E09](source-matching.txt) supports this calculation; the older screenshot alone cannot prove it. The separate maximum-social-level filter still uses the provisional L2 value.

[Open full-size Figure 2 (E06)](figure-uncertainty.png)

## 3. Evidence index

These identifiers can be used when referring to this supplementary material from the report.

| ID | Open evidence | What it supports |
|---|---|---|
| E01 | [Earlier implementation](source-before.txt) | V13 first-match logic, original lines 76–87. |
| E02 | [Weighted implementation](source-after.txt) | Field weights (39–44), scoring (114–124), uncertainty and explanations (125–141). |
| E03 | [Controlled cases](controlled-cases.json) | Synthetic inputs and before/after outputs for Z1–Z2. |
| E04 | [Automated test log](test-results.txt) | 15 passed, 0 failed; check 3 covers the Zumba issue and checks 6–7 cover uncertainty. |
| E05–E06 | [Figure 1](figure-zumba.png) / [Figure 2](figure-uncertainty.png) | Visible explanation and uncertainty states in the release preview. |
| E07 | [Provenance](PROVENANCE.md) | Source versions, hashes, capture conditions and differences from later GitHub main. |
| E08 | [References and attribution](REFERENCES.md) | Dataset sources, team attribution and AI-assistance acknowledgement. |
| E09 | [Unknown-evidence matching excerpt](source-matching.txt) | Later GitHub implementation: unknown social evidence contributes neither earned weight nor assessed weight. |

## 4. Scope and remaining limitations

- **Technical verification:** the 15 automated checks cover the model and validation-statistics helpers. They are not participant tests or activity observations.
- **Human validation:** the source release's 58-activity rating sheet has no completed rating cells; its historical audit states human validation had not run. Real-world accuracy remains unverified.
- **Capture scope:** the screenshots use an offline release preview. Live data updates, the PHP account backend and Team Zone deployment were not tested in this capture.
- **Version distinction:** later GitHub main, inspected at `eab476f393123480baed57cbe402c3fcd042b066`, excludes unknown evidence from the internal preference-score denominator. Provisional L2 still participates in the maximum social-level filter. See [E07](PROVENANCE.md).
- **Next evaluation:** obtain independent human ratings and test whether intended users understand the explanation and uncertainty labels.

The report should retain the essential reasoning and evaluation; this page supplies the supporting evidence.
