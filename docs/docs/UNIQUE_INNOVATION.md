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

## 5. Optional tamper-evident alert log (hash chain)
Status: `PLANNED / optional`. Build only after the core detectors and API work. Not the core innovation.

**Idea:** each stored alert carries `prev_hash` and `alert_hash`.
`alert_hash = SHA-256(prev_hash || canonical_json(alert without hash fields))`. The first alert uses a fixed genesis value (64 zeros). Changing, deleting or reordering any stored alert breaks every later hash.

**What it gives:** after-the-fact detection of alert tampering, and integrity evidence for audits.
**What it does not give:**
- It is a hash chain in the existing database, not a distributed ledger or consensus network.
- Someone who can write the database can recompute the whole chain. To be meaningful, the latest head hash must be exported to a place the attacker cannot write (offline record, read-only medium, or signed with a key held outside the enclave). Choice of anchoring: `UNVERIFIED / undecided`.
- It does not prove the alert was *correct*, only that it was not altered after being stored.

**Verification (proposed):** a script `verify_chain` recomputes hashes and reports the first broken index; optional `GET /api/integrity/verify`.
**Tests:** valid chain passes; modified field, deleted row and swapped order each fail at the right index.
