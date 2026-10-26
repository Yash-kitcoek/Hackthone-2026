# Deployment

Status: `PLANNED`. Prototype deployment only; production deployment is out of scope until hardened (Roadmap phase 6).

## Prototype (single host)
```bash
docker compose up --build
```
Services: ingest, analytics, api, frontend (see [SECURITY_AND_ISOLATION.md](SECURITY_AND_ISOLATION.md)).

## Live mirror (optional, `PLANNED`)
Capture interface must be a mirror/TAP receive-only port. Disable IP on that interface; do not bridge it. Verify no TX with `ip -s link`. Hardware testing: not done.

## Backup / data
Alert DB volume backup; PCAPs outside git; delete sensitive captures after use.

## Checklist
- [ ] `.env` set, no secrets in git
- [ ] Ingestion has no egress (test passed)
- [ ] API bound to management interface only
- [ ] Logs do not contain sensitive payloads
