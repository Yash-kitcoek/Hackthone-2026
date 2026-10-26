# ML Methodology

Status: `PLANNED`. No model has been trained.

## Approach per detector
| Detector | Method | Rationale |
|---|---|---|
| DDoS | Window thresholds + LightGBM on window features | Interpretable baseline first |
| Beaconing | Statistical periodicity (IAT CV, autocorrelation/FFT) + rule score | Little labelled data |
| DGA/DNS | Character n-gram + lexical features → LightGBM/logistic regression | Standard approach |
| Encrypted metadata | Flow/timing/size sequences + hello fields → gradient boosting | Metadata only |
| Scanning | Fan-out rules + optional model | Highly interpretable |
| Exfiltration | Rolling baseline z-score / robust deviation + novelty | Per-host baselines |

## Protocol
1. Fix seeds; pin library versions.
2. Build features only from observable fields (availability mask).
3. Split by time/family (see [DATASETS.md](DATASETS.md)).
4. Baselines: majority class, simple threshold rule, logistic regression.
5. Tune on validation; test once.
6. Metrics: per-class precision, recall, F1, FPR, PR-AUC; confusion matrices.
7. Calibration: reliability curve, Brier score. Until done, label scores `heuristic_score`.
8. Save model + feature list + data hash + config.

## Explainability
Rules: exact thresholds crossed. Trees: feature importance / SHAP (approximate). Do not equate explanation with causation.

## Risks
Dataset shift, label noise, evasion, class imbalance (use stratified/time-aware metrics).
