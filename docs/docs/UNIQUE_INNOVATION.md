# Unique Technical Contribution

Novelty is **not asserted** until we survey prior work (`UNVERIFIED`). Judges may ask; see [FAQ_AND_JUDGE_QA.md](FAQ_AND_JUDGE_QA.md).

## 1. Directional-blindness evaluation
Same detector, same samples, three configurations: bidirectional reference, unidirectional (permitted direction only), strict feature-availability. Report per-class precision, recall, F1, FPR and delta. Protocol: [DIRECTIONAL_BLINDNESS_EXPERIMENT.md](DIRECTIONAL_BLINDNESS_EXPERIMENT.md). Restricting dataset fields is a **simulation**, not a hardware data-diode test, and must be labelled so.

## 2. Read-only architecture
Ingestion container on an internal network, no egress, read-only FS, dropped capabilities, no response path. A diagram is not proof; the egress test is. See [SECURITY_AND_ISOLATION.md](SECURITY_AND_ISOLATION.md).

## 3. Evidence-based alerts
Every alert lists the features that triggered it. Schema: [ALERT_SCHEMA.md](ALERT_SCHEMA.md).

## 4. Explainability
Rule-derived evidence is exact; model explanations (e.g. feature importance/SHAP) are approximate. Heuristic scores are not probabilities unless calibration is evaluated.
