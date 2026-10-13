# Phase 7 Text Representation Report

A frozen `all-MiniLM-L6-v2` sentence encoder was applied only to non-empty reviews created strictly before the Phase 5 observation cutoff. Customer embeddings are the mean of eligible review embeddings; missing text remains explicitly unavailable.

- Customers: **57,510**
- Customers with text: **22,535**
- Eligible reviews: **54,778**
- Non-empty eligible reviews: **22,973**
- Duplicate review IDs removed: **562**
- Empty eligible reviews: **31,805**
- Embedding model/dimension: `sentence-transformers/all-MiniLM-L6-v2` / `384`
- Model revision: `1110a243fdf4706b3f48f1d95db1a4f5529b4d41`
- Embedding configuration: batch size `64`, max sequence length `256`, mean pooling, normalized embeddings `False`
- Cutoff rule: `review_creation_date < 2018-03-01T00:00:00`

## Embedding audit

- Review-level finite embeddings: **22,973**; non-finite values: **0**
- Customer-level finite embeddings: **22,535**; non-finite values: **0**
- Reviews at or after cutoff: **0**
- Independent mean-pooling mismatches: **0**
- Customer row uniqueness: **True**

No Phase 8, 9, 10, or 11 work was started.
