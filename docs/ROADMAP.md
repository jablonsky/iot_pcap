# Packets Insight Roadmap

## Project direction

Packets Insight remains a standalone Flask and Python data-analysis project while the Engineering Change Request Platform is developed separately.

The immediate goal is a reliable CSV-first minimum viable product based on packet data exported from Wireshark. Raw PCAP processing and cross-project integration are later stages.

## Phase 0 — Repository foundation

- [x] Establish standalone repository identity
- [x] Add project README
- [x] Protect secrets, databases, uploads, and packet captures with `.gitignore`
- [x] Document architecture and project boundaries
- [ ] Rename repository from `iot_pcap` to `packets-insight`
- [ ] Add the existing local application code in controlled commits
- [ ] Add an initial tagged baseline release

Suggested first tag: `v0.1.0-csv-foundation`

## Phase 1 — CSV ingestion

- [ ] Create packet-analysis case
- [ ] Upload Wireshark CSV file
- [ ] Apply file-size and extension checks
- [ ] Store uploads outside the public static directory
- [ ] Read CSV data with clear exception handling
- [ ] Record packet count and dataset time range

## Phase 2 — Validation and normalisation

- [ ] Define supported CSV export profiles
- [ ] Validate minimum required columns
- [ ] Implement column alias mapping
- [ ] Convert numeric and time fields safely
- [ ] Report missing and unsupported columns clearly
- [ ] Add tests for valid and invalid CSV datasets

## Phase 3 — Core packet analysis

- [ ] Packet and byte totals
- [ ] Frame-length statistics
- [ ] Protocol distribution
- [ ] Source and destination summaries
- [ ] Conversation summaries
- [ ] Time-based packet-rate analysis
- [ ] Dataset quality checks

## Phase 4 — Engineering dashboards and reporting

- [ ] Case dashboard
- [ ] Analysis summary cards
- [ ] Tables and charts
- [ ] Analyst notes and conclusions
- [ ] Exportable engineering report
- [ ] Anonymised demonstration case for the portfolio

## Phase 5 — Advanced network analysis

- [ ] Burst and utilisation indicators
- [ ] Jitter analysis
- [ ] Latency-related metrics where the dataset supports them
- [ ] Congestion and packet-loss indicators
- [ ] Before-and-after dataset comparison
- [ ] Design of Experiments support

## Phase 6 — Research features

- [ ] Feature-engineering pipeline
- [ ] Baseline traffic profiles
- [ ] Statistical anomaly checks
- [ ] Machine-learning anomaly-detection experiments
- [ ] Model-readiness and data-quality reports

## Phase 7 — Optional PCAP engine

- [ ] Deploy in an environment that supports TShark
- [ ] Add controlled PCAP upload
- [ ] Extract selected fields into the normalised packet dataset
- [ ] Reuse the existing validation and analysis services
- [ ] Consider Docker deployment

## Phase 8 — Engineering Change Request evidence interface

This phase begins only after both projects have stable internal structures.

- [ ] Define the evidence object exchanged between applications
- [ ] Link a Packets Insight case to an engineering change
- [ ] Attach approved analysis summaries or reports
- [ ] Support before-and-after change evidence
- [ ] Maintain independent repositories and release histories

## Development principles

- Build one understandable component at a time
- Keep route functions small
- Keep pandas analysis in dedicated services
- Commit working stages with meaningful messages
- Never commit real or confidential network data
- Prefer repeatable engineering analysis over decorative dashboards
- Document important design changes as the project evolves
