# Phase 10 Heterogeneous Mixture-of-Experts Report

All variants use the same 57,510-customer cohort and 8,621-customer test split. Experts are 32-dimensional train-fitted projected views; unavailable views are masked and weights renormalized.

| Routing variant | Silhouette | Davies-Bouldin | Calinski-Harabasz | Stability ARI | Single-view rate | Mean entropy |
|---|---:|---:|---:|---:|---:|---:|
| uniform | 0.273080 | 1.290308 | 3805.605 | 0.995613 | 0.000000 | 0.852027 |
| fixed_behavioral_heavy | 0.374525 | 1.214152 | 3350.098 | 0.999690 | 0.000000 | 0.714346 |
| learned_gate | 0.268705 | 1.345548 | 3795.696 | 0.978325 | 0.000000 | 0.850875 |
| quality_aware_gate | 0.277735 | 1.336678 | 3889.770 | 0.997184 | 0.000000 | 0.850666 |

Gate weight sums have maximum deviation **1.192e-07**.
Strongest Phase 9 static fusion (text + temporal fixed weight) silhouette: **0.557928**.
Neither learned gate exceeds the strongest fair Phase 9 static-fusion baseline; adaptive-routing superiority is not supported by this Phase 10 geometry evaluation.
No future retention labels were used for gate training, routing, or clustering selection.
Phase 11 has not started.
