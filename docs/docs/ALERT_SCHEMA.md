# Alert Event Schema (v1, proposed)

Separate from REST API wrappers. Versioned via `schema_version`.

## Fields
| Field | Type | Required | Notes |
|---|---|---|---|
| schema_version | string | yes | `"1.0"` |
| alert_id | string (uuid) | yes | unique |
| timestamp | ISO-8601 UTC | yes | event time |
| flow_id | string | no | null for window-level alerts |
| src_ip, dst_ip | string | no | may be null for aggregate alerts |
| protocol | enum tcp/udp/icmp/dns/tls/quic/other | yes | |
| threat_class | enum ddos, beaconing, dga_dns_tunnelling, encrypted_metadata, scanning, exfiltration | yes | |
| severity | enum low/medium/high/critical | yes | |
| confidence | number 0–1 | yes | |
| confidence_type | enum `heuristic_score` / `calibrated_probability` | yes | default heuristic |
| detector | string | yes | name + version |
| evidence_features | object | yes | feature → value (+ threshold) |
| unavailable_features | array | no | features not observable |
| model_version | string | no | null for pure rules |
| sensor_direction | enum `client_to_server`, `server_to_client`, `both`, `unknown` | yes | |
| explanation | string | yes | human text |
| dataset_or_capture_id | string | yes | |
| evaluation_kind | enum `real`, `synthetic`, `live` | yes | |

## Validation rules
confidence ∈ [0,1]; `calibrated_probability` only if calibration report exists; `evidence_features` non-empty; timestamps UTC; IPs valid or null; unknown fields rejected (version bump to add).

## Versioning
Semantic: additive optional fields → minor; breaking → major. Store `schema_version` on every alert.

## Example (synthetic — not from a real incident)
```json
{
  "schema_version": "1.0",
  "alert_id": "3f1c2d9e-0000-4000-8000-000000000001",
  "timestamp": "2026-01-01T10:00:00Z",
  "flow_id": null,
  "src_ip": "192.0.2.10",
  "dst_ip": null,
  "protocol": "tcp",
  "threat_class": "scanning",
  "severity": "medium",
  "confidence": 0.74,
  "confidence_type": "heuristic_score",
  "detector": "scan_fanout_v0",
  "evidence_features": {"unique_dst_hosts_60s": 240, "unique_dst_ports_60s": 3, "threshold_hosts": 100},
  "unavailable_features": ["syn_ack_ratio", "rst_response_rate"],
  "model_version": null,
  "sensor_direction": "client_to_server",
  "explanation": "One source contacted 240 distinct hosts in 60 s, above the 100-host threshold.",
  "dataset_or_capture_id": "synthetic-scan-01",
  "evaluation_kind": "synthetic"
}
```
