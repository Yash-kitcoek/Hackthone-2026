# Datasets

> **None of the URLs, licences or label details below were verified** (no internet access during authoring). Verify each before use. "Actual usage" = NOT USED until the team runs it.

| Dataset | Source URL (verify) | Threat classes | Format | Labels | Direction info | Known limitations | Licence | Planned preprocessing | Usage |
|---|---|---|---|---|---|---|---|---|---|
| CIC-IDS2017 | https://www.unb.ca/cic/datasets/ids-2017.html | DDoS, scanning, botnet (Ares), exfil-like (infiltration) | PCAP + CSV flows | per-flow attack labels | Flows have fwd/bwd fields; PCAP both directions | Known label/flow-construction issues reported in literature (`UNVERIFIED` — check Engelen et al.) | Check site terms | Rebuild features from PCAP; time split | NOT USED |
| UNSW-NB15 | https://research.unsw.edu.au/projects/unsw-nb15-dataset | DoS, recon/scan, backdoor, generic | PCAP + CSV | attack category | both | Synthetic testbed; dated | Check site terms | Time split | NOT USED |
| CTU-13 | https://www.stratosphereips.org/datasets-ctu13 | Botnet beaconing | PCAP / NetFlow | botnet labels | both | Older botnets | Check terms | Beacon features | NOT USED |
| Public DGA lists | e.g. Bambenek, 360 Netlab feeds `UNVERIFIED` | DGA | CSV domains | DGA family | n/a | Feed licences vary | Check | Family-based split | NOT USED |
| Benign domains | Tranco list https://tranco-list.eu `UNVERIFIED` | DGA negatives | CSV | benign | n/a | Popularity bias | Check | Dedupe vs DGA | NOT USED |
| DNS tunnelling data | candidate sets `UNVERIFIED`; else synthetic (iodine/dnscat2-style in lab) | DNS tunnelling | PCAP | varies | both | Scarce | Check | — | NOT USED |
| TLS/QUIC metadata | candidate: CIC / Stratosphere captures `UNVERIFIED`; else self-captured benign + synthetic | Encrypted metadata | PCAP | weak | both | Few labelled malware TLS sets | Check | JA3/JA4 via Zeek | NOT USED |

## Gaps → synthetic generation
For classes lacking labels, generate synthetic traffic (scan loops, beacon timers with jitter, DNS tunnelling in an isolated lab, bulk uploads). **Report synthetic results in a separate table** from real-dataset results.

## Leakage prevention
- Time-based train/validation/test splits.
- Attack-family / DGA-family held-out test sets.
- De-duplicate flows and domains across splits.
- Fit scalers/encoders on training data only.
- Never random-split flows from the same session, host-pair or capture.
- Pick thresholds on validation, report on test once.

## Dataset hygiene
Record URL, version, SHA-256, download date, licence in `experiments/datasets.lock` (proposed). Do not commit raw data.
