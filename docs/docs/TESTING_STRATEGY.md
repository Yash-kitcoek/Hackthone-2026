# Testing Strategy

All tests `PLANNED`. Keep result categories separate.

| Area | Test | Type |
|---|---|---|
| Parsing | handcrafted packets, truncated/corrupt PCAP | unit |
| Features | known inputs → known values; missing fields → null | unit |
| Each detector | positive, negative, boundary, evasion-lite cases | unit |
| Malformed fields | detector must not crash | unit |
| Alert schema | valid/invalid fixtures | unit |
| API | httpx tests for each endpoint, 404/422 | integration |
| Dashboard | render with fixture alerts; empty/error state | frontend |
| Stream stability | replay 10+ minutes, no crash/leak | soak |
| Replay reproducibility | run twice → identical alert IDs/content (fixed seeds, deterministic IDs) | integration |
| Duplicates | same event twice → one alert | unit |
| Read-only enforcement | egress/FS tests in [SECURITY_AND_ISOLATION.md](SECURITY_AND_ISOLATION.md) | integration |
| Failure handling | DB down, queue full, bad model file | integration |
| Load | sustained replay at increasing rates | benchmark |
| Alert integrity (if hash chain built) | valid chain passes; modified/deleted/reordered alert detected at correct index | unit |

Commands (template): `pytest -q`, `pytest -m integration`, `npm test`.
Report each category in a separate table in [RESULTS.md](RESULTS.md).
