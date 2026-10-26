# Problem Statement — SIH26145

> Official wording: `UNVERIFIED`. Copy the exact text from the SIH 2026 portal here. Sponsor requirements below are our interpretation, not official.

## Plain-language explanation
Imagine watching a phone call but only hearing one speaker. You can still learn a lot (who calls, how often, how long, what is said), but you miss the replies. Some high-security networks only allow this one-way view, and the monitoring system must never "speak back".

## Key terms
- **Unidirectional IP traffic:** traffic observed in only one direction (e.g. client→server).
- **Passive monitoring:** observing copies of traffic without injecting, modifying or answering packets.
- **Network TAP:** hardware that copies traffic from a link to a monitoring port.
- **SPAN / mirror port:** switch feature that copies traffic to a monitoring port.
- **Data diode:** hardware that physically permits data flow in one direction only.
- **Isolated analytics enclave:** a segregated environment where analysis runs with no route back to the monitored network.

## Why the system cannot talk back
Sending packets (RSTs, handshake replies, blocks) could leak information, break isolation or violate policy. Therefore detection must be **observation-only**, and alerts go to humans, not to automated blocking.

## Why ordinary IDS can struggle
Many detectors use SYN/SYN-ACK completion, RTT, server responses, NXDOMAIN replies, upload/download ratios and certificate details. These need both directions. Which ones are missing depends on where the mirror sits.

## Problem-to-solution map
| Problem | Why it matters | Proposed solution | Evidence needed | Expected benefit | Remaining limitation |
|---|---|---|---|---|---|
| Missing reverse traffic | Common features unavailable | Feature-availability policy; detectors use only observable features | Directional-blindness experiment | Quantified, honest coverage | Some attacks undetectable one-way |
| No active response allowed | Risk of leakage/policy violation | Read-only ingestion, no egress, alert-only output | Egress test, config review | Safe deployment | Humans must act on alerts |
| Encrypted traffic | No payload visibility | Metadata-only (timing, size, TLS hello fields) | Offline eval on labelled data | Suspicion without decryption | Cannot confirm malware |
| Diverse threats | One model cannot cover all | Six specialised detectors | Per-class metrics | Targeted detection | More components to maintain |
| Analyst trust | Black-box alerts ignored | Evidence features in each alert | Alert review with sample users | Faster triage | Evidence ≠ proof |
| False positives | Alert fatigue | Thresholds on validation data, severity tiers | FPR on benign traffic | Manageable alert volume | Dataset-to-field gap |

## Intended users and deployment (proposed, not claimed)
SOC analysts, network security engineers and researchers at organisations that use TAP/SPAN/diode monitoring. No organisation is claimed to have deployed this.

## Consequences
- Missed threat: undetected botnet, exfiltration or scanning.
- False positive: wasted analyst time, loss of trust.

## Existing approaches and limits
Signature IDS (Snort/Suricata): good for known patterns, weaker on novel behaviour, often assumes full sessions. Flow-based ML IDS on CIC-IDS2017-like features: frequently use bidirectional features. Commercial NDR: capabilities vary; not assessed here (`UNVERIFIED`).
