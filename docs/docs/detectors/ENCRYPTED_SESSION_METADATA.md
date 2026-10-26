# Encrypted-Session Metadata Detection (TLS/QUIC)

> Implementation status: **PLANNED**. Metrics: **NOT YET MEASURED**. Feature availability depends on sensor placement and mirrored direction (see [../DETECTOR_DESIGN.md](../DETECTOR_DESIGN.md#feature-availability-unidirectional)).

## Threat definition
Potential malware communication hidden in encrypted sessions.

## Detection objective
Flag suspicious sessions from metadata only. No payload inspection and no definitive malware identification.

## Observable data (one-way)
TLS ClientHello fields (SNI, ciphers, extensions, JA3/JA4 client), QUIC initial metadata where visible, packet sizes/timing in the observed direction.

## Required features
Client fingerprint hash/rarity, SNI characteristics, hello size, packet-size/timing sequence, session duration, bytes in observed direction. Server hello, certificate and JA3S are unavailable one-way.

## Proposed algorithm
Gradient boosting on session metadata; rarity/novelty scores for fingerprints.

## Training / calibration data
Public captures with labelled malicious TLS are limited (verify); otherwise benign baseline + synthetic. Reputation data only if a permitted source exists.

## Inference workflow
Window/flow → compute features (with availability mask) → score → compare to threshold → build evidence → emit candidate alert → schema validation.

## Threshold selection
Validation-chosen at target FPR; fingerprint-rarity threshold.

## Confidence interpretation
Heuristic score unless calibration is evaluated. Mark `confidence_type` accordingly.

## Example alert (synthetic)
See [../ALERT_SCHEMA.md](../ALERT_SCHEMA.md); use `threat_class`: as defined for this detector and synthetic IPs (192.0.2.0/24).

## Evaluation methodology
ENCRYPTED_SESSION_METADATA.md0

## Expected failure cases
ENCRYPTED_SESSION_METADATA.md1

## False-positive sources
ENCRYPTED_SESSION_METADATA.md2

## Limitations
ENCRYPTED_SESSION_METADATA.md3
