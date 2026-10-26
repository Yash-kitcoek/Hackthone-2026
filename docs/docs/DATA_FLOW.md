# Data Flow

```mermaid
flowchart TD
  A["PCAP or mirrored packets<br/>one direction"] --> B["Ingestion (read-only)"]
  B --> C["Parsed packets"]
  C --> D["Flows and time windows"]
  D --> E["Feature vectors"]
  E --> F["Detectors"]
  F --> G["Candidate alerts with evidence"]
  G --> H{"Schema valid?"}
  H -->|yes| I["Alert store"]
  H -->|no| J["Reject and log"]
  I --> K["REST API"] --> L["Dashboard"]
```

| Stage | Input | Output | Failure handling |
|---|---|---|---|
| Ingest | pcap/interface | raw packets | skip corrupt, count |
| Parse | packets | flow records | malformed → counter |
| Features | flows | vectors | missing fields → `null` + availability mask |
| Detect | vectors | scored candidates | detector exceptions isolated |
| Normalise | candidates | alerts | schema failure logged |
| Store/API | alerts | JSON | 4xx/5xx per API doc |

No stage sends data toward the monitored network.
