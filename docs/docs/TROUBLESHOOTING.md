# Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| `scapy` import/permission errors | missing libpcap / privileges | install libpcap; for PCAP file reading no root needed |
| Empty alerts after replay | threshold too high / wrong direction config | check `SENSOR_DIRECTION`, lower threshold on validation |
| Non-identical alerts between runs | random seed / unordered dict / time.now IDs | seed, sort, derive IDs from content hash |
| Dashboard blank | CORS / wrong API URL | check API URL env, CORS origins |
| Docker container can reach internet | network not `internal` | set `internal: true`, rerun egress test |
| High memory | unbounded flow table | add flow timeout/eviction |
| Schema rejection | wrong enum or confidence | check [ALERT_SCHEMA.md](ALERT_SCHEMA.md) |
| Dataset features missing | CSV vs PCAP mismatch | rebuild from PCAP |
