# DGA and DNS Tunnelling Detection

> Implementation status: **PLANNED**. Metrics: **NOT YET MEASURED**. Feature availability depends on sensor placement and mirrored direction (see [../DETECTOR_DESIGN.md](../DETECTOR_DESIGN.md#feature-availability-unidirectional)).

## Threat definition
DGA: malware generates many pseudo-random domains. DNS tunnelling: data hidden in DNS queries.

## Detection objective
Identify suspicious domain names and abnormal query behaviour.

## Observable data (one-way)
DNS query names, types, rate, source (queries only if mirror carries queries).

## Required features
Domain length, character entropy, n-gram scores, digit ratio, label length, subdomain depth, unique-subdomain count per parent domain, query rate, TXT/NULL query share. Response/NXDOMAIN/TTL features are unavailable if responses aren't mirrored.

## Proposed algorithm
Character n-gram + lexical features into LightGBM/logistic regression; rule layer for tunnelling (high label entropy + many unique subdomains).

## Training / calibration data
Public DGA lists + Tranco benign (verify licences); tunnelling data scarce → synthetic lab captures (labelled synthetic).

## Inference workflow
Window/flow → compute features (with availability mask) → score → compare to threshold → build evidence → emit candidate alert → schema validation.

## Threshold selection
Validation-chosen threshold at target FPR; separate thresholds for DGA and tunnelling.

## Confidence interpretation
Heuristic score unless calibration is evaluated. Mark `confidence_type` accordingly.

## Example alert (synthetic)
See [../ALERT_SCHEMA.md](../ALERT_SCHEMA.md); use `threat_class`: as defined for this detector and synthetic IPs (192.0.2.0/24).

## Evaluation methodology
DGA_AND_DNS_TUNNELLING.md0

## Expected failure cases
DGA_AND_DNS_TUNNELLING.md1

## False-positive sources
DGA_AND_DNS_TUNNELLING.md2

## Limitations
DGA_AND_DNS_TUNNELLING.md3
