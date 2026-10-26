# Security and Isolation

Status: all `PLANNED`. **A diagram is not proof; the tests below are.**

## Design
| Control | Intent |
|---|---|
| Separate services | ingestion, analytics, API/dashboard |
| Ingestion on `internal: true` network | no route outside |
| `read_only: true` rootfs, tmpfs for scratch | immutability |
| `cap_drop: [ALL]` (add only what capture needs) | least privilege |
| Non-root user | least privilege |
| PCAP volume mounted `:ro` | no tampering |
| No code path to send packets or call firewall APIs | no active response |

Docker Compose sketch (`UNVERIFIED`):
```yaml
services:
  ingest:
    build: ./docker/ingest
    networks: [enclave]
    read_only: true
    cap_drop: [ALL]
    volumes: ["./data/pcaps:/data/pcaps:ro"]
  analytics:
    networks: [enclave]
  api:
    networks: [enclave, mgmt]
networks:
  enclave: { internal: true }
  mgmt: {}
```
Note: the API bridging `enclave` and `mgmt` is a deliberate, read-only query path; it must have no route into the monitored network.

## Tests to write
1. From the ingestion container: `curl -m 3 https://example.com` must fail; DNS must fail.
2. `touch /x` on rootfs must fail.
3. Static check: grep for raw-socket send, `sendp`, `send(`, firewall/iptables calls — must be absent.
4. Alerts never contain executable actions; API has no mutation endpoint that reaches the network.

Evidence to store: test output with date and commit hash. Not yet collected.

## Limitations
Docker isolation is not equal to a hardware diode. Physical one-way guarantees come from hardware, which we have not tested.
