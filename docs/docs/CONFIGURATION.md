# Configuration

> Variable names are proposals (`UNVERIFIED`). Align with the real `.env.example`.

| Variable | Purpose | Example |
|---|---|---|
| `SENSOR_DIRECTION` | Observed direction | `client_to_server` |
| `INPUT_MODE` | `pcap` or `live` | `pcap` |
| `PCAP_DIR` | Replay location (read-only mount) | `/data/pcaps` |
| `ALERT_DB_URL` | Alert store | `sqlite:///alerts.db` |
| `MODEL_DIR` | Saved models | `/models` |
| `WINDOW_SECONDS` | Aggregation window | `60` |
| `LOG_LEVEL` | Logging | `INFO` |
| `API_KEY` | API auth (if enabled) | set locally, never commit |

Thresholds live in `config/detectors.yaml` (proposed), chosen on validation data, never on test data. Record every config used for a result.
