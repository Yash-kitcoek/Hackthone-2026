# Limitations and Risks

## Technical limitations
- One-way view removes handshake, RTT, response and ratio features.
- Encrypted traffic: metadata only; cannot confirm malware.
- Public datasets differ from real networks; label issues exist.
- Slow, jittered or low-volume attacks may evade thresholds.
- Docker isolation ≠ hardware data diode.
- Heuristic scores are not calibrated probabilities.

## Project risks
| Risk | Impact | Mitigation |
|---|---|---|
| Time shortage | Fewer detectors | Build order: scan → DDoS → beacon → exfil → DGA → TLS |
| No labelled data for a class | Weak eval | Synthetic, clearly labelled |
| Hardware unavailable | No live test | PCAP replay only, say so |
| High false positives | Low trust | Validation thresholds, severity tiers |
| Scope creep | Unfinished demo | Exclude Kafka/K8s/LLM/blockchain |
| Unverified references | Credibility | Check before slides |

## Not claimed
Perfect accuracy, zero false positives, production readiness, active defence, definitive malware attribution.
