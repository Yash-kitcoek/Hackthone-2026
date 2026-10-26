# Reproducibility

Status: `PLANNED`.

- Pin dependencies (`requirements.lock`, `package-lock.json`).
- Fix random seeds for NumPy, scikit-learn, LightGBM.
- Record dataset URL, version, SHA-256, download date, licence.
- Use deterministic alert IDs (hash of detector + flow/window + timestamp).
- Sort inputs and outputs; avoid wall-clock in logic (use packet time).
- Save config + model + feature list with each result.
- Verify: run the replay twice, `diff` alert JSON outputs — must match.
- Keep one `make reproduce` target (proposed) that downloads (manual step), builds features, trains, evaluates.
