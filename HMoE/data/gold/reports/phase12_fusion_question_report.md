# Phase 12 Multimodal Fusion Research Question

Research question: **When does multimodal fusion help beyond temporal-only representation?**

All variants use the same 57,510-customer cohort, 8,621 test customers, train-only projection, KMeans k=5, and Euclidean internal metrics.

| Variant | Dim. | Silhouette | Delta vs temporal | DBI | CH | Stability ARI | Delta ARI |
|---|---:|---:|---:|---:|---:|---:|---:|
| temporal_only | 32 | 0.596058 | +0.000000 | 0.663541 | 18176.656 | 1.000000 | +0.000000 |
| text_temporal_availability_aware | 34 | 0.557928 | -0.038130 | 0.779689 | 9113.616 | 1.000000 | +0.000000 |
| text_temporal_indicator_free | 32 | 0.319270 | -0.276788 | 1.270539 | 5502.779 | 0.862250 | -0.137750 |

## Protocol audit

- Stability ARI compares independently refit KMeans test assignments; it is not a comparison to ground-truth labels.
- Every internal metric uses Euclidean geometry on the same test population.
- The availability-aware fusion includes explicit modality indicators.
- The indicator-free sensitivity removes the text availability indicator and zeros unavailable projected text.
- Future retention outcomes were not used for preprocessing, fitting, or selection.

## Retention limitation

The behavioral-heavy retention result is exploratory. Its binary retention finding has not been independently confirmed on a separate outcome holdout. No retention outcome was used in this comparison.

## Decision

Text adds reproducible value beyond temporal geometry only if the indicator-free comparison improves both silhouette and stability. This report records that decision rule before outcome inspection.
