# Project Audit

> **Audit status: NOT PERFORMED.** The repository was not available to the author of this document. This file is a template plus a worst-case assumption: nothing is implemented until evidence says otherwise.

## How to complete this audit
Run from the repo root and paste results below:
```bash
git log --oneline | head -30
find . -maxdepth 3 -not -path './.git/*' -not -path '*/node_modules/*' | sort
ls README* requirements*.txt pyproject.toml package.json Dockerfile* docker-compose* .env* 2>/dev/null
grep -rn "@app\.\(get\|post\|put\|delete\)\|@router\." --include=*.py .
grep -rn "TODO\|FIXME\|placeholder\|mock" --include=*.py --include=*.js --include=*.jsx --include=*.ts --include=*.tsx . | head -50
```

## Status classes
`VERIFIED` (implemented + test/run evidence) · `UNVERIFIED` (code exists, no evidence) · `PARTIAL` · `PLANNED` · `MISSING/BLOCKED`

## Feature status
| # | Feature | Status | Evidence (file / test / run) | Notes |
|---|---------|--------|------------------------------|-------|
| 1 | PCAP replay ingestion | PLANNED | — | |
| 2 | Live mirror ingestion | PLANNED | — | Only if safe and available |
| 3 | Packet/flow parsing | PLANNED | — | |
| 4 | Streaming feature extraction | PLANNED | — | |
| 5 | DDoS detector | PLANNED | — | |
| 6 | Beaconing detector | PLANNED | — | |
| 7 | DGA / DNS tunnelling detector | PLANNED | — | |
| 8 | Encrypted-session metadata detector | PLANNED | — | |
| 9 | Scanning detector | PLANNED | — | |
| 10 | Exfiltration detector | PLANNED | — | |
| 11 | Alert schema + validation | PLANNED | — | |
| 12 | Alert storage | PLANNED | — | |
| 13 | FastAPI backend | PLANNED | — | |
| 14 | React dashboard | PLANNED | — | |
| 15 | Docker isolation + egress test | PLANNED | — | |
| 16 | Directional-blindness experiment | PLANNED | — | |
| 17 | Test suite / CI | PLANNED | — | |

## Issues checklist (fill in)
- [ ] Placeholder / hard-coded API responses
- [ ] Broken frontend-backend integration
- [ ] Missing tests
- [ ] Secrets in repo or history
- [ ] README vs code mismatch
- [ ] Docker/deploy gaps (egress, privileges, writable FS)
- [ ] Unlicensed or oversized datasets committed

## Highest-priority tasks (if repo is empty)
1. Parse a PCAP into flows and print them (end-to-end skeleton).
2. Define and validate the alert schema (`docs/ALERT_SCHEMA.md`).
3. Implement two simplest detectors (scanning, DDoS) with tests.
4. FastAPI `GET /health`, `GET /api/alerts` backed by stored alerts.
5. Minimal React table of alerts.
6. Docker Compose with ingestion on an internal network + egress test.
7. Remaining detectors, then the directional-blindness experiment.
