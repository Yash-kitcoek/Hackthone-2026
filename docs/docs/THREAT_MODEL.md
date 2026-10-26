# Threat Model

## Assets
Alert integrity, captured metadata confidentiality, enclave isolation, model integrity.

## Trust boundaries
1. Monitored network → TAP (one-way, untrusted data).
2. Enclave internal services.
3. Enclave → management zone (read-only query).

## Threats to the sensor itself (STRIDE-style)
| Threat | Example | Mitigation (planned) |
|---|---|---|
| Malformed packet attack (DoS on parser) | Crafted PCAP crashes parser | Defensive parsing, fuzz tests, resource limits |
| Evasion | Attacker slows beacon, randomises jitter | Document limits; multi-window analysis |
| Poisoning | Training on attacker-controlled data | Curated datasets, versioned models |
| Alert flooding | Attack designed to create alert storms | Rate limits, dedup, aggregation |
| Egress/exfil from enclave | Compromised service calls out | Internal network, no egress rules, tested |
| API abuse | Unauthenticated access to alerts | Auth, bind to management interface only |
| Sensitive data exposure | PCAPs in repo | `.gitignore`, SECURITY.md |

## Out of scope
Endpoint compromise detection, payload decryption, active response, physical attacks.

## Assumptions
Mirror integrity is trusted; hardware diode behaviour not tested by us (`UNVERIFIED`).
