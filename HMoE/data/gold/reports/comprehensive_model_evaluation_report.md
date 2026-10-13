# H-MoE Customer Segmentation
# Comprehensive Base-Model and MoE Evaluation Report

Generated from the preserved Phase 6-11 manifests and reports. This report
does not replace any historical result.

## 1. Executive summary

| Finding | Result |
|---|---|
| Best legacy base-model geometry | Phase 6 KMeans RFM: silhouette 0.5314, DBI 0.6182, CH 7,213.43 |
| Best frozen multimodal geometry | Phase 9/11 text + temporal fixed-weight fusion: silhouette 0.557928, DBI 0.779689, CH 9,113.616 |
| Best MoE/routing geometry | Fixed behavioral-heavy routing: silhouette 0.374525 |
| Best learned MoE geometry | Quality-aware learned gate: silhouette 0.274782 in the corrected Phase 11 rerun |
| Adaptive-routing conclusion | Not supported; neither learned gate exceeded the strongest fair static baseline |
| Highest corrected retention lift | Phase 6 KMeans RFM: 3.756427x, 4.705882% maximum cluster retention |
| Retention inference caution | Cluster-retention differences are descriptive unless supported by binary-outcome tests and corrected pairwise comparisons |
| Leakage/model-selection audit | No future retention outcomes were used for representation fitting, gate training, clustering selection, or configuration selection |

The strongest overall evidence is therefore **static text + temporal fusion**, not
adaptive routing. The Phase 6 RFM model remains the strongest legacy model for
retention separation and has a much better compact cluster geometry than most
legacy alternatives.

## 2. Common evaluation protocol

| Item | Frozen value |
|---|---|
| Customer cohort | 57,510 |
| Train / validation / test | 40,208 / 8,681 / 8,621 |
| Test customer hash | `98436e8f74505213a9fbb779e68341dcb86c1500d053000f108644806d54e00f` |
| Observation cutoff | Before `2018-03-01T00:00:00` |
| Future retention window | `[2018-03-01T00:00:00, 2018-09-01T00:00:00)` |
| Retention target | `future_is_retained = 1` iff `future_orders_count > 0` |
| Blind-test retention baseline | 108 / 8,621 = **1.252755%** |
| Cohort retention baseline | 684 / 57,510 = **1.189358%** |
| Frozen clustering for Phases 9-11 | KMeans, `k=5`, `n_init=10` |
| Stability seeds | 42, 43, 44, 45, 46 |
| Stability statistic | Mean pairwise label-permutation-invariant ARI |
| Learned preprocessing | Fit on training customers only |
| Test retention use | Downstream evaluation only; not used for fitting or selection |

Phase 6 has heterogeneous model-specific values of `k`, because KMeans and GMM
were selected under their documented validation procedures and HDBSCAN was
transductive. Phases 9-11 use fixed `k=5` to make representation and routing
comparisons fair.

## 3. Representation inventory

| Representation | Dimensions | Cohort / audit result | Evaluation role |
|---|---:|---|---|
| Classical RFM | 3 | Pre-cutoff behavioral features | Phase 6 legacy baseline |
| RFM + behavioral | 7 | Pre-cutoff customer behavior | Phase 6 legacy baseline |
| Selected non-redundant | 8 | Audited pre-cutoff features | Phase 6, temporal and fusion inputs |
| All engineered | 16 | All pre-cutoff ratios/features | Phase 6 legacy baseline |
| Text customer embedding | 384 raw; 32 projected | 22,535 customers with text; 0 non-finite customer embeddings; 0 cutoff violations | Phase 9 static fusion and MoE expert |
| Temporal customer embedding | 32 | 59,427 pre-cutoff events; 57,510 customers; 0 non-finite values; 0 cutoff violations | Phase 9 static fusion and MoE expert |
| Behavioral projected expert | 32 | Train-fitted scaling/PCA | Phase 10 routing expert |
| Text projected expert | 32 | Train-fitted scaling/PCA; availability mask retained | Phase 10 routing expert |
| Temporal projected expert | 32 | Train-fitted scaling/PCA; availability mask retained | Phase 10 routing expert |

The text encoder was `sentence-transformers/all-MiniLM-L6-v2`, revision
`1110a243fdf4706b3f48f1d95db1a4f5529b4d41`, with mean pooling, batch size 64,
maximum sequence length 256, and unnormalized embeddings before downstream
preprocessing.

## 4. Phase 6 legacy base models

### 4.1 Internal clustering and stability metrics

| Model | Algorithm | Feature set | Features | K | Silhouette | DBI | CH | ARI | NMI |
|---|---|---|---:|---:|---:|---:|---:|---:|---:|
| B1 KMeans RFM | KMeans | RFM | 3 | 5 | 0.5314 | 0.6182 | 7,213.43 | 0.9937 | 0.9814 |
| B2 KMeans RFM + behavioral | KMeans | RFM + purchase scale | 7 | 4 | 0.3379 | 1.0759 | 2,691.23 | 0.9998 | 0.9994 |
| B3 KMeans selected non-redundant | KMeans | Audited non-redundant | 8 | 5 | 0.3253 | 1.2518 | 1,865.92 | 0.6034 | 0.7136 |
| B4 KMeans all engineered | KMeans | All pre-cutoff ratios | 16 | 4 | 0.5096 | 1.1484 | 1,646.96 | 0.9996 | 0.9988 |
| B5 GMM | Gaussian mixture | Selected non-redundant | 8 | 7 | 0.0784 | 1.9130 | 930.07 | 0.5582 | 0.6393 |
| B6 HDBSCAN | HDBSCAN | Selected non-redundant | 8 | 6 | 0.1209 | 1.9047 | 1,497.21 | 1.0000 | 1.0000 |
| B7 DEC | Deep embedded clustering | Selected non-redundant | 8 | 5 | 0.1429 | 1.6039 | 1,490.72 | 0.5829 | 0.6600 |

**Interpretation of stability:** B2 and B4 have near-perfect ARI/NMI because
their repeated KMeans fits converge to almost identical partitions. B3 and DEC
are much less stable because their representation/optimization landscape
produces more seed-sensitive partitions. HDBSCAN's perfect value is repeated
fit consistency on the same test matrix; it is not out-of-sample predictive
stability because HDBSCAN is transductive in this evaluation.

### 4.2 Corrected retention results

The corrected lift uses the exact blind-test baseline of 1.252755%, not a
rounded 1.25% baseline. Intervals are Wilson 95% intervals and effect sizes
are Cohen's `h` against the exact test baseline.

| Model | Max cluster | Max retention | Corrected lift | Wilson 95% CI | Cohen's h | Binary omnibus p | Holm-significant pairwise differences |
|---|---:|---:|---:|---|---:|---:|---|
| B1 KMeans RFM | 0 | 4.705882% | 3.756427x | 2.712159%-8.044023% | 0.213015 | <0.00001 | 0 vs 1, 0 vs 2, 0 vs 3 |
| B2 KMeans RFM + behavioral | 3 | 4.330000% | 3.456948x | 2.435139%-7.587089% | 0.194948 | <0.00001 | 0 vs 3, 1 vs 3, 2 vs 3 |
| B3 KMeans selected non-redundant | 2 | 4.650000% | 3.712748x | 2.680387%-7.952558% | 0.210424 | <0.0001 | 0 vs 2, 1 vs 2, 2 vs 3, 2 vs 4 |
| B4 KMeans all engineered | 3 | 4.490000% | 3.583938x | 2.525246%-7.859462% | 0.202697 | <0.0001 | 0 vs 3, 1 vs 3, 2 vs 3 |
| B5 GMM | 2 | 3.350000% | 2.673534x | 2.005399%-5.542806% | 0.143772 | 0.00833 | 2 vs 5 |
| B6 HDBSCAN | 0 | 2.600000% | 2.073353x | 1.195730%-5.549867% | 0.099418 | 0.45444 | None |
| B7 DEC | 3 | 4.650000% | 3.712748x | 2.680387%-7.952558% | 0.210424 | <0.0001 | 0 vs 3, 1 vs 3, 2 vs 3, 3 vs 4 |

ANOVA values are retained for historical comparability, but the binary
chi-square/Fisher/Holm results are the appropriate evidence for binary
retention differences. B3 and DEC have the same maximum rate and lift, but
their saved assignments and cluster summaries were independently generated;
equal maxima do not imply identical partitions.

## 5. Phase 9 static multimodal fusion

All rows below use the same cohort, test population, train-only preprocessing,
and fixed `k=5`. The first group is normalized concatenation; the second group
uses train-fitted 32-dimensional PCA per view, equal fixed weights, and
availability indicators.

| Variant | Fusion protocol | Dim. | Silhouette | DBI | CH | Stability ARI |
|---|---|---:|---:|---:|---:|---:|
| Behavioral only | Normalized concatenation | 8 | 0.417657 | 1.157549 | 3,857.446 | 0.999362 |
| Text only | Normalized concatenation | 385 | 0.624421 | 3.474894 | 1,704.446 | 0.990473 |
| Temporal only | Normalized concatenation | 32 | 0.596058 | 0.663542 | 18,176.656 | 1.000000 |
| Behavioral + text | Normalized concatenation | 393 | 0.217365 | 1.899254 | 1,527.787 | 0.789790 |
| Behavioral + temporal | Normalized concatenation | 40 | 0.329211 | 1.285685 | 3,656.771 | 0.998804 |
| Text + temporal | Normalized concatenation | 417 | 0.412614 | 1.384387 | 3,571.522 | 0.994338 |
| Full three-view | Normalized concatenation | 425 | 0.206452 | 1.821804 | 1,880.265 | 0.999585 |
| Behavioral + text | Projected equal-weight + indicators | 34 | 0.297989 | 1.451636 | 3,872.340 | 0.998484 |
| Behavioral + temporal | Projected equal-weight + indicators | 34 | 0.342977 | 1.128105 | 4,970.821 | 0.994900 |
| **Text + temporal** | **Projected equal-weight + indicators** | **34** | **0.557928** | **0.779689** | **9,113.616** | **1.000000** |
| Full three-view | Projected equal-weight + indicators | 35 | 0.305570 | 1.245361 | 6,564.488 | 0.998652 |

The original Phase 9 text-only result included the availability indicator.
Indicator-free sensitivity was lower, with silhouette 0.476372. This is why
availability handling is reported explicitly.

## 6. Phase 10 MoE and routing variants

Each expert is a 32-dimensional train-fitted projected view. Missing views are
masked and available weights are renormalized. Gate training reconstructs the
mean projected representation using training customers only and does not use
future retention outcomes.

| Routing model | Routing rule | Silhouette | DBI | CH | Stability ARI | Single-view rate | Mean entropy |
|---|---|---:|---:|---:|---:|---:|---:|
| Uniform | Equal weights over available experts | 0.273080 | 1.290308 | 3,805.605 | 0.995613 | 0.000000 | 0.852027 |
| Fixed behavioral-heavy | Fixed 0.6 / 0.2 / 0.2 before masking | 0.374525 | 1.214152 | 3,350.098 | 0.999690 | 0.000000 | 0.714346 |
| Standard learned gate | Learned gate, reconstruction objective | 0.268705 | 1.345548 | 3,795.696 | 0.978325 | 0.000000 | 0.850875 |
| Quality-aware learned gate | Learned gate with expert quality inputs | 0.277735 | 1.336678 | 3,889.770 | 0.997184 | 0.000000 | 0.850666 |

The strongest fair static baseline is projected text + temporal fusion with
silhouette 0.557928. The best learned gate is 0.268705 (Phase 10) or 0.274782
in the corrected Phase 11 rerun, both below the static baseline. Therefore no
adaptive-routing superiority claim is justified.

## 7. Phase 11 ablations and robustness controls

Phase 11 reran the routing comparison with complete retention uncertainty and
binary inference. It also added remove-one-modality controls.

| Ablation | Silhouette | DBI | CH | Stability ARI | Retention omnibus p |
|---|---:|---:|---:|---:|---:|
| A1 Behavioral only | 0.417658 | 1.157437 | 3,857.465 | 0.999687 | 0.0996572680 |
| A2 Text only | 0.509313 | 2.317270 | 486.576 | 0.694995 | 0.2821285984 |
| A3 Temporal only | 0.596058 | 0.663541 | 18,176.656 | 1.000000 | 0.6643222635 |
| A4 Text + temporal fixed weight | 0.557928 | 0.779689 | 9,113.616 | 1.000000 | 0.5072817433 |
| A5 Full static fixed weight | 0.305570 | 1.245361 | 6,564.488 | 0.998652 | 0.2847809816 |
| A6 Uniform routing | 0.273080 | 1.290308 | 3,805.605 | 0.995613 | 0.2470133137 |
| A6 Fixed behavioral-heavy | 0.374525 | 1.214152 | 3,350.098 | 0.999690 | 0.0375008907 |
| A7 Standard learned gate | 0.268705 | 1.345548 | 3,795.696 | 0.978325 | 0.3770395479 |
| A8 Quality-aware learned gate | 0.274782 | 1.342117 | 3,842.340 | 0.998501 | 0.3873133919 |
| A9 Remove behavioral | 0.344392 | 1.234574 | 7,640.951 | 0.987613 | 0.4667946218 |
| A9 Remove text | 0.342977 | 1.128105 | 4,970.821 | 0.994034 | 0.1990559109 |
| A9 Remove temporal | 0.326250 | 1.361327 | 2,799.689 | 0.998855 | 0.2080149655 |

The Phase 11 report contains the full per-cluster retention tables for every
ablation, including Wilson 95% intervals and all Holm-adjusted Fisher
comparisons.

## 8. What the metrics mean

| Metric | Preferred direction | Interpretation |
|---|---:|---|
| Silhouette | Higher | Separation and compactness; higher is better |
| Davies-Bouldin | Lower | Average cluster similarity/separation penalty; lower is better |
| Calinski-Harabasz | Higher | Between-cluster dispersion relative to within-cluster dispersion |
| ARI | Higher | Seed-to-seed agreement, invariant to label permutation |
| NMI | Higher | Seed-to-seed information agreement |
| Retention lift | Higher | Maximum cluster rate divided by exact blind-test baseline |
| Wilson interval | Narrower is more precise | Uncertainty around each cluster's binary retention rate |
| Pearson chi-square | Lower p-value | Evidence that retention is not homogeneous across clusters |
| Holm-adjusted Fisher p-value | Lower p-value | Multiplicity-corrected evidence for a specific cluster pair |
| Mean gate entropy | Context dependent | Lower means more concentrated routing; it is not evidence of predictive superiority |

No single metric should be optimized in isolation. For example, temporal-only
and text + temporal fusion have strong geometry, while the legacy RFM model has
the clearest corrected retention separation. These are different objectives.

## 9. Reproducibility and limitations

| Check | Status |
|---|---|
| Review/customer text embeddings finite | Passed |
| Review cutoff strictly before observation cutoff | Passed |
| Temporal embeddings finite | Passed |
| Train-only standardization/PCA | Passed |
| Same test customers across Phase 9-11 comparisons | Passed |
| Assignment alignment | Passed |
| HDBSCAN interpretation corrected | Passed |
| Binary retention tests and multiplicity correction | Passed |
| Earlier blind-test exploration disclosure | Documented |

Limitations:

1. Phase 6 and Phases 9-11 are not one identical experiment: feature sets,
   dimensionality, `k`, and model families differ.
2. The blind test was explored in earlier phases. The later reports disclose
   this and do not claim a pristine untouched final holdout.
3. Retention events are rare: only 108 retained test customers, so some
   cluster intervals are wide.
4. HDBSCAN is transductive in the saved evaluation.
5. Internal clustering geometry does not establish future-retention
   usefulness by itself.

## 10. Source artifacts and rerun commands

| Artifact | Purpose |
|---|---|
| `data/gold/reports/phase6_corrected_report.md` | Corrected legacy baselines, retention reconciliation, binary tests |
| `data/gold/reports/phase7_text_report.md` | Text embedding provenance and audit |
| `data/gold/reports/phase8_temporal_report.md` | Temporal representation and leakage audit |
| `data/gold/reports/phase9_fusion_report.md` | Static fusion comparison |
| `data/gold/reports/phase10_moe_report.md` | Original MoE routing comparison |
| `data/gold/reports/phase11_analysis_report.md` | Corrected MoE ablations and full retention inference |
| `data/gold/reports/phase11_analysis_manifest.json` | Machine-readable Phase 11 metrics |
| `data/gold/baselines/phase11_ablation_test_assignments.parquet` | Per-customer Phase 11 assignments |

From the `HMoE` project directory:

```powershell
& ..\venv\Scripts\python.exe -m src.phase11_analysis
```

The command regenerates the Phase 11 manifest, report, and assignment artifact
without changing the preserved Phase 6-10 historical artifacts.

