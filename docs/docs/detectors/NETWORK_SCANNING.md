# Network Scanning Detection

> Implementation status: **PLANNED**. Metrics: **NOT YET MEASURED**. Feature availability depends on sensor placement and mirrored direction (see [../DETECTOR_DESIGN.md](../DETECTOR_DESIGN.md#feature-availability-unidirectional)).

## Threat definition
Probing many hosts or ports to find targets.

## Detection objective
Flag sources with abnormal destination fan-out or port sweep.

## Observable data (one-way)
Outbound SYNs/UDP/ICMP, destinations, ports.

## Required features
Unique destination hosts/ports per window, attempt rate, sequential address/port patterns, ratio of ports per host. Failed-connection indicators (RST/ICMP unreachable) are unavailable one-way.

## Proposed algorithm
Threshold rules on fan-out and rate; optional classifier.

## Training / calibration data
CIC-IDS2017 PortScan, UNSW recon (verify); synthetic scans (slow/fast, horizontal/vertical).

## Inference workflow
Window/flow → compute features (with availability mask) → score → compare to threshold → build evidence → emit candidate alert → schema validation.

## Threshold selection
Validation-tuned host/port thresholds per window length.

## Confidence interpretation
Heuristic score unless calibration is evaluated. Mark `confidence_type` accordingly.

## Example alert (synthetic)
See [../ALERT_SCHEMA.md](../ALERT_SCHEMA.md); use `threat_class`: as defined for this detector and synthetic IPs (192.0.2.0/24).

## Evaluation methodology
NETWORK_SCANNING.md0

## Expected failure cases
NETWORK_SCANNING.md1

## False-positive sources
NETWORK_SCANNING.md2

## Limitations
NETWORK_SCANNING.md3
