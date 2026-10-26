# Use Cases

Proposed scenarios only; no deployment is claimed.

| ID | Actor | Scenario | Detector(s) | Output |
|---|---|---|---|---|
| UC1 | SOC analyst | Reviews alerts from a diode-fed sensor | All | Alert list with evidence |
| UC2 | Analyst | Replays a captured incident PCAP | All | Reproducible alerts |
| UC3 | Analyst | Investigates a host with periodic outbound connections | Beaconing | Periodicity/jitter evidence |
| UC4 | Analyst | Reviews suspicious DNS names | DGA/DNS | Entropy, n-gram, query-rate evidence |
| UC5 | Engineer | Checks the sensor cannot egress | — | Isolation test report |
| UC6 | Researcher | Measures one-way visibility penalty | All | Directional-blindness table |
| UC7 | Analyst | Sees a fan-out from one source | Scanning | Unique host/port counts |
| UC8 | Analyst | Sees large outbound transfer to a new destination | Exfiltration | Byte-volume deviation |

## Candidate deployment locations (proposed)
Government/critical-infrastructure enclaves with TAP/SPAN/diode monitoring; research testbeds; training labs.
