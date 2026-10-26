# Demo Script (5–7 min)

> Commands are templates (`UNVERIFIED`). Rehearse and record real output. Use only synthetic/public PCAPs.

| # | Time | Step | Action / command | Expected | Fallback |
|---|---|---|---|---|---|
| 1 | 0:00–0:45 | Problem | Slide: one-way traffic, no reply allowed | — | — |
| 2 | 0:45–1:30 | Read-only design | Show compose file + isolation test | Egress command fails | Show saved test output |
| 3 | 1:30–2:15 | Start replay | `curl -X POST /api/replay ...` or UI button | Run accepted | Run CLI replay |
| 4 | 2:15–3:30 | Alerts | Dashboard alert list | Alerts across classes | Pre-recorded screen capture |
| 5 | 3:30–4:15 | Evidence | Open one alert | Evidence features visible | Show JSON |
| 6 | 4:15–5:00 | Measured results | Show results table | Real numbers or "not measured" | — |
| 7 | 5:00–6:00 | Directional blindness | Show table A/B/C | Δ per class | Show plan if unfinished |
| 8 | 6:00–7:00 | Limits + close | Slide | Honest limitations | — |

Say clearly which parts are replayed, synthetic or live.
