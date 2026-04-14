# Customs Data Analysis Project

**Freight & Customs Operations Dashboard — Power BI & Excel**
Reporting Period: January 2023 – December 2024

---

## Overview

This project analyses freight and customs operations data across a two-year period, covering 1,200 shipments, 10 clients, 10 carriers, 10 European destination ports, and 15 HS codes. The goal was to build a reporting layer that surfaces compliance KPIs, duty optimisation performance, and operational bottlenecks in a format accessible to both operational teams and senior stakeholders.

The dashboard was designed and built end-to-end — from data modelling and Power Query transformations to DAX measure development and report layout — and is actively used for decision-making across customs, logistics, and finance functions.

---

## Business Problem

Customs and trade operations generate large volumes of shipment, classification, and financial data across multiple carriers, regimes, and trade lanes. Without a centralised reporting layer, identifying duty savings opportunities, monitoring clearance performance, and benchmarking carrier efficiency required significant manual effort and produced inconsistent outputs.

This project addresses that gap by consolidating multi-source operational data into a single interactive dashboard, enabling:

- Real-time visibility into duty liability and savings performance
- HS code-level classification and duty rate analysis
- Carrier and port performance benchmarking
- On-time clearance monitoring against SLA thresholds
- Customs regime effectiveness comparison across four relief schemes

---

## Key Findings

### Duty Optimisation
- **€2.88M in duties saved** against €3.08M paid — a **48.26% savings rate**, nearly double the industry benchmark of 20–35%
- Total cargo value managed: **€152.52M** across 1,200 shipments
- Temporary Admission was the highest-performing relief instrument at 30.73% of total savings
- All four customs regimes contributed meaningfully — Temporary Admission (30.73%), End Use Relief (26.57%), IP Relief (22.53%), and FTA Relief (20.16%) — confirming a sophisticated multi-regime approach
- Standard Entry shipments represent an untapped opportunity: a 10% conversion to relief schemes could add an estimated €150–200K in annual savings

### HS Code & Classification Analysis
- 7 of 15 HS codes are zero-rated — duty mitigation efforts concentrated on the remaining 8 dutiable codes
- Textiles carry the highest duty rate at 12% — identified as the highest financial exposure category requiring maximum relief coverage
- Automotive Parts (HS 8708.99) achieved the highest absolute savings at €291,736 with a 53.76% savings rate
- Machinery (HS 8428.90) achieved a 52.32% savings rate at a 1.70% duty rate — the most efficient relief scheme application in the dataset

### Operational Performance
- On-time clearance rate of **41.08%** — identified as the most critical improvement area against a 75–85% industry benchmark
- Average clearance time of 4.09 days — best-in-class operations target under 2 days
- Import and export clearance times virtually identical (4.10 vs 4.07 days) — consistent processing across both directions
- The current 3-day SLA threshold is likely too aggressive for relief scheme shipments requiring additional documentation; a 5-day SLA would more accurately reflect operational complexity

### Geographic & Carrier Distribution
- Port distribution is highly balanced — no single port exceeds 11% of total volume, minimising concentration risk
- Active UK trade lane management via Felixstowe post-Brexit
- No carrier exceeds 12.25% of total volume — strong diversification reducing operational dependency
- MSC leads import volumes at 114 shipments, consistent with Asia-Europe sea freight dominance

---

## Dashboard Structure

The Power BI dashboard is organised across the following report pages:

| Page | Content |
|---|---|
| Executive Summary | Top-line KPIs — shipments, cargo value, duty saved, on-time rate |
| Shipment Analysis | Volume by direction, transport mode, and client |
| Time & Performance | Transit times, clearance times, on-time rate vs SLA |
| HS Code & Classification | Category breakdown, duty rates, zero-rated codes |
| Duty & Financial Analysis | Savings by regime, direction, and client |
| Geographic Analysis | Destination port distribution and trade lane mapping |
| Carrier Performance | Carrier volume, mode breakdown, and import/export split |

---

## Technical Stack

### Power BI
- **Power Query (M)** — multi-source data ingestion, cleaning, and transformation; handling of nulls, data type standardisation, and column normalisation across shipment, financial, and carrier datasets
- **DAX measures** — dynamic KPI calculations including duty savings rate, on-time rate, average clearance days, and period-over-period comparisons using time intelligence functions (`CALCULATE`, `DATEADD`, `TOTALYTD`)
- **Data modelling** — star schema design with a central fact table (shipments) connected to dimension tables (clients, carriers, ports, HS codes, customs regimes)
- **Scheduled refresh** — automated data refresh configuration for live operational monitoring

### Excel
- Supporting financial models and reconciliation templates used in pre-dashboard data preparation
- Power Query connections mirroring dashboard data sources for offline analysis

---

## DAX Measures — Key Examples

```dax
-- Duty Savings Rate
Duty Savings Rate =
DIVIDE(
    SUM(Shipments[Duty_Saved]),
    SUM(Shipments[Duty_Saved]) + SUM(Shipments[Duty_Paid]),
    0
)

-- On-Time Clearance Rate
On-Time Rate =
DIVIDE(
    COUNTROWS(FILTER(Shipments, Shipments[Clearance_Days] <= 3)),
    COUNTROWS(Shipments),
    0
)

-- Average Clearance Days
Avg Clearance Days =
AVERAGE(Shipments[Clearance_Days])

-- Total Duty Saved YTD
Duty Saved YTD =
TOTALYTD(
    SUM(Shipments[Duty_Saved]),
    Dates[Date]
)
```

---

## Files in This Repository

```
customs-data-analysis-project/
│
├── README.md                         
├── data/
│   └── Shipments.csv
│   └── Calendar.csv
│   └── Clients.csv
│   └── Duties.csv
│   └── HS Codes.csv
│   └── Time Tracking.csv
└── Full_Report/
    └── Customs_Report.pdf
└── Insights Report/
    └── Full_Insights_Report.pdf     
```

---

## What I Learned

Building this dashboard made clear that the hardest part of any analytics project is not the tool — it's the data. Shipment records arrived inconsistently formatted across sources, clearance timestamps required significant cleaning before they were usable, and defining "on-time" turned out to be a more nuanced question than it first appeared.

The most interesting finding was the gap between the 48.26% duty savings rate — which looks strong — and the 41.08% on-time rate, which tells a different story about operational efficiency. Both numbers are correct. They just measure different things, and presenting them together without context would lead to the wrong conclusions. That tension between metrics is where the real analytical work happens.

The recommendation to review the 3-day SLA threshold came directly from drilling into which shipment types were consistently late — relief scheme shipments requiring additional documentation were disproportionately represented. That's not a performance problem; it's a target-setting problem.

---

## Strategic Recommendations (from the full report)

1. Implement clearance delay analysis by carrier, port, and HS code to identify root causes of the 58.92% late rate
2. Review the 3-day clearance SLA — a 5-day threshold better reflects relief scheme complexity
3. Conduct a relief scheme eligibility review on all Standard Entry shipments, particularly Textiles and Food & Beverage
4. Expand FTA utilisation — currently 20.16% of savings despite being the most scalable relief instrument
5. Develop carrier scorecards tracking on-time performance to inform future carrier allocation decisions

---

## About

Built by **Francisco Costa** — Customs Analyst with a background in legal analysis, trade compliance, and data analytics. This project is part of a broader portfolio of data analysis and visualisation work in compliance, governance, and operational reporting contexts.

[LinkedIn](https://linkedin.com/in/francscosta) · franciscostabusiness@gmail.com
