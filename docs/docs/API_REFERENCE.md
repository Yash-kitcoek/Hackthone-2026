# API Reference

> **Nothing here is verified.** Endpoints below are the *proposed* contract. After the audit, list real endpoints from source and mark each `VERIFIED` only after a passing test.

Common: JSON, UTF-8. Auth: `PLANNED` (API key or none on isolated management network). Validation errors: HTTP 422 with Pydantic detail.

| Method | Path | Purpose | Status |
|---|---|---|---|
| GET | `/health` | Liveness | PLANNED |
| GET | `/api/alerts` | List/filter alerts | PLANNED |
| GET | `/api/alerts/{alert_id}` | One alert | PLANNED |
| GET | `/api/metrics` | Counters, latency | PLANNED |
| POST | `/api/replay` | Start PCAP replay | PLANNED |
| GET | `/api/detectors` | Detector list/status | PLANNED |
| GET | `/api/experiments` | Stored experiment results | PLANNED |

## GET /health
Response `200`: `{"status":"ok","version":"0.0.0"}`.

## GET /api/alerts
Query: `threat_class`, `severity`, `since` (ISO-8601), `limit` (1–500, default 50), `offset`.
```bash
curl "http://localhost:8000/api/alerts?threat_class=scanning&limit=10"
```
Response `200`:
```json
{"total":1,"items":[{"alert_id":"a-0001","timestamp":"2026-01-01T00:00:00Z","threat_class":"scanning","severity":"medium","confidence":0.71,"confidence_type":"heuristic_score","src_ip":"192.0.2.10","dst_ip":"198.51.100.5"}]}
```
(Synthetic example.) Errors: `422` invalid parameter.

## GET /api/alerts/{alert_id}
`200` full alert per [ALERT_SCHEMA.md](ALERT_SCHEMA.md); `404 {"detail":"alert not found"}`.

## POST /api/replay
Request: `{"capture_id":"synthetic-01","speed":1.0}`. Response `202`: `{"run_id":"..."}`. Must only read local files; never touches the network under observation. Errors: `404` unknown capture, `422`.

## GET /api/metrics, /api/detectors, /api/experiments
Response shapes to be defined with implementation; values must come from real runs or be `null`.

## Missing endpoints needed for the prototype
`POST /api/replay`, `/api/metrics`, `/api/detectors`, `/api/experiments` (all unimplemented until verified).

Source file for each endpoint: `UNVERIFIED`.
