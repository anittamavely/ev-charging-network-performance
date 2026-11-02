# EV Charging Network Performance & Operational Efficiency

## Project Overview

A Power BI project analysing charging-session activity, revenue, energy delivered, station utilisation, and operational reliability across a simulated electric-vehicle (EV) charging network.

The dashboard has three pages:

1. **Executive Overview** — KPIs, monthly trends, revenue by power class, connector share, and network pricing versus utilisation.
2. **Operational Reliability & Grid Diagnostics** — failed sessions, grid events, queue time, failure rate by power class and temperature band, and failure rate versus target.
3. **Demand & Root-Cause Analysis** — revenue breakdown, key influencers, network comparisons, and sessions by start hour.

> **Important:** Charging-session records and operational outcomes are simulated. Findings are illustrative and are not actual results from real charging providers.

## Dataset and Source

This project uses four tables from the Kaggle dataset [**EV Charging Network Operations Benchmark 2026**](https://www.kaggle.com/datasets/dianatofficial/ev-charging-network-operations-benchmark-2026), published by **dianatofficial**. The source dataset README identifies the licence as **CC BY-SA 4.0**. Retain attribution and share adaptations under the same licence. Network and connector names belong to their respective owners, and network scale figures are approximate public estimates.

The project analyses 100,000 simulated charging sessions across 10 networks, 4 power classes, and 5 connector types. Session dates run from **1 March to 26 September 2026**; September is incomplete.

### Data files used

| File | Purpose |
|---|---|
| `charging_sessions.csv` | Session-level records: energy, revenue, connector, network, power class, temperature, queue time, duration, utilisation, failure status, grid events, and start hour. |
| `charging_networks.csv` | Network-level attributes such as footprint, public ports, connectors, and strategy. |
| `connector_types.csv` | Connector descriptions and maximum power. |
| `power_classes.csv` | Power-class attributes, typical power, use case, and session share. |

`network_profile.csv` is not used in this project and is intentionally excluded.

## Key Dashboard Figures

The dashboard displays these values when slicers are set to **All**:

| Metric | Displayed value |
|---|---:|
| Total charging sessions | 100,000 |
| Total revenue | Approximately $2.01 million |
| Energy delivered | Approximately 3.96 GWh |
| Failed sessions | 3,214 |
| Overall failure rate | 3.21% |
| Average station utilisation | 43.85% |
| Average queue time | 1.99 minutes |
| Grid-event sessions | 1,197 |
| Failure-rate target | 2.00% |

The overall failure rate is above the dashboard's 2.00% target. Among the displayed power classes, DC 350 kW has the highest failure rate. These are descriptive patterns in simulated data, not proof that power class or temperature causes failures.

Figures may change when slicers or visual-level filters are applied. Interpret September carefully because it covers only part of the month.

## Analysis and DAX

DAX measures calculate the KPIs and comparisons shown in the report. Main calculation groups include:

- Total sessions and total revenue
- Total energy delivered, shown in kWh and GWh
- Successful and failed sessions, and failure rate
- Average station utilisation and queue time
- Average energy per session, delivered power, session duration, session revenue, price per kWh, and temperature
- Grid-event sessions
- Previous-month revenue, month-over-month revenue growth, and month-to-date revenue
- Failure-rate target and supporting top/bottom network selection

The model also includes a `Dim_Date` table for date filtering and time-based calculations, plus supporting fields/tables for temperature bands and ranking. The full DAX code remains in the `EV Charging Session Project.pbix` file; this README summarises the calculations rather than listing every formula.

## Data Model

`charging_sessions` is the central session-level table. It is related to lookup tables for networks, connector types, and power classes. `Dim_Date` supports date-based analysis.

## Tools Used

- Microsoft Power BI Desktop
- DAX measures
- Data modelling and relationships
- Interactive slicers and report-page tooltips
- KPI cards, line-and-column chart, bar charts, donut chart, scatter plot, decomposition tree, and key-influencer visual

## Repository Structure

```text
ev-charging-network-performance/
├── dashboard/
│   └── EV Charging Session Project.pbix
├── data/
│   ├── charging_sessions.csv
│   ├── charging_networks.csv
│   ├── connector_types.csv
│   └── power_classes.csv
├── screenshots/
│   ├── Executive Overview.png
│   ├── Operational Reliability & Grid Diagnostics.png
│   ├── Demand & Root-Cause Analysis.png
│   └── Data Modeling.png
└── README.md
```

## How to View the Project

1. Download or clone this repository.
2. Open the `.pbix` file in Microsoft Power BI Desktop.
3. If Power BI asks for source paths, point it to the CSV files in `data/` and refresh.
4. Use the slicers to explore the report by network, date, and power class.

## Limitations

- Session records and outcomes are simulated, not real operator telemetry.
- September 2026 is an incomplete reporting month.
- Results can change with slicer and filter selections.
- Relationships between variables do not establish cause and effect.

## Dataset Attribution

Source: [**EV Charging Network Operations Benchmark 2026**](https://www.kaggle.com/datasets/dianatofficial/ev-charging-network-operations-benchmark-2026) by **dianatofficial**.  
Licence: **CC BY-SA 4.0**, as stated in the source dataset README. Retain attribution and share adapted material under the same licence.
