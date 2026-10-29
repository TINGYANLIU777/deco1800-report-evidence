## 4.3 Resolving Technical and Design Problems

The application uses Council event records but must derive its own social-level estimates (Brisbane City Council, n.d.-a, n.d.-b). Early rules combined titles, categories and descriptions and returned the first keyword match. Consequently, “at your own pace” could classify a Zumba class as independent, potentially misleading families seeking limited interaction.

The later implementation applies weighted rules to each field separately. Titles and structured categories generally outweigh descriptions, reducing the influence of incidental wording. This approach keeps decisions inspectable and adjustable. Evidence strength and matched clues are displayed to users. Weak or conflicting evidence receives a provisional L2 classification and is labelled as uncertain; current-main matching excludes unknown evidence from the internal preference score.

Controlled regression cases reproduced the earlier inconsistency: two descriptions produced L1 and L3 in V13, but both produced L3 in the weighted model. This supports the specific technical fix. Real-world accuracy remains unverified; independent human ratings and feedback after attendance are still needed.

Supporting materials: [implementation comparison, test log, screenshots and limitations](README.md). Dataset references: [References](REFERENCES.md).
