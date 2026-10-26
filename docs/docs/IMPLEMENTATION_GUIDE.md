# Implementation Guide (clean clone → working prototype)

> Commands are **templates**. None were verified against the repository. Adjust paths after the audit and tick each step only after it works.

## Step 1 — Prerequisites
Purpose: toolchain. Needs Python 3.10+, Node 18+, Docker, Git, libpcap. Verify: `python --version && node --version && docker --version`.
Common error: missing libpcap → `sudo apt install libpcap-dev`.

## Step 2 — Repo and Python env
```bash
git clone <REPO_URL> && cd <REPO>
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt   # file name UNVERIFIED
```
Verify: `pip list | grep -i -E "fastapi|scapy|scikit|lightgbm"`.

## Step 3 — Frontend
```bash
cd frontend && npm install && npm run dev
```
Verify: dashboard opens on the dev-server URL printed.

## Step 4 — Environment variables
Copy `.env.example` → `.env` (see [CONFIGURATION.md](CONFIGURATION.md)). Never commit `.env`.

## Step 5 — Datasets
Follow [DATASETS.md](DATASETS.md). Store under `data/` (git-ignored). Record checksums.

## Step 6 — PCAP ingestion
Module: `backend/ingest/` (proposed). Run a replay on a small public/synthetic PCAP. Expected: packet count log. Verify: count matches `capinfos` / `tshark -r f.pcap | wc -l`.

## Step 7 — Feature extraction
Module: `backend/features/`. Expected: a table of flows with availability masks. Verify with unit tests on handcrafted packets.

## Step 8 — Detectors
Module: `backend/detectors/`. Implement in this order: scanning → DDoS → beaconing → exfiltration → DGA/DNS → TLS metadata. Each: unit tests + one labelled sample.

## Step 9 — Training and saving
```bash
python -m ml.train --config experiments/<cfg>.yaml   # PLANNED
```
Save model with version, feature list, data hash and seed. Verify: reload and reproduce a score.

## Step 10 — Streaming inference
asyncio queue between parser and detectors. Verify: replay twice → identical alerts.

## Step 11 — Alert normalisation + persistence
Validate with the schema in [ALERT_SCHEMA.md](ALERT_SCHEMA.md); dedupe; store. Verify: invalid alert rejected.

## Step 12 — FastAPI
```bash
uvicorn app.main:app --reload
curl http://localhost:8000/health
```
See [API_REFERENCE.md](API_REFERENCE.md).

## Step 13 — Dashboard integration
Point frontend base URL to API. Verify: alerts table shows API data, not mock data.

## Step 14 — Docker
```bash
docker compose up --build
```
Verify isolation per [SECURITY_AND_ISOLATION.md](SECURITY_AND_ISOLATION.md).

## Step 15 — Tests
```bash
pytest -q          # unit + integration
cd frontend && npm test
```
## Step 16 — Benchmarks
See [PERFORMANCE_BENCHMARKS.md](PERFORMANCE_BENCHMARKS.md).

## Step 17 — Demo
See [DEMO_SCRIPT.md](DEMO_SCRIPT.md). Troubleshooting: [TROUBLESHOOTING.md](TROUBLESHOOTING.md).

Rules: do not overwrite working code; do not add duplicate modules to match this layout; separate code commits from doc commits.
