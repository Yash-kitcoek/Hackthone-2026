# Directional-Blindness Experiment

Status: `PLANNED`. Results: `NOT YET MEASURED`.

## Question
How much detection performance is lost when only one direction is visible?

## Configurations
| Config | Features allowed | Label |
|---|---|---|
| A — Bidirectional reference | both directions | reference |
| B — Unidirectional | features from permitted direction only | **simulated restriction** |
| C — Strict availability | only features in the availability table marked Yes | **simulated restriction** |

Honesty rule: filtering dataset fields is **not** a hardware data-diode experiment. A real sensor test, if done, is reported separately.

## Controls
Same samples, same time-based split, same preprocessing code path, same model family and tuning budget, same seeds. Rebuild features from PCAP per config rather than dropping CSV columns where possible.

## Metrics per class
Precision, recall, F1, FPR, and Δ(A−B), Δ(A−C), with confidence intervals (bootstrap over time blocks or captures).

## Result table (empty)
| Class | Config | Precision | Recall | F1 | FPR | Δ vs A |
|---|---|---|---|---|---|---|
| DDoS | A/B/C | NOT YET MEASURED | | | | |
| Beaconing | A/B/C | NOT YET MEASURED | | | | |
| DGA/DNS | A/B/C | NOT YET MEASURED | | | | |
| Encrypted metadata | A/B/C | NOT YET MEASURED | | | | |
| Scanning | A/B/C | NOT YET MEASURED | | | | |
| Exfiltration | A/B/C | NOT YET MEASURED | | | | |

Flow: [diagrams/README.md](diagrams/README.md#8-experiment-and-directional-blindness-flow).
