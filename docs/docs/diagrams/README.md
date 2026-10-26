# Diagrams

All diagrams are **proposed designs**, not proof of implementation. No diagram shows a path from the enclave back to the monitored network.

## 1. High-level system architecture
Shows trust zones and the one-way copy. Slide: 4, 6.
```mermaid
flowchart LR
  subgraph MON["Monitored network (untrusted)"]
    SRC["Hosts and links"]
  end
  TAP["TAP / SPAN / diode<br/>one-way copy"]
  subgraph ENC["Analytics enclave (no path back)"]
    ING["Read-only ingestion"] --> PARSE["Parse and flow assembly"] --> FEAT["Feature extraction"] --> DET["Six detectors"] --> NORM["Alert normaliser"] --> STORE[("Alert store")]
  end
  subgraph MGMT["Management zone"]
    API["FastAPI"] --> UI["React dashboard"]
  end
  SRC -->|"mirrored copy"| TAP --> ING
  STORE --> API
```

## 2. Data flow
Shows each stage and the rejection path. Slide: 6.
```mermaid
flowchart TD
  A["Mirrored packets or PCAP"] --> B["Ingestion"] --> C["Parsed packets"] --> D["Flows and windows"] --> E["Feature vectors"] --> F["Detectors"] --> G["Candidate alerts"] --> H{"Schema valid?"}
  H -->|yes| I["Alert store"] --> J["API"] --> K["Dashboard"]
  H -->|no| L["Reject and log"]
```

## 3. Deployment and network isolation
Shows internal network and where the only bridge is. Slide: 6, 8.
```mermaid
flowchart LR
  subgraph MONNET["Monitored network"]
    S["Source traffic"]
  end
  M["Receive-only mirror port<br/>no IP, no transmit"]
  subgraph ENCLAVE["Docker internal network: no egress"]
    I["ingest container<br/>read-only FS, caps dropped"]
    AN["analytics container"]
    DB[("alert DB volume")]
  end
  subgraph MGMTNET["Management network"]
    AP["API container<br/>read-only queries"]
    FE["Dashboard"]
  end
  S -->|"copy"| M --> I --> AN --> DB
  DB --> AP --> FE
```

## 4. Streaming detection sequence
Shows time order; note that nothing returns to the source. Slide: 6.
```mermaid
sequenceDiagram
  participant T as TAP or PCAP
  participant I as Ingestion
  participant F as Feature extractor
  participant D as Detectors
  participant N as Normaliser
  participant S as Alert store
  participant A as API
  T->>I: mirrored packets (one-way)
  I->>F: parsed packets
  F->>D: window features and availability mask
  D->>N: candidate alert with evidence
  N->>S: validated alert
  A->>S: read query
  Note over T,I: No packet is ever sent back to the source
```

## 5. Six-detector components
Shows detectors share features and output. Slide: 7.
```mermaid
flowchart TB
  FEAT["Feature extractor"] --> D1["DDoS"]
  FEAT --> D2["Beaconing"]
  FEAT --> D3["DGA and DNS tunnelling"]
  FEAT --> D4["Encrypted-session metadata"]
  FEAT --> D5["Scanning"]
  FEAT --> D6["Exfiltration"]
  D1 --> OUT["Evidence and confidence"]
  D2 --> OUT
  D3 --> OUT
  D4 --> OUT
  D5 --> OUT
  D6 --> OUT
  OUT --> NORM["Alert normaliser"]
```

## 6. Alert lifecycle
Shows validation, dedup and human-only action. Slide: 8.
```mermaid
flowchart TD
  A["Detector emits candidate"] --> B{"Schema valid?"}
  B -->|no| X["Reject and log"]
  B -->|yes| C{"Duplicate?"}
  C -->|yes| M["Merge or suppress"]
  C -->|no| D["Store alert"]
  D --> E["Analyst views in dashboard"]
  E --> F["Human decides action outside this system"]
```

## 7. Dataset preparation and training pipeline
Slide: 9.
```mermaid
flowchart LR
  R["Raw datasets and synthetic"] --> V["Verify licence and hash"] --> P["Rebuild features from PCAP"] --> S["Time and family split"] --> T["Train on train only"] --> U["Tune on validation"] --> E["Test once"] --> M["Save model, config, data hash"]
```

## 8. Experiment and directional-blindness flow
Slide: 8, 9, 10.
```mermaid
flowchart TD
  D["Same samples and split"] --> A["Config A: bidirectional reference"]
  D --> B["Config B: unidirectional, simulated"]
  D --> C["Config C: strict availability, simulated"]
  A --> E["Same model family and tuning budget"]
  B --> E
  C --> E
  E --> R["Per-class precision, recall, F1, FPR"]
  R --> X["Delta versus A with intervals"]
```

## 9. Frontend/backend integration
Slide: 11, 12.
```mermaid
flowchart LR
  UI["React dashboard"] -->|"GET /api/alerts"| API["FastAPI"]
  UI -->|"GET /api/metrics"| API
  UI -->|"POST /api/replay"| API
  API --> DB[("Alert store")]
  API --> RP["Replay runner: reads local PCAP only"]
```

## 10. Implementation roadmap
Slide: 13, 15.
```mermaid
flowchart LR
  P1["1 MVP and replay"] --> P2["2 Six detectors"] --> P3["3 Streaming performance"] --> P4["4 Unidirectional validation"] --> P5["5 Data and calibration"] --> P6["6 Hardening"] --> P7["7 SOC integration"]
```
