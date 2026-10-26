# Performance Benchmarks

**All values: NOT YET MEASURED.** Do not fill in numbers without a recorded run.

## Environment record (fill per run)
CPU / RAM / OS / Python / library versions / Docker version / commit hash / dataset + hash / duration / input volume / concurrency / command.

## Metrics
| Metric | Method | Value |
|---|---|---|
| Precision/recall/F1 per class | offline eval | NOT YET MEASURED |
| False-positive rate | benign-only replay | NOT YET MEASURED |
| Alert latency p50 / p95 | timestamp ingest→stored | NOT YET MEASURED |
| Sustained flows/s | replay at increasing rate until drops | NOT YET MEASURED |
| CPU / memory | `docker stats` / psutil | NOT YET MEASURED |
| Dropped/unprocessed flows | queue counters | NOT YET MEASURED |
| Model size / inference latency | file size / timeit | NOT YET MEASURED |
| Directional-blindness penalty | see experiment doc | NOT YET MEASURED |

## Command templates
```bash
python -m bench.replay --pcap data/raw/x.pcap --rate 1x --duration 600   # PLANNED
docker stats --no-stream
```
Separate tables: unit-test, offline evaluation, replay benchmark, live sensor, synthetic.
