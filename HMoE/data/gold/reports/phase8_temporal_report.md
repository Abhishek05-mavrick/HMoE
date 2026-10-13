# Phase 8 Temporal Representation Report

A train-only standardized GRU autoencoder represents ordered pre-cutoff order history. Later-known delivery, review, and final-status fields were excluded.

- Customers: **57,510**
- Events before cutoff: **59,427**
- Customers with history: **57,510**
- Truncated customers: **0**
- Max sequence length: **20**
- Embedding dimension: **32**
- Non-finite embedding values: **0**
- Cutoff violations: **0**

## Fixed-k blind-test comparison

- Behavioral-only test silhouette: **0.399719**
- Temporal-only test silhouette: **0.029728**
- Behavioral + temporal test silhouette: **0.399719**
- Behavioral + temporal minus behavioral-only: **+0.000000**

All views use the same 57,510-customer cohort, the same 8,621 blind-test customers, train-fitted preprocessing, and KMeans with k=5 and n_init=10. The test set was not used to fit preprocessing or select k.

### Stability across seeds

- Behavioral-only mean test ARI across all seed pairs: **0.841149**
- Temporal-only mean test ARI across all seed pairs: **0.320647**
- Behavioral + temporal mean test ARI across all seed pairs: **0.841149**

No temporal representation was selected using future retention labels.
