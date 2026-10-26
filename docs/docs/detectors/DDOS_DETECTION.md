# DDoS Detection

> Implementation status: **PLANNED**. Metrics: **NOT YET MEASURED**. Feature availability depends on sensor placement and mirrored direction (see [../DETECTOR_DESIGN.md](../DETECTOR_DESIGN.md#feature-availability-unidirectional)).

## Threat definition
Many sources flooding a target to exhaust resources (volumetric, SYN, UDP/DNS amplification).

## Detection objective
Flag abnormal surges in packet/flow rate toward a destination.

## Observable data (one-way)
Packets, bytes, SYNs, sources, destinations, ports in the observed direction.

## Required features
pps/bps per destination window, unique source count, SYN share of packets, source/destination entropy, change vs rolling baseline.

## Proposed algorithm
Rule baseline (rate and cardinality thresholds) + optional LightGBM on window features.

## Training / calibration data
CIC-IDS2017 DDoS, UNSW-NB15 DoS (verify); synthetic floods labelled synthetic.

## Inference workflow
Window/flow → compute features (with availability mask) → score → compare to threshold → build evidence → emit candidate alert → schema validation.

## Threshold selection
Chosen on validation windows to meet a target FPR; documented per capture.

## Confidence interpretation
Heuristic score unless calibration is evaluated. Mark `confidence_type` accordingly.

## Example alert (synthetic)
See [../ALERT_SCHEMA.md](../ALERT_SCHEMA.md); use `threat_class`: as defined for this detector and synthetic IPs (192.0.2.0/24).

## Evaluation methodology
DDOS_DETECTION.md0

## Expected failure cases
DDOS_DETECTION.md1

## False-positive sources
DDOS_DETECTION.md2

## Limitations
DDOS_DETECTION.md3
