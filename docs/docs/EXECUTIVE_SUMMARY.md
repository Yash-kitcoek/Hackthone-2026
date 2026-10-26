# Executive Summary

**Problem (SIH26145, NTRO):** Detect cyber threats in unidirectional IP traffic, where only one direction of a conversation is observable and the sensor must never transmit back.

**Proposed solution:** A passive, modular detection platform with six detectors (DDoS, beaconing, DGA/DNS tunnelling, encrypted-session metadata, scanning, exfiltration) that emits evidence-based alerts through an API and dashboard.

**Differentiators (planned):**
1. Measure how much detection performance is lost when reverse traffic is unavailable.
2. Read-only architecture with a test that proves no egress from ingestion.
3. Alerts that carry the evidence features that triggered them.

**Honest status:** Documentation baseline only. Implementation, tests and metrics are `UNVERIFIED` / `NOT YET MEASURED`.

**What we will not claim:** perfect accuracy, zero false positives, production readiness, payload inspection, or definitive malware identification.
