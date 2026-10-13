# Phase 9 Static Multimodal Fusion Report

All variants use the same **57,510**-customer cohort, including the same **8,621** blind-test customers. Each view is standardized on training customers only, row-normalized, and clustered with KMeans at fixed k=5.

| Variant | Components | Dim. | Silhouette | Davies-Bouldin | Calinski-Harabasz | Stability ARI |
|---|---|---:|---:|---:|---:|---:|
| behavioral_only | behavioral | 8 | 0.417657 | 1.157549 | 3857.446 | 0.999362 |
| text_only | text | 385 | 0.624421 | 3.474894 | 1704.446 | 0.990473 |
| temporal_only | temporal | 32 | 0.596058 | 0.663542 | 18176.656 | 1.000000 |
| behavioral_text | behavioral, text | 393 | 0.217365 | 1.899254 | 1527.787 | 0.789790 |
| behavioral_temporal | behavioral, temporal | 40 | 0.329211 | 1.285685 | 3656.771 | 0.998804 |
| text_temporal | text, temporal | 417 | 0.412614 | 1.384387 | 3571.522 | 0.994338 |
| behavioral_text_temporal | behavioral, text, temporal | 425 | 0.206452 | 1.821804 | 1880.265 | 0.999585 |
| behavioral_text_fixed_weight | behavioral, text | 34 | 0.297989 | 1.451636 | 3872.340 | 0.998484 |
| behavioral_temporal_fixed_weight | behavioral, temporal | 34 | 0.342977 | 1.128105 | 4970.821 | 0.994900 |
| text_temporal_fixed_weight | text, temporal | 34 | 0.557928 | 0.779689 | 9113.616 | 1.000000 |
| behavioral_text_temporal_fixed_weight | behavioral, text, temporal | 35 | 0.305570 | 1.245361 | 6564.488 | 0.998652 |

Text available customers: **22,535**; temporal available customers: **57,510**.

No future retention outcomes were used for preprocessing, fusion weighting, or clustering selection. Phase 10 has not started.
