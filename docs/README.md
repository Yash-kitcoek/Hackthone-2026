# SIH26145 — AI-Based Detection of Cyber Threats in Unidirectional IP Traffic

> **Status banner:** These documents were generated **without access to the source repository**. Every capability is `PLANNED` or `UNVERIFIED`, and every metric is `NOT YET MEASURED`. Run the audit in [docs/PROJECT_AUDIT.md](docs/PROJECT_AUDIT.md) first and update statuses.

- **Problem ID:** SIH26145 · **Sponsor:** NTRO · **Category:** Software
- **Theme:** `UNVERIFIED` (check the official SIH 2026 catalogue wording)

## Problem
Some sensitive networks only allow traffic to be *observed* in one direction (TAP, SPAN port, or data diode). Conventional IDS tools often rely on seeing both sides of a conversation. We need to detect threats from one-way copies of traffic, without ever sending anything back.

## Solution (proposed)
A passive-only pipeline: PCAP/flow input → read-only ingestion → parsing → streaming features → six detectors → evidence-based alerts → FastAPI → React dashboard.

Six detector classes: DDoS, botnet beaconing, DGA/DNS tunnelling, encrypted-session metadata anomalies, network scanning, data exfiltration.

## Key differentiators (all PLANNED)
1. Directional-blindness evaluation (bidirectional vs unidirectional vs strict feature availability).
2. Read-only architecture with testable isolation.
3. Evidence-based, explainable alerts.

## Architecture preview
See [docs/diagrams/README.md](docs/diagrams/README.md) (10 Mermaid diagrams).

## Tech stack (proposed)
Python, Scapy or Zeek, scikit-learn/LightGBM, FastAPI, React, Docker. See [docs/TECH_STACK.md](docs/TECH_STACK.md).

## Install / quick start / tests
Commands cannot be verified until the repo is audited. Template steps: [docs/IMPLEMENTATION_GUIDE.md](docs/IMPLEMENTATION_GUIDE.md). Demo: [docs/DEMO_SCRIPT.md](docs/DEMO_SCRIPT.md). Tests: [docs/TESTING_STRATEGY.md](docs/TESTING_STRATEGY.md).

## Current status and results
Implementation: `UNVERIFIED`. Results: `NOT YET MEASURED` — see [docs/RESULTS.md](docs/RESULTS.md).

## Limitations
See [docs/LIMITATIONS_AND_RISKS.md](docs/LIMITATIONS_AND_RISKS.md). No encrypted payload inspection, no definitive malware identification, no active response.

## Documentation index
**Core:** [Audit](docs/PROJECT_AUDIT.md) · [Executive summary](docs/EXECUTIVE_SUMMARY.md) · [Problem](docs/PROBLEM_STATEMENT.md) · [Solution](docs/SOLUTION_OVERVIEW.md) · [Requirements](docs/REQUIREMENTS.md) · [Use cases](docs/USE_CASES.md) · [Architecture](docs/SYSTEM_ARCHITECTURE.md) · [ADRs](docs/ARCHITECTURE_DECISIONS.md) · [Threat model](docs/THREAT_MODEL.md) · [Features](docs/FEATURES.md) · [Innovation](docs/UNIQUE_INNOVATION.md) · [Tech stack](docs/TECH_STACK.md) · [Implementation](docs/IMPLEMENTATION_GUIDE.md) · [Structure](docs/PROJECT_STRUCTURE.md) · [Data flow](docs/DATA_FLOW.md) · [API](docs/API_REFERENCE.md) · [Alert schema](docs/ALERT_SCHEMA.md) · [Config](docs/CONFIGURATION.md) · [Isolation](docs/SECURITY_AND_ISOLATION.md)
**ML/Eval:** [Datasets](docs/DATASETS.md) · [ML methodology](docs/ML_METHODOLOGY.md) · [Detector design](docs/DETECTOR_DESIGN.md) · [Directional blindness](docs/DIRECTIONAL_BLINDNESS_EXPERIMENT.md) · [Testing](docs/TESTING_STRATEGY.md) · [Benchmarks](docs/PERFORMANCE_BENCHMARKS.md) · [Results](docs/RESULTS.md)
**Delivery:** [Limitations](docs/LIMITATIONS_AND_RISKS.md) · [Roadmap](docs/ROADMAP.md) · [Deployment](docs/DEPLOYMENT.md) · [Troubleshooting](docs/TROUBLESHOOTING.md) · [Demo](docs/DEMO_SCRIPT.md) · [PPT](docs/PPT_CONTENT.md) · [Submission checklist](docs/SUBMISSION_CHECKLIST.md) · [Judge Q&A](docs/FAQ_AND_JUDGE_QA.md) · [References](docs/REFERENCES.md) · [Glossary](docs/GLOSSARY.md)
**Detectors:** [DDoS](docs/detectors/DDOS_DETECTION.md) · [Beaconing](docs/detectors/BOTNET_BEACONING.md) · [DGA/DNS](docs/detectors/DGA_AND_DNS_TUNNELLING.md) · [Encrypted metadata](docs/detectors/ENCRYPTED_SESSION_METADATA.md) · [Scanning](docs/detectors/NETWORK_SCANNING.md) · [Exfiltration](docs/detectors/DATA_EXFILTRATION.md)
**Experiments:** [Plan](docs/experiments/EXPERIMENT_PLAN.md) · [Results template](docs/experiments/RESULTS_TEMPLATE.md) · [Reproducibility](docs/experiments/REPRODUCIBILITY.md) · [Diagrams](docs/diagrams/README.md) · [Completeness report](docs/COMPLETENESS_REPORT.md)
