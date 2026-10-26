# Detector Design

Per-detector docs: [detectors/](detectors/). Shared interface (proposed):
```python
class Detector:
    name: str; version: str
    required_features: set[str]
    def score(self, window) -> list[CandidateAlert]: ...
```
Detectors must declare required features; if any are unavailable for the configured `SENSOR_DIRECTION`, the detector degrades (uses subset) or disables itself and reports it.

## Feature availability (unidirectional)
Assumes mirror exposes **client→server** only. Flip for server→client mirrors. Sensor placement decides this; `UNVERIFIED` against real hardware.

| Feature | Observable one-way? | Notes |
|---|---|---|
| Packets/bytes in observed direction | Yes | |
| Inter-arrival times | Yes | |
| Destination IP/port, protocol | Yes | |
| TCP SYN count | Yes | |
| SYN-ACK, handshake completion | **No** | reverse traffic |
| RTT, server response latency | **No** | |
| Connection refused (RST from server) | **No** | scanning "failed" indicator unavailable |
| Retransmissions | Partial | |
| Flow duration | Partial | end may be missed |
| Upload/download ratio | **No** | needs both |
| DNS query name, type, rate | Yes (if queries mirrored) | |
| DNS response, NXDOMAIN rate, TTL | **No** | |
| TLS ClientHello (SNI, ciphers, JA3/JA4 client) | Yes | |
| TLS ServerHello, cert, JA3S | **No** | |
| QUIC initial packet metadata | Partial | |
| Packet-size/timing sequence | Yes | one direction |

Implementation status of every detector: `PLANNED`.
