# PPT Content Blueprint

Official SIH template, slide count and rules: `UNVERIFIED` — adapt to the real template. Tag every claim as **Implemented / Tested / Proposed / Future**. At the time of writing, everything is **Proposed**.

Forbidden claims: perfect accuracy, zero false positives, production readiness, guaranteed selection, encrypted payload inspection, definitive malware identification, any unmeasured number.

---
### 1. Title
- Message: Passive threat detection when you can only watch one direction.
- Bullets: SIH26145 · NTRO · Software · Team name/members · Theme (verify)
- Visual: logo + one-line tagline
- Notes: "We built a system that detects cyber threats from one-way copies of network traffic."
- Evidence: official problem ID. Don't show: unverified theme wording.

### 2. Problem statement
- Message: Sensitive networks allow observation only, and detection tools often need both directions.
- Bullets: Unidirectional traffic (TAP/SPAN/diode) · No reply packets allowed · Missing handshakes/responses · Six threat types required
- Visual: diagram 1 simplified
- Notes: "Imagine hearing only one side of a phone call."
- Evidence: official statement text.

### 3. Existing problem and significance
- Message: Missed threats and alert fatigue both hurt.
- Bullets: Signature IDS miss novel behaviour · Many ML IDS use bidirectional features · Encrypted traffic hides payload · False positives waste analyst time
- Visual: problem-to-solution table
- Notes: Be careful comparing with products you have not tested.
- Evidence: cited references only.

### 4. Proposed solution
- Message: A passive, modular, evidence-based pipeline.
- Bullets: PCAP/flow in → features → six detectors → alerts → API → dashboard · Read-only · Evidence in every alert
- Visual: diagram 1 or 2
- Notes: Say what is built vs planned.
- Evidence: audit status.

### 5. Users and use cases
- Message: Built for analysts who can't respond actively.
- Bullets: SOC analysts · Network engineers · Researchers · Replay of captured incidents · Triage with evidence
- Visual: use-case table
- Notes: Don't claim any organisation uses it.

### 6. System architecture
- Message: Trust boundaries are explicit and one-way.
- Bullets: Monitored net → TAP → enclave → management · No path back · Read-only query path
- Visual: diagrams 1 and 3
- Evidence: compose file + isolation test.

### 7. Six detection modules
- Message: Each threat has a dedicated detector using only observable features.
- Bullets: DDoS · Beaconing · DGA/DNS tunnelling · Encrypted metadata · Scanning · Exfiltration
- Visual: diagram 5
- Evidence: per-detector status. Don't show: detectors not built.

### 8. Innovation and read-only enforcement
- Message: We measure the cost of one-way visibility and prove isolation by test.
- Bullets: Directional-blindness evaluation · No-egress ingestion · Evidence alerts · Explainability
- Visual: diagram 8 + egress test output
- Notes: Say "simulated restriction" unless hardware was used.
- Evidence: experiment results, test output.

### 9. Datasets and methodology
- Message: Leakage-aware, reproducible evaluation.
- Bullets: CIC-IDS2017, UNSW-NB15, CTU-13, DGA lists (verify) · Time/family splits · Synthetic data labelled separately · Baselines
- Visual: diagram 7
- Evidence: dataset lock file.

### 10. Results
- Message: Only measured numbers appear here.
- Bullets: Per-class P/R/F1/FPR · Latency p50/p95 · Flows/s · Directional penalty
- Visual: table or chart from [RESULTS.md](RESULTS.md)
- Evidence: run logs. If unmeasured, show "in progress" honestly.

### 11. Dashboard and prototype
- Message: Alerts with evidence, in a working UI.
- Bullets: Alert list · Alert detail with evidence · Filters
- Visual: **real** screenshots only
- Evidence: screenshots from the running app.

### 12. Tech stack
- Bullets: Python · Scapy/Zeek · LightGBM/scikit-learn · FastAPI · React · Docker
- Visual: stack diagram. Note: no blockchain/Kafka/K8s/LLM unless verified need.

### 13. Feasibility and plan
- Bullets: Public datasets · Single-host Docker · Phased roadmap · Build order scan→DDoS→beacon→exfil→DGA→TLS
- Visual: diagram 10

### 14. Limitations and risk mitigation
- Bullets: Metadata-only for encrypted · Some features unavailable one-way · Dataset gap vs real nets · Docker ≠ hardware diode
- Visual: limitations table. Mitigations: synthetic labelling, calibration, hardware tests later.

### 15. Future scope
- Bullets: Live sensor tests · Calibration · More datasets · SOC export from management zone only · Hardening

### 16. Impact and conclusion
- Message: A safe, explainable, measured approach to one-way traffic.
- Bullets: Passive · Evidence-based · Honest limits · Reproducible
- Notes: Close with what is done and what is next.
