# Phase 9 Audit Report

## Status

Phase 9 comparability and readiness audit completed. Phase 10 was not started.

## Resolved issues

| ID | Issue | Resolution |
|---|---|---|
| A1 | Full normalized concatenation mean pairwise ARI was absent from the human-readable table. | Recovered from the machine-readable manifest and independently recomputed. |
| A2 | Documented text-only includes an availability indicator. | Retained the original result and added an indicator-free sensitivity result. |
| A3 | Per-cluster profiles and imbalance diagnostics were not previously reported. | Added profiles for behavioral, text-only, temporal-only, and full documented fusion. |

## Frozen evaluation protocol

- Cohort: **57,510** customers
- Train/validation/test: **40,208 / 8,681 / 8,621**
- All experiments use the same ordered test customer IDs and KMeans k=5.
- Standardization and PCA are fit on training customers only.
- Stability uses independent seeds and label-permutation-invariant ARI.

## Key sensitivity

- Documented text-only silhouette: **0.624421**
- Text-only without availability indicator: **0.476372**
- Full normalized fusion mean pairwise ARI: **0.999585**

## Retention protocol

Retention is `future_orders_count > 0` in the future window [2018-03-01, 2018-09-01). Future outcomes were not used to construct representations or select models. Prior test-set exploration is disclosed and no further test-driven tuning was performed.

## Readiness decision

The audit artifacts are complete. Phase 10 should compare adaptive routing against the strongest fair static-fusion baseline and fixed-routing controls, not against a weak baseline. Approval is required before implementation.
