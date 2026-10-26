# Project Structure

> **Proposed layout.** Replace with the real tree after the audit (`find . -maxdepth 3`).

```
sih26145/
├── backend/
│   ├── app/            # FastAPI: main.py, routes/, schemas/
│   ├── ingest/         # pcap reader, live capture (read-only)
│   ├── features/       # flow assembly, feature extractors
│   ├── detectors/      # ddos.py beaconing.py dga_dns.py tls_meta.py scan.py exfil.py
│   ├── alerts/         # schema, normaliser, dedup, store
│   ├── ml/             # train.py, evaluate.py, models/
│   └── tests/
├── frontend/           # React app
├── data/               # git-ignored: raw/, processed/, synthetic/
├── experiments/        # configs, scripts, outputs
├── docker/             # Dockerfiles, compose, isolation tests
├── docs/
└── README.md
```
