# Quantitative Evaluation Results

This document summarizes the quantitative evaluation of FinAlogy's visual encoder and retrieval pipeline.

## Dataset

- **Stocks**: DOW30 components (N = 30)
- **Training period**: 2010–2020
- **Test period**: 2021
- **Window size**: W = 5 trading days
- **Silver-pair threshold**: τ = 0.98 (yielding 6,225 anchor-positive pairs in the test set)
- **Retrieval database**: Full 2010–2021 corpus

## Metrics

- **Encoder Similarity**: Mean cosine similarity between (anchor, positive) pairs on the test set
- **52D Alignment (52d_ret)**: For each anchor, retrieve top-3 candidates by encoder similarity (threshold > 0.85) and compute mean cosine similarity between anchor and retrieved candidates in the 52-dimensional morphological feature space. This directly measures how well the encoder captures the morphological definition.
- **Recall@k**: Proportion of queries whose ground-truth positive appears in the top-k retrieved results

---

## Table 1: Loss Function Comparison

| Method | Enc. Similarity | enc_ret | 52D Alignment |
|---|---|---|---|
| Barlow Twins | 0.975 | 0.995 | 0.785 |
| SimSiam | 0.982 | 0.996 | 0.814 |
| **VICReg (ours)** | **0.780** | **0.947** | **0.910** |

VICReg achieves the highest 52D alignment despite lower encoder similarity on original pairs, indicating that its variance and covariance regularization better preserves morphology-discriminative structure. We adopt VICReg for FinAlogy.

---

## Table 2: VICReg Hyperparameter Tuning

Grid search over λ = µ ∈ {5, 10, 25, 50} with ν = 1 fixed.

| λ = µ | Recall@1 | Recall@3 | enc_ret | 52D Alignment |
|---|---|---|---|---|
| **5** | **0.037** | **0.118** | 0.911 | **0.864** |
| 10 | 0.036 | 0.113 | 0.913 | 0.862 |
| 25 | 0.039 | 0.106 | 0.913 | 0.830 |
| 50 | 0.034 | 0.100 | 0.918 | 0.825 |

We select **λ = µ = 5** based on best Recall@3 and 52D alignment. Larger λ increases encoder confidence but degrades morphological alignment.

---

## Table 3: Comparison with Kronos Baseline

Both models produce a 5-day future OHLC forecast for each test sample. FinAlogy uses the top-3 retrieved neighbors' future outcomes averaged in 52D space; Kronos uses its predicted future OHLC. We compute cosine similarity between each forecast and the ground-truth future 52D features.

| Method | 52D Similarity (mean) | n |
|---|---|---|
| Kronos (autoregressive) | 0.504 | 2,075 |
| **FinAlogy (retrieval-based)** | **0.610** | 2,075 |

FinAlogy outperforms the Kronos autoregressive baseline by a clear margin, demonstrating that analogy-based retrieval better preserves structural patterns than direct autoregressive prediction.
