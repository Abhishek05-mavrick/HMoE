# Phase 6 Corrected Retention Report

This report preserves the original manifest and recalculates every lift from the blind-test assignments.

- Blind-test baseline: **1.252755%** (108/8621)
- Cohort target: **1.189358%** (684/57510)
- Per-cluster intervals: Wilson 95%; effect size: Cohen's h versus the blind-test baseline.
- Binary retention inference: Pearson chi-square omnibus test; pairwise two-sided Fisher exact tests with Holm correction.
- Model selection audit: confirmed no blind-test retention outcomes were used for K/BIC selection.
- HDBSCAN is reported as blind-test transductive and its stability is exact repeated-fit stability, not out-of-sample stability.

| Model | Original lift | Corrected max non-noise lift | Max cluster | 95% CI | Cohen's h |
|---|---:|---:|---:|---|---:|
| Baseline_1_KMeans_RFM | 3.76x | 3.75642702x | 0 | 2.712159%–8.044023% | 0.21301478 |
| Baseline_2_KMeans_RFM_Behavioral | 3.46x | 3.45694809x | 3 | 2.435139%–7.587089% | 0.19494820 |
| Baseline_3_KMeans_RFM_Selected_NonRedundant | 3.71x | 3.71274763x | 2 | 2.680387%–7.952558% | 0.21042362 |
| Baseline_4_KMeans_RFM_All_Engineered | 3.58x | 3.58393802x | 3 | 2.525246%–7.859462% | 0.20269666 |
| Baseline_5_GMM | 2.67x | 2.67353358x | 2 | 2.005399%–5.542806% | 0.14377238 |
| Baseline_6_HDBSCAN | 2.07x | 2.07335257x | 0 | 1.195730%–5.549867% | 0.09941801 |
| Baseline_7_DEC | 3.71x | 3.71274763x | 3 | 2.680387%–7.952558% | 0.21042362 |

## Reproducibility and validation

- Report version: `2.0-corrected`
- Generated at (UTC): `2026-10-13T09:48:22.511517+00:00`
- Source cohort: `data/gold/temporal_customer_cohort.parquet`
- Source assignments: `data/gold/baselines/phase6_baseline_test_assignments.parquet`
- Original manifest preserved at: `data/gold/baselines/phase6_baselines_manifest.json`
- Split counts: `{'train': 40208, 'val': 8681, 'test': 8621}`
- Target count check: `True`
- Retained count check: `True`
- Assignment coverage check: `True`

## K-selection results

| Selection | Candidate results | Selected K | Criterion |
|---|---|---:|---|
| RFM | k=3, inertia=57252.219591549496, silhouette=0.5057, davies_bouldin=0.7013, calinski_harabasz=4987.7682; k=4, inertia=38410.344729782766, silhouette=0.5314, davies_bouldin=0.6634, calinski_harabasz=6047.9398; k=5, inertia=32831.17727221173, silhouette=0.5412, davies_bouldin=0.6507, calinski_harabasz=5799.6246; k=6, inertia=27767.01050207455, silhouette=0.4398, davies_bouldin=0.7246, calinski_harabasz=5664.2985; k=7, inertia=23961.24408599676, silhouette=0.4412, davies_bouldin=0.7664, calinski_harabasz=6424.6113 | 5 | Highest Validation Silhouette Score with Elbow/DBI cross-validation |
| RFM_Selected_NonRedundant | k=3, inertia=231941.9457155615, silhouette=0.3061, davies_bouldin=1.6524, calinski_harabasz=1655.2526; k=4, inertia=205786.08957638068, silhouette=0.2187, davies_bouldin=1.5482, calinski_harabasz=1684.3744; k=5, inertia=178063.0061948782, silhouette=0.3176, davies_bouldin=1.279, calinski_harabasz=1769.2495; k=6, inertia=158941.93487401874, silhouette=0.2585, davies_bouldin=1.2103, calinski_harabasz=1773.8568; k=7, inertia=145948.54204292645, silhouette=0.2676, davies_bouldin=1.1359, calinski_harabasz=1747.5964 | 5 | Highest Validation Silhouette Score with Elbow/DBI cross-validation |
| GMM | k=3, bic=-143693.27, aic=-144046.71, davies_bouldin=1.987; k=4, bic=-158431.33, aic=-158904.95, davies_bouldin=1.7456; k=5, bic=-207447.64, aic=-208041.43, davies_bouldin=1.879; k=6, bic=-226023.81, aic=-226737.77, davies_bouldin=1.9424; k=7, bic=-236797.78, aic=-237631.91, davies_bouldin=1.9584 | 7 | Minimum Bayesian Information Criterion (BIC) |

## Complete model results

| Model | Type | Feature set | Features | K | Silhouette | DBI | CHI | ARI | NMI | Retention ANOVA F | Retention ANOVA p | Spend ANOVA F | Spend ANOVA p | Original max retention | Original lift |
|---|---|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Baseline_1_KMeans_RFM | KMeans | RFM | 3 | 5 | 0.5314 | 0.6182 | 7213.43 | 0.9937 | 0.9814 | 7.2742 | 7.6322082e-06 | 12.8513 | 1.9712289e-10 | 4.710000% | 3.76000000x |
| Baseline_2_KMeans_RFM_Behavioral | KMeans | RFM_Behavioral | 7 | 4 | 0.3379 | 1.0759 | 2691.23 | 0.9998 | 0.9994 | 7.2248 | 7.719025e-05 | 11.4809 | 1.6500724e-07 | 4.330000% | 3.46000000x |
| Baseline_3_KMeans_RFM_Selected_NonRedundant | KMeans | RFM_Selected_NonRedundant | 8 | 5 | 0.3253 | 1.2518 | 1865.92 | 0.6034 | 0.7136 | 6.3845 | 3.9845669e-05 | 12.9022 | 1.7884251e-10 | 4.650000% | 3.71000000x |
| Baseline_4_KMeans_RFM_All_Engineered | KMeans | RFM_All_Engineered | 16 | 4 | 0.5096 | 1.1484 | 1646.96 | 0.9996 | 0.9988 | 7.6744 | 4.0502086e-05 | 13.0318 | 1.7279735e-08 | 4.490000% | 3.58000000x |
| Baseline_5_GMM | GaussianMixture | RFM_Selected_NonRedundant | 8 | 7 | 0.0784 | 1.913 | 930.07 | 0.5582 | 0.6393 | 2.8823 | 0.0083053769 | 5.5447 | 9.5451105e-06 | 3.350000% | 2.67000000x |
| Baseline_6_HDBSCAN | HDBSCAN | RFM_Selected_NonRedundant | 8 | 6 | 0.1209 | 1.9047 | 1497.21 | 1.0 | 1.0 | 0.9385 | 0.45465997 | 2.8385 | 0.014509446 | 2.600000% | 2.07000000x |
| Baseline_7_DEC | DEC | RFM_Selected_NonRedundant | 8 | 5 | 0.1429 | 1.6039 | 1490.72 | 0.5829 | 0.66 | 6.3273 | 4.4290776e-05 | 12.8855 | 1.8464178e-10 | 4.650000% | 3.71000000x |

## Binary retention tests

ANOVA is retained as a descriptive legacy metric, but binary-outcome claims use the chi-square omnibus test and Holm-adjusted two-sided Fisher pairwise tests.

| Model | Chi-square | df | Omnibus p | Pairwise significant after Holm correction |
|---|---:|---:|---:|---|
| Baseline_1_KMeans_RFM | 29.015798 | 4 | 7.7598352e-06 | 0 vs 1 (p=0.00061854287), 0 vs 2 (p=0.0025771708), 0 vs 3 (p=0.0025771708) |
| Baseline_2_KMeans_RFM_Behavioral | 21.630139 | 3 | 7.7872807e-05 | 0 vs 3 (p=0.00099587195), 1 vs 3 (p=0.0049681981), 2 vs 3 (p=0.0049681981) |
| Baseline_3_KMeans_RFM_Selected_NonRedundant | 25.477431 | 4 | 4.0326663e-05 | 0 vs 2 (p=0.0058343194), 1 vs 2 (p=0.0013521536), 2 vs 3 (p=0.0015920632), 2 vs 4 (p=0.015171899) |
| Baseline_4_KMeans_RFM_All_Engineered | 22.972543 | 3 | 4.091869e-05 | 0 vs 3 (p=0.0015635908), 1 vs 3 (p=0.010680051), 2 vs 3 (p=0.031570494) |
| Baseline_5_GMM | 17.273332 | 6 | 0.0083294987 | 2 vs 5 (p=0.018817409) |
| Baseline_6_HDBSCAN | 4.693321 | 5 | 0.45444146 | None |
| Baseline_7_DEC | 25.249808 | 4 | 4.4813329e-05 | 0 vs 3 (p=0.002711768), 1 vs 3 (p=0.00086902364), 2 vs 3 (p=0.002711768), 3 vs 4 (p=0.014265613) |

## Complete per-cluster retention results

### Baseline_1_KMeans_RFM

| Cluster | Customers | Retained | Retention | Wilson 95% CI | Lift vs exact test baseline | Cohen's h |
|---:|---:|---:|---:|---|---:|---:|
| 0 | 255 | 12 | 4.705882% | 2.712159%–8.044023% | 3.75642702x | 0.21301478 |
| 1 | 3128 | 32 | 1.023018% | 0.725592%–1.440593% | 0.81661457x | -0.02168791 |
| 2 | 332 | 1 | 0.301205% | 0.053190%–1.686160% | 0.24043396x | -0.11450367 |
| 3 | 4859 | 63 | 1.296563% | 1.014762%–1.655311% | 1.03496947x | 0.00390535 |
| 4 | 47 | 0 | 0.000000% | 0.000000%–7.555760% | 0.00000000x | -0.22432311 |

Original downstream cluster breakdown (including spend and order metrics):

```json
[
  {
    "cluster": 0,
    "customer_count": 255,
    "retention_rate": 0.047058823529411764,
    "mean_future_spend": 12.899372549019606,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.050980392156862744
  },
  {
    "cluster": 1,
    "customer_count": 3128,
    "retention_rate": 0.010230179028132993,
    "mean_future_spend": 1.7058727621483376,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.010549872122762148
  },
  {
    "cluster": 2,
    "customer_count": 332,
    "retention_rate": 0.0030120481927710845,
    "mean_future_spend": 0.2655120481927711,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.0030120481927710845
  },
  {
    "cluster": 3,
    "customer_count": 4859,
    "retention_rate": 0.01296563078822803,
    "mean_future_spend": 1.610479522535501,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.013994649104754064
  },
  {
    "cluster": 4,
    "customer_count": 47,
    "retention_rate": 0.0,
    "mean_future_spend": 0.0,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.0
  }
]
```

Original pre-cutoff cluster profiles:

```json
[
  {
    "cluster": 0,
    "customer_count": 255,
    "customer_pct": 2.9578935158334296,
    "median_recency_days": 130.3369097222222,
    "mean_frequency_orders": 2.0980392156862746,
    "median_spend": 219.67000000000002,
    "mean_items": 2.3372549019607844,
    "median_installments": 2.5,
    "median_delivery_days": 11.239716435185185,
    "mean_review_score": 4.2202231520223155,
    "future_retention_rate": 0.047058823529411764
  },
  {
    "cluster": 1,
    "customer_count": 3128,
    "customer_pct": 36.28349379422341,
    "median_recency_days": 273.2708622685185,
    "mean_frequency_orders": 1.0,
    "median_spend": 95.505,
    "mean_items": 1.1010230179028133,
    "median_installments": 2.0,
    "median_delivery_days": 10.376435185185185,
    "mean_review_score": 4.157801418439717,
    "future_retention_rate": 0.010230179028132993
  },
  {
    "cluster": 2,
    "customer_count": 332,
    "customer_pct": 3.851061361790976,
    "median_recency_days": 132.67262152777778,
    "mean_frequency_orders": 1.0,
    "median_spend": 652.69,
    "mean_items": 1.3614457831325302,
    "median_installments": 5.0,
    "median_delivery_days": 12.284039351851852,
    "mean_review_score": 4.0,
    "future_retention_rate": 0.0030120481927710845
  },
  {
    "cluster": 3,
    "customer_count": 4859,
    "customer_pct": 56.362370954645634,
    "median_recency_days": 81.18908564814815,
    "mean_frequency_orders": 1.0,
    "median_spend": 98.31,
    "mean_items": 1.0987857583864993,
    "median_installments": 1.0,
    "median_delivery_days": 11.319542824074073,
    "mean_review_score": 4.067061831706183,
    "future_retention_rate": 0.01296563078822803
  },
  {
    "cluster": 4,
    "customer_count": 47,
    "customer_pct": 0.5451803735065538,
    "median_recency_days": 175.22671296296295,
    "mean_frequency_orders": 1.0638297872340425,
    "median_spend": 1944.86,
    "mean_items": 1.7659574468085106,
    "median_installments": 6.0,
    "median_delivery_days": 12.774976851851852,
    "mean_review_score": 3.688888888888889,
    "future_retention_rate": 0.0
  }
]
```

All pairwise binary retention comparisons:

```json
{
  "omnibus_test": "Pearson chi-square test of retention by cluster",
  "omnibus_chi2": 29.01579793,
  "omnibus_degrees_of_freedom": 4,
  "omnibus_p_value": 7.7598352087593e-06,
  "pairwise_test": "Two-sided Fisher exact test",
  "pairwise_correction": "Holm step-down family-wise error correction",
  "pairwise_comparisons": [
    {
      "cluster_a": 0,
      "cluster_b": 1,
      "odds_ratio_a_vs_b": 4.77777778,
      "raw_p_value": 6.185428728731433e-05,
      "holm_adjusted_p_value": 0.0006185428728731434,
      "significant_at_0.05": true
    },
    {
      "cluster_a": 0,
      "cluster_b": 2,
      "odds_ratio_a_vs_b": 16.34567901,
      "raw_p_value": 0.0003083504887326383,
      "holm_adjusted_p_value": 0.0025771708368005604,
      "significant_at_0.05": true
    },
    {
      "cluster_a": 0,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 3.75935724,
      "raw_p_value": 0.00028635231520006226,
      "holm_adjusted_p_value": 0.0025771708368005604,
      "significant_at_0.05": true
    },
    {
      "cluster_a": 0,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": null,
      "raw_p_value": 0.2245495794976676,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 2,
      "odds_ratio_a_vs_b": 3.42118863,
      "raw_p_value": 0.3648665946610442,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 0.78684221,
      "raw_p_value": 0.29166039192844306,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": null,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 2,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 0.22999089,
      "raw_p_value": 0.18928199239887566,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 2,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": null,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 3,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": null,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    }
  ],
  "claim_policy": "A particular cluster difference is called significant only when its Holm-adjusted p-value is below 0.05."
}
```

### Baseline_2_KMeans_RFM_Behavioral

| Cluster | Customers | Retained | Retention | Wilson 95% CI | Lift vs exact test baseline | Cohen's h |
|---:|---:|---:|---:|---|---:|---:|
| 0 | 2714 | 26 | 0.957996% | 0.654602%–1.400023% | 0.76471110x | -0.02825471 |
| 1 | 1259 | 14 | 1.111994% | 0.663536%–1.857878% | 0.88763863x | -0.01302805 |
| 2 | 4394 | 57 | 1.297223% | 1.002644%–1.676886% | 1.03549664x | 0.00396372 |
| 3 | 254 | 11 | 4.330709% | 2.435139%–7.587089% | 3.45694809x | 0.19494820 |

Original downstream cluster breakdown (including spend and order metrics):

```json
[
  {
    "cluster": 0,
    "customer_count": 2714,
    "retention_rate": 0.009579955784819455,
    "mean_future_spend": 1.7846462785556374,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.009579955784819455
  },
  {
    "cluster": 1,
    "customer_count": 1259,
    "retention_rate": 0.011119936457505957,
    "mean_future_spend": 1.24,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.011914217633042097
  },
  {
    "cluster": 2,
    "customer_count": 4394,
    "retention_rate": 0.01297223486572599,
    "mean_future_spend": 1.6714269458352298,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.014110150204824761
  },
  {
    "cluster": 3,
    "customer_count": 254,
    "retention_rate": 0.04330708661417323,
    "mean_future_spend": 10.983622047244095,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.047244094488188976
  }
]
```

Original pre-cutoff cluster profiles:

```json
[
  {
    "cluster": 0,
    "customer_count": 2714,
    "customer_pct": 31.48126667439972,
    "median_recency_days": 275.3276909722222,
    "mean_frequency_orders": 1.005526897568165,
    "median_spend": 84.62,
    "mean_items": 1.0792188651436994,
    "median_installments": 1.0,
    "median_delivery_days": 10.451342592592592,
    "mean_review_score": 4.166419019316494,
    "future_retention_rate": 0.009579955784819455
  },
  {
    "cluster": 1,
    "customer_count": 1259,
    "customer_pct": 14.60387426052662,
    "median_recency_days": 154.46096064814813,
    "mean_frequency_orders": 1.0127084988085782,
    "median_spend": 232.70999999999998,
    "mean_items": 1.2255758538522636,
    "median_installments": 8.0,
    "median_delivery_days": 11.707534722222222,
    "mean_review_score": 4.020833333333334,
    "future_retention_rate": 0.011119936457505957
  },
  {
    "cluster": 2,
    "customer_count": 4394,
    "customer_pct": 50.96856513165526,
    "median_recency_days": 80.04034143518518,
    "mean_frequency_orders": 1.0059171597633136,
    "median_spend": 91.055,
    "mean_items": 1.0912608101957215,
    "median_installments": 1.0,
    "median_delivery_days": 11.227372685185184,
    "mean_review_score": 4.0956980937661,
    "future_retention_rate": 0.01297223486572599
  },
  {
    "cluster": 3,
    "customer_count": 254,
    "customer_pct": 2.946293933418397,
    "median_recency_days": 122.31129629629629,
    "mean_frequency_orders": 1.889763779527559,
    "median_spend": 229.925,
    "mean_items": 2.547244094488189,
    "median_installments": 3.0,
    "median_delivery_days": 10.485260416666666,
    "mean_review_score": 3.885277777777778,
    "future_retention_rate": 0.04330708661417323
  }
]
```

All pairwise binary retention comparisons:

```json
{
  "omnibus_test": "Pearson chi-square test of retention by cluster",
  "omnibus_chi2": 21.63013936,
  "omnibus_degrees_of_freedom": 3,
  "omnibus_p_value": 7.787280679989844e-05,
  "pairwise_test": "Two-sided Fisher exact test",
  "pairwise_correction": "Holm step-down family-wise error correction",
  "pairwise_comparisons": [
    {
      "cluster_a": 0,
      "cluster_b": 1,
      "odds_ratio_a_vs_b": 0.86017219,
      "raw_p_value": 0.7328449884153766,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 2,
      "odds_ratio_a_vs_b": 0.73596752,
      "raw_p_value": 0.2125152451428755,
      "holm_adjusted_p_value": 0.6375457354286265,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 0.21367695,
      "raw_p_value": 0.00016597865900586426,
      "holm_adjusted_p_value": 0.0009958719540351857,
      "significant_at_0.05": true
    },
    {
      "cluster_a": 1,
      "cluster_b": 2,
      "odds_ratio_a_vs_b": 0.85560488,
      "raw_p_value": 0.6689587829163013,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 0.24841183,
      "raw_p_value": 0.0011847254066084962,
      "holm_adjusted_p_value": 0.004968198090443245,
      "significant_at_0.05": true
    },
    {
      "cluster_a": 2,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 0.29033475,
      "raw_p_value": 0.000993639618088649,
      "holm_adjusted_p_value": 0.004968198090443245,
      "significant_at_0.05": true
    }
  ],
  "claim_policy": "A particular cluster difference is called significant only when its Holm-adjusted p-value is below 0.05."
}
```

### Baseline_3_KMeans_RFM_Selected_NonRedundant

| Cluster | Customers | Retained | Retention | Wilson 95% CI | Lift vs exact test baseline | Cohen's h |
|---:|---:|---:|---:|---|---:|---:|
| 0 | 1189 | 14 | 1.177460% | 0.702670%–1.966709% | 0.93989658x | -0.00687329 |
| 1 | 5275 | 62 | 1.175355% | 0.917988%–1.503783% | 0.93821661x | -0.00706848 |
| 2 | 258 | 12 | 4.651163% | 2.680387%–7.952558% | 3.71274763x | 0.21042362 |
| 3 | 1105 | 10 | 0.904977% | 0.492300%–1.657823% | 0.72238981x | -0.03377437 |
| 4 | 794 | 10 | 1.259446% | 0.685521%–2.302724% | 1.00534098x | 0.00060079 |

Original downstream cluster breakdown (including spend and order metrics):

```json
[
  {
    "cluster": 0,
    "customer_count": 1189,
    "retention_rate": 0.011774600504625737,
    "mean_future_spend": 1.517375946173255,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.012615643397813289
  },
  {
    "cluster": 1,
    "customer_count": 5275,
    "retention_rate": 0.011753554502369668,
    "mean_future_spend": 1.6403469194312796,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.012511848341232227
  },
  {
    "cluster": 2,
    "customer_count": 258,
    "retention_rate": 0.046511627906976744,
    "mean_future_spend": 12.74937984496124,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.050387596899224806
  },
  {
    "cluster": 3,
    "customer_count": 1105,
    "retention_rate": 0.00904977375565611,
    "mean_future_spend": 0.7659366515837104,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.00904977375565611
  },
  {
    "cluster": 4,
    "customer_count": 794,
    "retention_rate": 0.012594458438287154,
    "mean_future_spend": 2.4509949622166247,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.013853904282115869
  }
]
```

Original pre-cutoff cluster profiles:

```json
[
  {
    "cluster": 0,
    "customer_count": 1189,
    "customer_pct": 13.791903491474306,
    "median_recency_days": 173.0192361111111,
    "mean_frequency_orders": 1.0,
    "median_spend": 212.32000000000002,
    "mean_items": 1.015138772077376,
    "median_installments": 8.0,
    "median_delivery_days": 11.574166666666667,
    "mean_review_score": 4.388888888888889,
    "future_retention_rate": 0.011774600504625737
  },
  {
    "cluster": 1,
    "customer_count": 5275,
    "customer_pct": 61.18779723929938,
    "median_recency_days": 131.15984953703702,
    "mean_frequency_orders": 1.0,
    "median_spend": 81.63000000000001,
    "mean_items": 1.0036018957345971,
    "median_installments": 1.0,
    "median_delivery_days": 10.114583333333332,
    "mean_review_score": 4.6675338189386055,
    "future_retention_rate": 0.011753554502369668
  },
  {
    "cluster": 2,
    "customer_count": 258,
    "customer_pct": 2.992692263078529,
    "median_recency_days": 128.38619212962962,
    "mean_frequency_orders": 2.0968992248062017,
    "median_spend": 220.76999999999998,
    "mean_items": 2.395348837209302,
    "median_installments": 2.583333333333333,
    "median_delivery_days": 11.244522569444445,
    "mean_review_score": 4.221625344352617,
    "future_retention_rate": 0.046511627906976744
  },
  {
    "cluster": 3,
    "customer_count": 1105,
    "customer_pct": 12.81753856861153,
    "median_recency_days": 132.20453703703703,
    "mean_frequency_orders": 1.0,
    "median_spend": 102.03,
    "mean_items": 1.0171945701357465,
    "median_installments": 2.0,
    "median_delivery_days": 19.177413194444444,
    "mean_review_score": 1.808529945553539,
    "future_retention_rate": 0.00904977375565611
  },
  {
    "cluster": 4,
    "customer_count": 794,
    "customer_pct": 9.210068437536249,
    "median_recency_days": 134.56195601851852,
    "mean_frequency_orders": 1.0,
    "median_spend": 150.83,
    "mean_items": 2.104534005037783,
    "median_installments": 2.0,
    "median_delivery_days": 10.144265046296296,
    "mean_review_score": 3.367667121418827,
    "future_retention_rate": 0.012594458438287154
  }
]
```

All pairwise binary retention comparisons:

```json
{
  "omnibus_test": "Pearson chi-square test of retention by cluster",
  "omnibus_chi2": 25.47743097,
  "omnibus_degrees_of_freedom": 4,
  "omnibus_p_value": 4.03266632957366e-05,
  "pairwise_test": "Two-sided Fisher exact test",
  "pairwise_correction": "Holm step-down family-wise error correction",
  "pairwise_comparisons": [
    {
      "cluster_a": 0,
      "cluster_b": 1,
      "odds_ratio_a_vs_b": 1.00181194,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 2,
      "odds_ratio_a_vs_b": 0.24425532,
      "raw_p_value": 0.0007292899294629551,
      "holm_adjusted_p_value": 0.005834319435703641,
      "significant_at_0.05": true
    },
    {
      "cluster_a": 0,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 1.30468085,
      "raw_p_value": 0.5457281483131883,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 0.93412766,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 2,
      "odds_ratio_a_vs_b": 0.24381354,
      "raw_p_value": 0.0001352153555655162,
      "holm_adjusted_p_value": 0.0013521535556551621,
      "significant_at_0.05": true
    },
    {
      "cluster_a": 1,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 1.30232112,
      "raw_p_value": 0.5318474030594871,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 0.93243814,
      "raw_p_value": 0.8599129224527449,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 2,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 5.34146341,
      "raw_p_value": 0.00017689591177539444,
      "holm_adjusted_p_value": 0.0015920632059785499,
      "significant_at_0.05": true
    },
    {
      "cluster_a": 2,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 3.82439024,
      "raw_p_value": 0.002167414106966203,
      "holm_adjusted_p_value": 0.015171898748763422,
      "significant_at_0.05": true
    },
    {
      "cluster_a": 3,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 0.71598174,
      "raw_p_value": 0.49881661315280124,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    }
  ],
  "claim_policy": "A particular cluster difference is called significant only when its Holm-adjusted p-value is below 0.05."
}
```

### Baseline_4_KMeans_RFM_All_Engineered

| Cluster | Customers | Retained | Retention | Wilson 95% CI | Lift vs exact test baseline | Cohen's h |
|---:|---:|---:|---:|---|---:|---:|
| 0 | 7298 | 85 | 1.164703% | 0.942966%–1.437823% | 0.92971311x | -0.00805913 |
| 1 | 269 | 1 | 0.371747% | 0.065653%–2.075319% | 0.29674377x | -0.10230528 |
| 2 | 809 | 11 | 1.359703% | 0.760905%–2.418246% | 1.08537060x | 0.00942128 |
| 3 | 245 | 11 | 4.489796% | 2.525246%–7.859462% | 3.58393802x | 0.20269666 |

Original downstream cluster breakdown (including spend and order metrics):

```json
[
  {
    "cluster": 0,
    "customer_count": 7298,
    "retention_rate": 0.011647026582625376,
    "mean_future_spend": 1.536749794464237,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.012332145793368046
  },
  {
    "cluster": 1,
    "customer_count": 269,
    "retention_rate": 0.0037174721189591076,
    "mean_future_spend": 0.32769516728624537,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.0037174721189591076
  },
  {
    "cluster": 2,
    "customer_count": 809,
    "retention_rate": 0.013597033374536464,
    "mean_future_spend": 3.0229789864029666,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.014833127317676144
  },
  {
    "cluster": 3,
    "customer_count": 245,
    "retention_rate": 0.044897959183673466,
    "mean_future_spend": 11.387102040816327,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.04897959183673469
  }
]
```

Original pre-cutoff cluster profiles:

```json
[
  {
    "cluster": 0,
    "customer_count": 7298,
    "customer_pct": 84.65375246491126,
    "median_recency_days": 137.30630787037035,
    "mean_frequency_orders": 1.0004110715264456,
    "median_spend": 93.97,
    "mean_items": 1.0030145245272677,
    "median_installments": 2.0,
    "median_delivery_days": 11.020381944444443,
    "mean_review_score": 4.189235085646781,
    "future_retention_rate": 0.011647026582625376
  },
  {
    "cluster": 1,
    "customer_count": 269,
    "customer_pct": 3.120287669643893,
    "median_recency_days": 138.5920486111111,
    "mean_frequency_orders": 1.0223048327137547,
    "median_spend": 802.65,
    "mean_items": 1.1561338289962826,
    "median_installments": 7.0,
    "median_delivery_days": 13.211707175925925,
    "mean_review_score": 4.004,
    "future_retention_rate": 0.0037174721189591076
  },
  {
    "cluster": 2,
    "customer_count": 809,
    "customer_pct": 9.384062173761745,
    "median_recency_days": 134.47668981481482,
    "mean_frequency_orders": 1.065512978986403,
    "median_spend": 148.14,
    "mean_items": 2.0778739184178,
    "median_installments": 2.0,
    "median_delivery_days": 10.258912037037037,
    "mean_review_score": 3.401433691756272,
    "future_retention_rate": 0.013597033374536464
  },
  {
    "cluster": 3,
    "customer_count": 245,
    "customer_pct": 2.841897691683099,
    "median_recency_days": 124.5187037037037,
    "mean_frequency_orders": 1.9020408163265305,
    "median_spend": 223.67000000000002,
    "mean_items": 2.4571428571428573,
    "median_installments": 3.0,
    "median_delivery_days": 10.395509259259258,
    "mean_review_score": 3.9114942528735632,
    "future_retention_rate": 0.044897959183673466
  }
]
```

All pairwise binary retention comparisons:

```json
{
  "omnibus_test": "Pearson chi-square test of retention by cluster",
  "omnibus_chi2": 22.97254281,
  "omnibus_degrees_of_freedom": 3,
  "omnibus_p_value": 4.0918689963859196e-05,
  "pairwise_test": "Two-sided Fisher exact test",
  "pairwise_correction": "Holm step-down family-wise error correction",
  "pairwise_comparisons": [
    {
      "cluster_a": 0,
      "cluster_b": 1,
      "odds_ratio_a_vs_b": 3.15818661,
      "raw_p_value": 0.37428788959108417,
      "holm_adjusted_p_value": 0.9396292339962705,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 2,
      "odds_ratio_a_vs_b": 0.85489583,
      "raw_p_value": 0.6063692196048371,
      "holm_adjusted_p_value": 0.9396292339962705,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 0.25068374,
      "raw_p_value": 0.0002605984721285394,
      "holm_adjusted_p_value": 0.0015635908327712364,
      "significant_at_0.05": true
    },
    {
      "cluster_a": 1,
      "cluster_b": 2,
      "odds_ratio_a_vs_b": 0.27069199,
      "raw_p_value": 0.3132097446654235,
      "holm_adjusted_p_value": 0.9396292339962705,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 0.07937585,
      "raw_p_value": 0.0021360102907526757,
      "holm_adjusted_p_value": 0.010680051453763379,
      "significant_at_0.05": true
    },
    {
      "cluster_a": 2,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 0.29323308,
      "raw_p_value": 0.007892623435095397,
      "holm_adjusted_p_value": 0.03157049374038159,
      "significant_at_0.05": true
    }
  ],
  "claim_policy": "A particular cluster difference is called significant only when its Holm-adjusted p-value is below 0.05."
}
```

### Baseline_5_GMM

| Cluster | Customers | Retained | Retention | Wilson 95% CI | Lift vs exact test baseline | Cohen's h |
|---:|---:|---:|---:|---|---:|---:|
| 0 | 1143 | 12 | 1.049869% | 0.601577%–1.826087% | 0.83804802x | -0.01903662 |
| 1 | 594 | 6 | 1.010101% | 0.463738%–2.186038% | 0.80630378x | -0.02297560 |
| 2 | 418 | 14 | 3.349282% | 2.005399%–5.542806% | 2.67353358x | 0.14377238 |
| 3 | 2737 | 35 | 1.278772% | 0.920914%–1.773202% | 1.02076821x | 0.00232734 |
| 4 | 602 | 6 | 0.996678% | 0.457564%–2.157222% | 0.79558878x | -0.02432244 |
| 5 | 3039 | 33 | 1.085884% | 0.774255%–1.521016% | 0.86679646x | -0.01553260 |
| 6 | 88 | 2 | 2.272727% | 0.625493%–7.912545% | 1.81418350x | 0.07834216 |

Original downstream cluster breakdown (including spend and order metrics):

```json
[
  {
    "cluster": 0,
    "customer_count": 1143,
    "retention_rate": 0.010498687664041995,
    "mean_future_spend": 1.0529746281714785,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.010498687664041995
  },
  {
    "cluster": 1,
    "customer_count": 594,
    "retention_rate": 0.010101010101010102,
    "mean_future_spend": 1.4412794612794613,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.011784511784511785
  },
  {
    "cluster": 2,
    "customer_count": 418,
    "retention_rate": 0.03349282296650718,
    "mean_future_spend": 8.642775119617225,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.03827751196172249
  },
  {
    "cluster": 3,
    "customer_count": 2737,
    "retention_rate": 0.01278772378516624,
    "mean_future_spend": 1.799773474607234,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.013153087321885276
  },
  {
    "cluster": 4,
    "customer_count": 602,
    "retention_rate": 0.009966777408637873,
    "mean_future_spend": 2.1337873754152823,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.009966777408637873
  },
  {
    "cluster": 5,
    "customer_count": 3039,
    "retention_rate": 0.01085883514313919,
    "mean_future_spend": 1.4207634090161236,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.011846001974333662
  },
  {
    "cluster": 6,
    "customer_count": 88,
    "retention_rate": 0.022727272727272728,
    "mean_future_spend": 3.843295454545455,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.022727272727272728
  }
]
```

Original pre-cutoff cluster profiles:

```json
[
  {
    "cluster": 0,
    "customer_count": 1143,
    "customer_pct": 13.258322700382784,
    "median_recency_days": 150.38493055555554,
    "mean_frequency_orders": 1.0,
    "median_spend": 102.03,
    "mean_items": 1.0,
    "median_installments": 3.0,
    "median_delivery_days": 12.902997685185184,
    "mean_review_score": 2.9758983347940404,
    "future_retention_rate": 0.010498687664041995
  },
  {
    "cluster": 1,
    "customer_count": 594,
    "customer_pct": 6.890151954529637,
    "median_recency_days": 161.7866261574074,
    "mean_frequency_orders": 1.0,
    "median_spend": 361.01,
    "mean_items": 1.0,
    "median_installments": 8.0,
    "median_delivery_days": 13.13990162037037,
    "mean_review_score": 3.2810344827586206,
    "future_retention_rate": 0.010101010101010102
  },
  {
    "cluster": 2,
    "customer_count": 418,
    "customer_pct": 4.848625449483818,
    "median_recency_days": 126.7254398148148,
    "mean_frequency_orders": 1.6770334928229664,
    "median_spend": 232.56,
    "mean_items": 2.8636363636363638,
    "median_installments": 2.5,
    "median_delivery_days": 10.94130787037037,
    "mean_review_score": 3.828547008547009,
    "future_retention_rate": 0.03349282296650718
  },
  {
    "cluster": 3,
    "customer_count": 2737,
    "customer_pct": 31.748057069945478,
    "median_recency_days": 138.1028472222222,
    "mean_frequency_orders": 1.0,
    "median_spend": 140.23000000000002,
    "mean_items": 1.0,
    "median_installments": 3.0,
    "median_delivery_days": 10.17515625,
    "mean_review_score": 5.0,
    "future_retention_rate": 0.01278772378516624
  },
  {
    "cluster": 4,
    "customer_count": 602,
    "customer_pct": 6.982948613849901,
    "median_recency_days": 138.02302083333333,
    "mean_frequency_orders": 1.0,
    "median_spend": 152.81,
    "mean_items": 2.0,
    "median_installments": 2.0,
    "median_delivery_days": 10.056909722222223,
    "mean_review_score": 3.6504504504504505,
    "future_retention_rate": 0.009966777408637873
  },
  {
    "cluster": 5,
    "customer_count": 3039,
    "customer_pct": 35.25113095928546,
    "median_recency_days": 126.92886574074073,
    "mean_frequency_orders": 1.0,
    "median_spend": 64.9,
    "mean_items": 1.0,
    "median_installments": 1.0,
    "median_delivery_days": 11.028043981481481,
    "mean_review_score": 4.15718827269516,
    "future_retention_rate": 0.01085883514313919
  },
  {
    "cluster": 6,
    "customer_count": 88,
    "customer_pct": 1.0207632525229091,
    "median_recency_days": 145.8443287037037,
    "mean_frequency_orders": 1.0,
    "median_spend": 0.0,
    "mean_items": 0.0,
    "median_installments": 1.0,
    "median_delivery_days": null,
    "mean_review_score": 1.5061728395061729,
    "future_retention_rate": 0.022727272727272728
  }
]
```

All pairwise binary retention comparisons:

```json
{
  "omnibus_test": "Pearson chi-square test of retention by cluster",
  "omnibus_chi2": 17.27333184,
  "omnibus_degrees_of_freedom": 6,
  "omnibus_p_value": 0.00832949871348199,
  "pairwise_test": "Two-sided Fisher exact test",
  "pairwise_correction": "Holm step-down family-wise error correction",
  "pairwise_comparisons": [
    {
      "cluster_a": 0,
      "cluster_b": 1,
      "odds_ratio_a_vs_b": 1.0397878,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 2,
      "odds_ratio_a_vs_b": 0.30617658,
      "raw_p_value": 0.0031457467547298125,
      "holm_adjusted_p_value": 0.06291493509459625,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 0.81909814,
      "raw_p_value": 0.631206365207625,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 1.05393457,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 5,
      "odds_ratio_a_vs_b": 0.96648179,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 6,
      "odds_ratio_a_vs_b": 0.45623342,
      "raw_p_value": 0.264224608775849,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 2,
      "odds_ratio_a_vs_b": 0.29446064,
      "raw_p_value": 0.010844855754509764,
      "holm_adjusted_p_value": 0.18703481960570206,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 0.7877551,
      "raw_p_value": 0.6862605803752428,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 1.01360544,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 5,
      "odds_ratio_a_vs_b": 0.92949907,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 6,
      "odds_ratio_a_vs_b": 0.43877551,
      "raw_p_value": 0.27616063846167277,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 2,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 2.67524752,
      "raw_p_value": 0.004269690181579611,
      "holm_adjusted_p_value": 0.08112411345001261,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 2,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 3.44224422,
      "raw_p_value": 0.010390823311427893,
      "holm_adjusted_p_value": 0.18703481960570206,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 2,
      "cluster_b": 5,
      "odds_ratio_a_vs_b": 3.15661566,
      "raw_p_value": 0.0008960671166099967,
      "holm_adjusted_p_value": 0.01881740944880993,
      "significant_at_0.05": true
    },
    {
      "cluster_a": 2,
      "cluster_b": 6,
      "odds_ratio_a_vs_b": 1.49009901,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 3,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 1.28670121,
      "raw_p_value": 0.685728854232345,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 3,
      "cluster_b": 5,
      "odds_ratio_a_vs_b": 1.17993406,
      "raw_p_value": 0.5421343011687229,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 3,
      "cluster_b": 6,
      "odds_ratio_a_vs_b": 0.55699482,
      "raw_p_value": 0.3213172941443041,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 4,
      "cluster_b": 5,
      "odds_ratio_a_vs_b": 0.91702257,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 4,
      "cluster_b": 6,
      "odds_ratio_a_vs_b": 0.43288591,
      "raw_p_value": 0.27142379807687206,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 5,
      "cluster_b": 6,
      "odds_ratio_a_vs_b": 0.47205589,
      "raw_p_value": 0.25851246522774396,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    }
  ],
  "claim_policy": "A particular cluster difference is called significant only when its Holm-adjusted p-value is below 0.05."
}
```

### Baseline_6_HDBSCAN

| Cluster | Customers | Retained | Retention | Wilson 95% CI | Lift vs exact test baseline | Cohen's h |
|---:|---:|---:|---:|---|---:|---:|
| noise | 2634 | 36 | 1.366743% | 0.988865%–1.886268% | 1.09098962x | 0.01002833 |
| 0 | 231 | 6 | 2.597403% | 1.195730%–5.549867% | 2.07335257x | 0.09941801 |
| 1 | 625 | 7 | 1.120000% | 0.543565%–2.293630% | 0.89402963x | -0.01226590 |
| 2 | 267 | 3 | 1.123596% | 0.382846%–3.250815% | 0.89689971x | -0.01192451 |
| 3 | 326 | 3 | 0.920245% | 0.313450%–2.670243% | 0.73457737x | -0.03216878 |
| 4 | 839 | 12 | 1.430274% | 0.820040%–2.483245% | 1.14170309x | 0.01543890 |
| 5 | 3699 | 41 | 1.108408% | 0.818119%–1.500140% | 0.88477617x | -0.01337029 |

Original downstream cluster breakdown (including spend and order metrics):

```json
[
  {
    "cluster": 0,
    "customer_count": 231,
    "retention_rate": 0.025974025974025976,
    "mean_future_spend": 6.053160173160173,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.025974025974025976
  },
  {
    "cluster": 1,
    "customer_count": 625,
    "retention_rate": 0.0112,
    "mean_future_spend": 2.17536,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.0128
  },
  {
    "cluster": 2,
    "customer_count": 267,
    "retention_rate": 0.011235955056179775,
    "mean_future_spend": 1.0442322097378278,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.011235955056179775
  },
  {
    "cluster": 3,
    "customer_count": 326,
    "retention_rate": 0.009202453987730062,
    "mean_future_spend": 0.9096319018404908,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.009202453987730062
  },
  {
    "cluster": 4,
    "customer_count": 839,
    "retention_rate": 0.014302741358760428,
    "mean_future_spend": 1.7653992848629319,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.015494636471990465
  },
  {
    "cluster": 5,
    "customer_count": 3699,
    "retention_rate": 0.011084076777507435,
    "mean_future_spend": 1.4550554203838875,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.011895106785617735
  }
]
```

Original pre-cutoff cluster profiles:

```json
[
  {
    "cluster": -1,
    "customer_count": 2634,
    "customer_pct": 30.553300081197076,
    "median_recency_days": 174.37509259259258,
    "mean_frequency_orders": 1.0197418375094913,
    "median_spend": 176.875,
    "mean_items": 1.1066818526955202,
    "median_installments": 4.0,
    "median_delivery_days": 14.661944444444444,
    "mean_review_score": 3.5512840568374395,
    "future_retention_rate": 0.01366742596810934
  },
  {
    "cluster": 0,
    "customer_count": 231,
    "customer_pct": 2.6795035378726366,
    "median_recency_days": 125.37229166666665,
    "mean_frequency_orders": 2.0,
    "median_spend": 213.10000000000002,
    "mean_items": 2.2034632034632033,
    "median_installments": 3.0,
    "median_delivery_days": 11.19449074074074,
    "mean_review_score": 4.1981566820276495,
    "future_retention_rate": 0.025974025974025976
  },
  {
    "cluster": 1,
    "customer_count": 625,
    "customer_pct": 7.249739009395661,
    "median_recency_days": 134.2099074074074,
    "mean_frequency_orders": 1.0,
    "median_spend": 153.32,
    "mean_items": 2.1744,
    "median_installments": 2.0,
    "median_delivery_days": 9.985972222222221,
    "mean_review_score": 3.700174825174825,
    "future_retention_rate": 0.0112
  },
  {
    "cluster": 2,
    "customer_count": 267,
    "customer_pct": 3.0970885048138266,
    "median_recency_days": 96.06799768518518,
    "mean_frequency_orders": 1.0,
    "median_spend": 81.63000000000001,
    "mean_items": 1.0,
    "median_installments": 1.0,
    "median_delivery_days": 13.619270833333331,
    "mean_review_score": 1.0,
    "future_retention_rate": 0.011235955056179775
  },
  {
    "cluster": 3,
    "customer_count": 326,
    "customer_pct": 3.7814638673007774,
    "median_recency_days": 119.19276041666666,
    "mean_frequency_orders": 1.0,
    "median_spend": 74.05,
    "mean_items": 1.0,
    "median_installments": 1.0,
    "median_delivery_days": 12.658726851851851,
    "mean_review_score": 3.0,
    "future_retention_rate": 0.009202453987730062
  },
  {
    "cluster": 4,
    "customer_count": 839,
    "customer_pct": 9.732049646212735,
    "median_recency_days": 138.53024305555556,
    "mean_frequency_orders": 1.0,
    "median_spend": 72.45,
    "mean_items": 1.0,
    "median_installments": 1.0,
    "median_delivery_days": 10.816799768518518,
    "mean_review_score": 4.0,
    "future_retention_rate": 0.014302741358760428
  },
  {
    "cluster": 5,
    "customer_count": 3699,
    "customer_pct": 42.906855353207284,
    "median_recency_days": 115.17167824074073,
    "mean_frequency_orders": 1.0,
    "median_spend": 78.91,
    "mean_items": 1.0,
    "median_installments": 1.0,
    "median_delivery_days": 9.59554398148148,
    "mean_review_score": 4.9998447204968945,
    "future_retention_rate": 0.011084076777507435
  }
]
```

HDBSCAN stability audit:

```json
{
  "method": "three repeated fits on the identical blind-test feature matrix",
  "mean_pairwise_ari": 1.0,
  "mean_pairwise_nmi": 1.0,
  "pairwise_ari": [
    1.0,
    1.0,
    1.0
  ],
  "pairwise_nmi": [
    1.0,
    1.0,
    1.0
  ],
  "identical_assignments_all_pairs": true,
  "interpretation": "Exact repeatability on the same test matrix; not seed robustness or out-of-sample stability."
}
```

All pairwise binary retention comparisons:

```json
{
  "omnibus_test": "Pearson chi-square test of retention by cluster",
  "omnibus_chi2": 4.69332062,
  "omnibus_degrees_of_freedom": 5,
  "omnibus_p_value": 0.4544414602404031,
  "pairwise_test": "Two-sided Fisher exact test",
  "pairwise_correction": "Holm step-down family-wise error correction",
  "pairwise_comparisons": [
    {
      "cluster_a": 0,
      "cluster_b": 1,
      "odds_ratio_a_vs_b": 2.35428571,
      "raw_p_value": 0.12422617449819327,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 2,
      "odds_ratio_a_vs_b": 2.34666667,
      "raw_p_value": 0.3144903565619449,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 2.87111111,
      "raw_p_value": 0.1727815564457491,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 1.83777778,
      "raw_p_value": 0.24615244849329776,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 5,
      "odds_ratio_a_vs_b": 2.37918699,
      "raw_p_value": 0.05505724606971251,
      "holm_adjusted_p_value": 0.8258586910456877,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 2,
      "odds_ratio_a_vs_b": 0.99676375,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 1.21952535,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 0.78060949,
      "raw_p_value": 0.6489778617572755,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 5,
      "odds_ratio_a_vs_b": 1.010577,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 2,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 1.22348485,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 2,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 0.78314394,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 2,
      "cluster_b": 5,
      "odds_ratio_a_vs_b": 1.01385809,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 3,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 0.64009288,
      "raw_p_value": 0.5778928995357426,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 3,
      "cluster_b": 5,
      "odds_ratio_a_vs_b": 0.8286642,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 4,
      "cluster_b": 5,
      "odds_ratio_a_vs_b": 1.29459994,
      "raw_p_value": 0.47505203784284566,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    }
  ],
  "claim_policy": "A particular cluster difference is called significant only when its Holm-adjusted p-value is below 0.05."
}
```

### Baseline_7_DEC

| Cluster | Customers | Retained | Retention | Wilson 95% CI | Lift vs exact test baseline | Cohen's h |
|---:|---:|---:|---:|---|---:|---:|
| 0 | 2330 | 28 | 1.201717% | 0.832733%–1.731343% | 0.95925926x | -0.00463592 |
| 1 | 2881 | 30 | 1.041305% | 0.730378%–1.482619% | 0.83121216x | -0.01987853 |
| 2 | 2351 | 28 | 1.190983% | 0.825284%–1.715926% | 0.95069080x | -0.00562323 |
| 3 | 258 | 12 | 4.651163% | 2.680387%–7.952558% | 3.71274763x | 0.21042362 |
| 4 | 801 | 10 | 1.248439% | 0.679519%–2.282737% | 0.99655523x | -0.00038833 |

Original downstream cluster breakdown (including spend and order metrics):

```json
[
  {
    "cluster": 0,
    "customer_count": 2330,
    "retention_rate": 0.01201716738197425,
    "mean_future_spend": 1.3938454935622318,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.013304721030042918
  },
  {
    "cluster": 1,
    "customer_count": 2881,
    "retention_rate": 0.010413051023950017,
    "mean_future_spend": 1.221464769177369,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.011107254425546685
  },
  {
    "cluster": 2,
    "customer_count": 2351,
    "retention_rate": 0.011909825606125054,
    "mean_future_spend": 1.9296682262866864,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.011909825606125054
  },
  {
    "cluster": 3,
    "customer_count": 258,
    "retention_rate": 0.046511627906976744,
    "mean_future_spend": 12.74937984496124,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.050387596899224806
  },
  {
    "cluster": 4,
    "customer_count": 801,
    "retention_rate": 0.012484394506866416,
    "mean_future_spend": 2.4295755305867663,
    "median_future_spend": 0.0,
    "mean_future_orders": 0.01373283395755306
  }
]
```

Original pre-cutoff cluster profiles:

```json
[
  {
    "cluster": 0,
    "customer_count": 2330,
    "customer_pct": 27.027027027027028,
    "median_recency_days": 54.340439814814815,
    "mean_frequency_orders": 1.0,
    "median_spend": 87.125,
    "mean_items": 1.0017167381974248,
    "median_installments": 1.0,
    "median_delivery_days": 10.942962962962962,
    "mean_review_score": 5.0,
    "future_retention_rate": 0.01201716738197425
  },
  {
    "cluster": 1,
    "customer_count": 2881,
    "customer_pct": 33.41839693771024,
    "median_recency_days": 142.48902777777778,
    "mean_frequency_orders": 1.0,
    "median_spend": 100.08,
    "mean_items": 1.01041305102395,
    "median_installments": 2.0,
    "median_delivery_days": 12.894837962962962,
    "mean_review_score": 2.994967025338424,
    "future_retention_rate": 0.010413051023950017
  },
  {
    "cluster": 2,
    "customer_count": 2351,
    "customer_pct": 27.27061825774272,
    "median_recency_days": 236.08274305555554,
    "mean_frequency_orders": 1.0,
    "median_spend": 105.28,
    "mean_items": 1.006380263717567,
    "median_installments": 3.0,
    "median_delivery_days": 9.727141203703702,
    "mean_review_score": 5.0,
    "future_retention_rate": 0.011909825606125054
  },
  {
    "cluster": 3,
    "customer_count": 258,
    "customer_pct": 2.992692263078529,
    "median_recency_days": 128.38619212962962,
    "mean_frequency_orders": 2.0968992248062017,
    "median_spend": 220.76999999999998,
    "mean_items": 2.395348837209302,
    "median_installments": 2.583333333333333,
    "median_delivery_days": 11.244522569444445,
    "mean_review_score": 4.221625344352617,
    "future_retention_rate": 0.046511627906976744
  },
  {
    "cluster": 4,
    "customer_count": 801,
    "customer_pct": 9.291265514441479,
    "median_recency_days": 134.47668981481482,
    "mean_frequency_orders": 1.0,
    "median_spend": 150.60000000000002,
    "mean_items": 2.1036204744069913,
    "median_installments": 2.0,
    "median_delivery_days": 10.198217592592592,
    "mean_review_score": 3.3516260162601625,
    "future_retention_rate": 0.012484394506866416
  }
]
```

All pairwise binary retention comparisons:

```json
{
  "omnibus_test": "Pearson chi-square test of retention by cluster",
  "omnibus_chi2": 25.24980849,
  "omnibus_degrees_of_freedom": 4,
  "omnibus_p_value": 4.4813329261670086e-05,
  "pairwise_test": "Two-sided Fisher exact test",
  "pairwise_correction": "Holm step-down family-wise error correction",
  "pairwise_comparisons": [
    {
      "cluster_a": 0,
      "cluster_b": 1,
      "odds_ratio_a_vs_b": 1.15592239,
      "raw_p_value": 0.597588821269651,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 2,
      "odds_ratio_a_vs_b": 1.0091225,
      "raw_p_value": 1.0,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 0,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 0.24934839,
      "raw_p_value": 0.00032494707105244666,
      "holm_adjusted_p_value": 0.0027117679692354735,
      "significant_at_0.05": true
    },
    {
      "cluster_a": 0,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 0.9621199,
      "raw_p_value": 0.853914990177118,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 2,
      "odds_ratio_a_vs_b": 0.87300195,
      "raw_p_value": 0.6908481670934139,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 1,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 0.21571378,
      "raw_p_value": 8.690236426477195e-05,
      "holm_adjusted_p_value": 0.0008690236426477196,
      "significant_at_0.05": true
    },
    {
      "cluster_a": 1,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 0.83233953,
      "raw_p_value": 0.5681362572563164,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 2,
      "cluster_b": 3,
      "odds_ratio_a_vs_b": 0.24709427,
      "raw_p_value": 0.0003013075521372748,
      "holm_adjusted_p_value": 0.0027117679692354735,
      "significant_at_0.05": true
    },
    {
      "cluster_a": 2,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 0.9534223,
      "raw_p_value": 0.8529999645451768,
      "holm_adjusted_p_value": 1.0,
      "significant_at_0.05": false
    },
    {
      "cluster_a": 3,
      "cluster_b": 4,
      "odds_ratio_a_vs_b": 3.85853659,
      "raw_p_value": 0.002037944695435357,
      "holm_adjusted_p_value": 0.0142656128680475,
      "significant_at_0.05": true
    }
  ],
  "claim_policy": "A particular cluster difference is called significant only when its Holm-adjusted p-value is below 0.05."
}
```

## Assignment audits

```json
{
  "source_file": "data/gold/baselines/phase6_baseline_test_assignments.parquet",
  "b3_dec": {
    "exact_assignment_arrays_equal": false,
    "b3_cluster_counts": {
      "0": 1189,
      "1": 5275,
      "2": 258,
      "3": 1105,
      "4": 794
    },
    "dec_cluster_counts": {
      "0": 2330,
      "1": 2881,
      "2": 2351,
      "3": 258,
      "4": 801
    },
    "retention_summaries_equal": false,
    "generation_independence": {
      "status": "confirmed_from_source",
      "evidence": [
        "B3 is generated by the KMeans branch with X_train/X_test for the selected non-redundant feature set.",
        "DEC is generated by the DEC training branch with a separately trained neural model.",
        "The saved parquet contains separate columns for B3 and DEC."
      ]
    }
  }
}
```

## Model-selection leakage audit

Status: **confirmed_no_blind_test_retention_outcomes_used**

- K selection is performed with X_train and X_val only.
- GMM BIC/AIC selection is performed with X_train and X_val only.
- Future retention columns are not feature columns and are evaluated only after test assignments are produced.

Caveat: HDBSCAN is transductive: sklearn HDBSCAN is fit_predict on X_test because it has no out-of-sample predict method.

The JSON file contains the same information in machine-readable form.
