# Experiment Plan

Status: `PLANNED`.

| ID | Experiment | Data | Output |
|---|---|---|---|
| E1 | Baseline per-class detection | real datasets | P/R/F1/FPR |
| E2 | Synthetic-class evaluation | synthetic | separate table |
| E3 | Directional blindness A/B/C | same as E1 | Δ table |
| E4 | Replay throughput/latency | fixed PCAPs | flows/s, p50/p95 |
| E5 | Isolation tests | containers | pass/fail logs |
| E6 | Calibration | validation set | reliability curve |

Protocol: fixed seeds; time/family splits; baselines (majority, threshold, logistic regression); thresholds on validation; test once. See [../ML_METHODOLOGY.md](../ML_METHODOLOGY.md).
