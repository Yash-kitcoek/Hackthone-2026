# Data Exfiltration Detection

> Implementation status: **PLANNED**. Metrics: **NOT YET MEASURED**. Feature availability depends on sensor placement and mirrored direction (see [../DETECTOR_DESIGN.md](../DETECTOR_DESIGN.md#feature-availability-unidirectional)).

## Threat definition
Unauthorised transfer of large or sensitive data out of the network.

## Detection objective
Flag unusual outbound volume/frequency/destination.

## Observable data (one-way)
Bytes, duration, destinations in the observed direction.

## Required features
Bytes per host per window, z-score/robust deviation vs per-host baseline, transfer duration, destination novelty, off-hours flag, DNS-based volume. Upload/download ratio unavailable one-way.

## Proposed algorithm
Rolling baseline deviation + novelty rule; optional anomaly model.

## Training / calibration data
Benign baselines from datasets/self-captured traffic; synthetic uploads (labelled synthetic). Real exfil labels are scarce (verify).

## Inference workflow
Window/flow → compute features (with availability mask) → score → compare to threshold → build evidence → emit candidate alert → schema validation.

## Threshold selection
Percentile/z-score thresholds from validation baseline; warm-up period defined.

## Confidence interpretation
Heuristic score unless calibration is evaluated. Mark `confidence_type` accordingly.

## Example alert (synthetic)
See [../ALERT_SCHEMA.md](../ALERT_SCHEMA.md); use `threat_class`: as defined for this detector and synthetic IPs (192.0.2.0/24).

## Evaluation methodology
DATA_EXFILTRATION.md0

## Expected failure cases
DATA_EXFILTRATION.md1

## False-positive sources
DATA_EXFILTRATION.md2

## Limitations
DATA_EXFILTRATION.md3
