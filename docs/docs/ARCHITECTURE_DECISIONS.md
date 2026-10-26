# Architecture Decision Records

| ID | Decision | Rationale | Alternatives | Status |
|---|---|---|---|---|
| ADR-1 | Python as main language | ML + packet libs, team familiarity (`UNVERIFIED`) | Go, Rust | Proposed |
| ADR-2 | Scapy for MVP parsing; Zeek optional | Scapy easy; Zeek richer logs (JA3/JA4 via packages) | tshark | Proposed |
| ADR-3 | LightGBM / scikit-learn | Tabular features, fast, small models | Deep learning | Proposed |
| ADR-4 | Rule + ML hybrid | Rules give interpretable evidence; ML for DGA/tunnelling | ML only | Proposed |
| ADR-5 | asyncio queue before Redis | Single-host prototype; add Redis Streams only if measured need | Kafka | Proposed |
| ADR-6 | FastAPI + React | Typed API, common stack | Flask, Streamlit | Proposed |
| ADR-7 | Alert-only, no active response | Policy/safety for one-way deployments | Auto-block | Fixed |
| ADR-8 | SQLite first | Simple; upgrade if needed | PostgreSQL | Proposed |
| ADR-9 | No blockchain / LLM / Kubernetes | No verified requirement; adds risk | — | Fixed unless requirement appears |

Add new ADRs with: context, decision, consequences, date.
