# Contributing

## Workflow
1. Branch from `main`: `feat/<topic>`, `fix/<topic>`, `docs/<topic>`.
2. Small, verifiable commits. Conventional Commits: `feat:`, `fix:`, `docs:`, `test:`, `chore:`.
3. Open a pull request; at least one teammate reviews.

## Testing expectations
- New detector or feature code ships with unit tests, including malformed/missing-field cases.
- Never mark a feature "Implemented and verified" in docs without a passing test or recorded run.

## Documentation requirements
- Update the status in `docs/FEATURES.md` and `docs/PROJECT_AUDIT.md` when status changes.
- Results go in `docs/RESULTS.md` only with a command, commit hash, dataset and date. Otherwise write `NOT YET MEASURED`.
- Never commit real PCAPs with private data, secrets, or `.env` files.
- Never add code that sends packets toward the monitored network or blocks traffic.
