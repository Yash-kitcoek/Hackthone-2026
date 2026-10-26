# Roadmap

Prototype roadmap (phases 1–5) vs production plan (6–7). Effort in person-days for a small student team (rough estimates, `UNVERIFIED`).

| Phase | Goal | Deliverables | Dependencies | Acceptance | Risks | Effort | Done when |
|---|---|---|---|---|---|---|---|
| 1 MVP + replay | End-to-end skeleton | PCAP reader, flows, 1 detector, API, table UI | Sample PCAP | Replay twice → same alerts | Parsing bugs | 7–10 | Demo runs from clean clone |
| 2 Six detectors | Full coverage | 6 detectors + tests + per-class eval | Datasets / synthetic | Per-class metrics recorded | Label gaps | 12–15 | Each detector has test + eval row |
| 3 Streaming perf | Measured speed | Benchmarks, queue tuning | Phase 2 | p50/p95, flows/s recorded | Bottlenecks | 5–7 | Benchmark doc filled |
| 4 Unidirectional validation | Directional experiment + isolation | Three-config results, egress tests | Phase 2 | Tables + passing tests | Weak signal | 5–7 | Results doc filled |
| 5 Data & calibration | Better data, fewer FPs | Calibration, extra datasets | Phase 4 | Reliability curves, FPR down vs baseline | Dataset licence | 7–10 | Calibration report |
| 6 Hardening | Production-style hardening | Observability, auth, CI, packaging | Phase 5 | Security review passed | Hardware access | 10+ | Hardening checklist |
| 7 SOC integration | Export to approved workflows | Read-only outbound alert export from management zone | Org approval | No path to monitored net (tested) | Policy | TBD | Approved integration test |

Diagram: [diagrams/README.md](diagrams/README.md#10-implementation-roadmap).
