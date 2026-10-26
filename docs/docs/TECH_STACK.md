# Tech Stack (proposed)

| Layer | Choice | Why | Status |
|---|---|---|---|
| Parsing | Scapy (MVP), Zeek (optional) | Simplicity / richer logs | PLANNED |
| ML | scikit-learn, LightGBM | Tabular, small models | PLANNED |
| Backend | FastAPI, Pydantic | Typed validation | PLANNED |
| Storage | SQLite → PostgreSQL if needed | Simplicity | PLANNED |
| Queue | asyncio queue; Redis Streams only if justified | Avoid complexity | PLANNED |
| Frontend | React | Dashboard | PLANNED |
| Packaging | Docker, Docker Compose | Isolation | PLANNED |
| Tests | pytest, httpx, React Testing Library | Standard | PLANNED |

Excluded unless a verified requirement appears: Kafka, Kubernetes, a distributed-ledger/blockchain network, LLM chatbot, multi-agent orchestration.

Theme note: the SIH theme is Blockchain & Cybersecurity, but no blockchain requirement in the problem statement has been verified (`UNVERIFIED` — read the portal text). Optional extension: SHA-256 hash-chained alert log (Python `hashlib`, no extra service) — `PLANNED`, see [UNIQUE_INNOVATION.md](UNIQUE_INNOVATION.md#5-optional-tamper-evident-alert-log-hash-chain).
