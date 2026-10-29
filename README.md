# Section 4.3 — Technical Problem & Supporting Evidence

**Out & About Brisbane · Team JETZ · Tingyan Liu**  
DECO1800 Design Computing Studio 1: Interactive Technology  
Evidence compiled: 29 October 2026

[Read Section 4.3](REPORT-SECTION-4.3.md) · [Evidence index](#3-evidence-index) · [References](REFERENCES.md) · [Versions and capture method](PROVENANCE.md)

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

![Zumba Gold explanation: L3 Guided together, Some evidence, with title and activity-type clues](figure-zumba.png)

**What to look for:** the L3 result, “Some evidence” label and matched title/category clues. These expose the basis of the estimate to the user. This complete Council record differs from the isolated synthetic inputs above.

[Open full-size Figure 1 (E05)](figure-zumba.png)

### Figure 2 — Making uncertainty visible

![Mobile library explanation: provisional L2, A guess, and insufficient listing evidence](figure-uncertainty.png)

**What to look for:** “A guess” and the explanation that the listing lacks activity-format clues. L2 is a fallback; it does not establish the actual interaction requirements of the Bellbowrie mobile library session.

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

## 4. Scope and remaining limitations

- **Technical verification:** the 15 automated checks cover the model and validation-statistics helpers. They are not participant tests or activity observations.
- **Human validation:** the source release's 58-activity rating sheet has no completed rating cells; its historical audit states human validation had not run. Real-world accuracy remains unverified.
- **Capture scope:** the screenshots use an offline release preview. Live data updates, the PHP account backend and Team Zone deployment were not tested in this capture.
- **Version distinction:** later GitHub main, inspected at `eab476f393123480baed57cbe402c3fcd042b066`, excludes unknown evidence from the internal preference-score denominator. Provisional L2 still participates in the maximum social-level filter. See [E07](PROVENANCE.md).
- **Next evaluation:** obtain independent human ratings and test whether intended users understand the explanation and uncertainty labels.

The report should retain the essential reasoning and evaluation; this page supplies the supporting evidence.
