# Packets Insight

**Packets Insight** is a Python and Flask portfolio project for analysing network packet data exported from Wireshark.

The current development stage uses structured CSV datasets rather than processing raw PCAP files directly. This keeps the application lightweight, easier to deploy, and suitable for developing repeatable analysis workflows with Python and pandas.

## Project purpose

Packets Insight is designed to turn packet-level network data into clear engineering evidence. The project combines networking knowledge, Python development, data analysis, and practical OT/network-security thinking.

The application is being developed as a standalone project so that it can mature independently and strengthen the portfolio. In a later phase, selected packet-analysis capabilities may be integrated with the separate **Engineering Change Request Platform** as supporting evidence for network changes, investigations, and approvals.

## Current scope

- Create and manage packet-analysis cases
- Upload Wireshark-exported CSV datasets
- Validate required columns and supported CSV profiles
- Normalise alternative Wireshark column names
- Analyse packet counts, frame sizes, protocols, addresses, and timing data
- Produce clear engineering summaries and visual results
- Keep uploaded datasets private and outside public static folders

## Current input method

The MVP uses CSV files exported from Wireshark.

Direct PCAP upload and server-side TShark processing are intentionally postponed because lightweight hosting platforms may not provide TShark or allow unrestricted packet-capture processing.

## Planned development

1. CSV upload and validation
2. Dataset normalisation and indexing
3. Packet and protocol summaries
4. Traffic-rate, burst, latency, and jitter analysis
5. Case dashboards and engineering reports
6. Experiment comparison and Design of Experiments support
7. Anomaly-detection research
8. Optional PCAP/TShark processing on Render or Docker
9. Future evidence interface with the Engineering Change Request Platform

## Technology

- Python
- Flask
- pandas
- Bootstrap
- SQLite during early development
- Wireshark CSV exports
- Render or Docker for later deployment stages

## Repository structure

```text
packets-insight/
├── app/                  # Flask application package
├── tests/                # Automated tests
├── docs/                 # Architecture, roadmap, and engineering notes
├── data/
│   └── samples/          # Small anonymised example datasets only
├── instance/             # Local database and runtime files; not committed
├── uploads/              # User uploads; not committed
├── .env                  # Local secrets; not committed
├── .gitignore
├── README.md
├── requirements.txt
└── run.py
```

The exact application folders will be added gradually as the code is rebuilt and understood file by file.

## Development status

**Active development — CSV analysis MVP**

The repository is being organised as a learning-led engineering project. Each component will be added deliberately, documented clearly, and kept understandable enough to explain during portfolio reviews and interviews.

## Data and security

Real packet captures, customer information, internal IP addressing, credentials, and confidential network data must not be committed to this repository.

Only small, anonymised sample datasets should be stored under `data/samples/`.

## Related project

- **Engineering Change Request Platform** — a separate Flask application for controlled engineering-change workflows, approvals, traceability, and governance.

Packets Insight remains independent until both projects are mature enough for a controlled integration.
