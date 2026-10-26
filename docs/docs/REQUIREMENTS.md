# Requirements

Priority: M = must, S = should, C = could. Status of all: `PLANNED`.

## Functional
| ID | Requirement | Pri |
|---|---|---|
| FR1 | Read PCAP files and replay deterministically | M |
| FR2 | Assemble packets into flows/windows using only observable direction | M |
| FR3 | Extract features per detector | M |
| FR4 | Implement six detectors | M |
| FR5 | Emit alerts conforming to the alert schema with evidence | M |
| FR6 | Persist alerts and expose via REST API | M |
| FR7 | Dashboard listing alerts, severity, evidence | M |
| FR8 | Directional-blindness evaluation harness | M |
| FR9 | Live mirrored ingestion | C |
| FR10 | Detector metrics endpoint | S |

## Non-functional
| ID | Requirement | Pri |
|---|---|---|
| NFR1 | No network egress from ingestion container (tested) | M |
| NFR2 | No automated blocking or packet injection anywhere | M |
| NFR3 | Reproducible runs (fixed seeds, pinned versions) | M |
| NFR4 | Throughput and p50/p95 latency measured, not assumed | S |
| NFR5 | Graceful handling of malformed packets/fields | M |
| NFR6 | Read-only filesystem for ingestion where feasible | S |

## Constraints
Student-team timeline; public datasets only; no sponsor data; official SIH rules `UNVERIFIED`.
