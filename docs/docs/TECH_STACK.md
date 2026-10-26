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

Excluded unless a verified requirement appears: Kafka, Kubernetes, blockchain, LLM chatbot, multi-agent orchestration. (The SIH theme mentions blockchain; no requirement for it has been verified — `UNVERIFIED`.)
