# Security Policy

## Assumptions
- The sensor receives a one-way copy of traffic (TAP/SPAN/diode). The system is **passive**.
- No active probing, no handshake completion, no automated blocking or firewall commands.
- The ingestion service should have no network egress (see `docs/SECURITY_AND_ISOLATION.md`). Isolation is `PLANNED` until a test proves it.

## Reporting a vulnerability
Contact the team lead privately (add email here: `TODO`). Do not open public issues for exploitable bugs. Include affected component, steps to reproduce and impact.

## Handling PCAPs and metadata
- PCAPs may contain personal or sensitive data. Use public datasets or synthetic traffic for the demo.
- Do not commit PCAPs unless they are public and licence-compatible. Store them outside git (`data/` is git-ignored).
- Alerts contain IPs and domains: treat as sensitive. Use synthetic or documentation-range IPs (192.0.2.0/24, 198.51.100.0/24, 203.0.113.0/24) in docs.
- Rotate any secret that is accidentally committed.
