# Packets Insight Architecture

## 1. Architectural objective

Packets Insight converts packet-level network data into structured and repeatable engineering analysis.

The initial architecture deliberately separates data ingestion, validation, normalisation, analysis, and presentation. This prevents the Flask routes from becoming responsible for every stage of the workflow and makes later PCAP support easier to introduce.

## 2. MVP data flow

```text
Wireshark CSV
      │
      ▼
Upload handling
      │
      ▼
Column validation
      │
      ▼
Column alias normalisation
      │
      ▼
Dataset indexing and metadata
      │
      ▼
Packet-analysis services
      │
      ▼
Flask views, dashboards, and reports
```

## 3. Proposed application layers

### Web layer

Responsibilities:

- Flask routes and forms
- User-facing validation messages
- Case pages and dashboards
- Report presentation

The web layer should call analysis services rather than contain pandas analysis directly inside route functions.

### Ingestion layer

Responsibilities:

- Accept supported CSV files
- Check file extension and size
- Store uploads outside the public static directory
- Read the dataset safely
- Return clear extraction errors

### Validation and normalisation layer

Responsibilities:

- Detect the supported Wireshark CSV profile
- Confirm required columns
- Map aliases to internal names
- Convert data types where practical
- Record missing, optional, and unexpected columns

Example aliases include:

- `No.` or `frame.number` → `frame_number`
- `frame.time_epoch` → `time_epoch`
- `Source` or `ip.src` → `ip_src`
- `Destination` or `ip.dst` → `ip_dst`
- `Protocol` or `frame.protocols` → internal protocol fields

### Analysis layer

Responsibilities:

- Packet and byte counts
- Frame-size statistics
- Protocol distribution
- Source and destination summaries
- Traffic rate and time-window analysis
- Burst, jitter, latency, and congestion indicators
- Dataset quality and anomaly checks

Analysis functions should receive a prepared pandas DataFrame and return structured results that are independent of HTML templates.

### Persistence layer

Early development may use SQLite for:

- Analysis cases
- Dataset metadata
- Analysis status
- User notes
- Generated result summaries

Uploaded packet datasets should remain separate from database records.

## 4. Suggested package direction

```text
app/
├── __init__.py
├── routes/
├── forms/
├── models/
├── services/
│   ├── csv_ingestion.py
│   ├── csv_validation.py
│   ├── column_mapping.py
│   └── packet_analysis.py
├── templates/
└── static/
```

This is a target structure, not a requirement to create every file immediately. The application should continue to be rebuilt one understandable file at a time.

## 5. Future PCAP processing

Raw PCAP support should be introduced as an alternative ingestion engine rather than a replacement architecture.

```text
PCAP file → TShark extraction → normalised packet dataset
CSV file  → CSV ingestion    → normalised packet dataset
                                      │
                                      ▼
                              shared analysis services
```

This approach allows CSV and PCAP inputs to use the same analysis layer.

## 6. Future Engineering Change Request integration

Packets Insight and the Engineering Change Request Platform remain separate applications during their early development.

A future integration should exchange controlled evidence rather than combine both codebases prematurely. Possible evidence exchanged later may include:

- Analysis case identifier
- Dataset time range
- Key traffic findings
- Before-and-after comparison
- Generated report reference
- Analyst conclusion

The Engineering Change Request Platform would consume approved analysis evidence while Packets Insight remains responsible for packet-data processing.

## 7. Security principles

- Never commit real captures or confidential CSV exports
- Keep uploads outside public static folders
- Restrict accepted file types and sizes
- Treat filenames as untrusted input
- Store secrets only in environment variables
- Use anonymised sample data for demonstrations
- Avoid exposing internal addresses or credentials in screenshots and reports
