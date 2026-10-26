# Solution Overview

## Pipeline
PCAP / Flow Input → Read-Only Ingestion → Packet & Flow Parsing → Streaming Feature Extraction → Six Detectors → Confidence & Evidence → Alert Validation/Normalisation → Alert Store / Event Stream → FastAPI → React Dashboard.

Diagram: [diagrams/README.md](diagrams/README.md#1-high-level-system-architecture).

## Modes
- **PCAP replay** (primary, reproducible) — `PLANNED`.
- **Live mirrored traffic** — `PLANNED`, only if safe hardware/permissions exist.

## Six detectors
| # | Detector | Doc |
|---|---|---|
| 1 | DDoS | [detectors/DDOS_DETECTION.md](detectors/DDOS_DETECTION.md) |
| 2 | Botnet beaconing | [detectors/BOTNET_BEACONING.md](detectors/BOTNET_BEACONING.md) |
| 3 | DGA & DNS tunnelling | [detectors/DGA_AND_DNS_TUNNELLING.md](detectors/DGA_AND_DNS_TUNNELLING.md) |
| 4 | Encrypted-session metadata | [detectors/ENCRYPTED_SESSION_METADATA.md](detectors/ENCRYPTED_SESSION_METADATA.md) |
| 5 | Network scanning | [detectors/NETWORK_SCANNING.md](detectors/NETWORK_SCANNING.md) |
| 6 | Data exfiltration | [detectors/DATA_EXFILTRATION.md](detectors/DATA_EXFILTRATION.md) |

## Sensor direction matters
Observable features depend on sensor placement and which direction the mirror exposes. The feature-availability table is in [DETECTOR_DESIGN.md](DETECTOR_DESIGN.md#feature-availability-unidirectional).

## Principles
Passive only · evidence over black-box scores · measured claims only · simplest tool that works (no Kafka/Kubernetes/blockchain/LLM unless justified).

## Expected benefits (to be validated)
Detection under one-way visibility, quantified performance penalty, safe alert-only operation, faster triage.
