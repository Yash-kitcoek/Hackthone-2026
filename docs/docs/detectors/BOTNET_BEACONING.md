# Botnet Beaconing Detection

> Implementation status: **PLANNED**. Metrics: **NOT YET MEASURED**. Feature availability depends on sensor placement and mirrored direction (see [../DETECTOR_DESIGN.md](../DETECTOR_DESIGN.md#feature-availability-unidirectional)).

## Threat definition
Infected hosts periodically contact command-and-control servers.

## Detection objective
Find highly regular outbound connections to the same destination.

## Observable data (one-way)
Timestamps, destinations, ports, sizes in the observed direction.

## Required features
IAT mean/std/CV, periodicity score (autocorrelation/FFT), jitter, repeat-destination count, small consistent sizes, window duration.

## Proposed algorithm
Statistical periodicity scoring with rule threshold; optional classifier on beacon features.

## Training / calibration data
CTU-13 (verify), synthetic beacons with configurable jitter (labelled synthetic).

## Inference workflow
Window/flow → compute features (with availability mask) → score → compare to threshold → build evidence → emit candidate alert → schema validation.

## Threshold selection
Min number of events, CV and periodicity cut-offs tuned on validation.

## Confidence interpretation
Heuristic score unless calibration is evaluated. Mark `confidence_type` accordingly.

## Example alert (synthetic)
See [../ALERT_SCHEMA.md](../ALERT_SCHEMA.md); use `threat_class`: as defined for this detector and synthetic IPs (192.0.2.0/24).

## Evaluation methodology
BOTNET_BEACONING.md0

## Expected failure cases
BOTNET_BEACONING.md1

## False-positive sources
BOTNET_BEACONING.md2

## Limitations
BOTNET_BEACONING.md3
