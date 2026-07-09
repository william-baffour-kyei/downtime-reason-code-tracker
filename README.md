# Manufacturing Downtime & Reason-Code Tracker

An Excel-based analytics tool that tracks, categorises, and visualises unplanned and planned downtime across a multi-line manufacturing operation. Built as a companion piece to my [OEE Dashboard](#) project.

> **Note:** the underlying dataset is synthetic, generated to reflect the general structure of a multi-division fabrication group (6 production lines, 3 shifts, Jan 2022–Dec 2024). It does not contain real company data.


## What this shows

- Working with messy, real-world-style data (duplicates, blanks, outliers) and documenting a clean, repeatable cleaning process
- Building a single flat fact table with row-level `XLOOKUP` formulas — a deliberate, simpler alternative to a Power Pivot/Data Model approach, chosen to match industry-standard practice taught in my Ivy Professional School analytics programme
- Filter-aware KPIs using `SUBTOTAL()`, so headline numbers stay accurate under any slicer selection
- A connected, interactive dashboard: one set of slicers filters the KPI table and all four charts simultaneously

## Data preparation

- Started from 18,094 raw downtime event records
- Removed 175 duplicate Event IDs
- Removed 177 rows with blank duration values
- Final clean dataset: **17,741 rows**
- 36 rows flagged with a duration/cost mismatch for further review (not yet resolved — a known open item)

## Dashboard

<img width="1742" height="656" alt="Manufacturing Dashbaord" src="https://github.com/user-attachments/assets/ff549a92-f37a-4fc2-aa2d-a0108fb90d07" />
<img width="1360" height="367" alt="Downtime Trend by Months" src="https://github.com/user-attachments/assets/6b6f0779-7a48-4cfd-b479-edf393ef2af1" />
<img width="1412" height="372" alt="Downtime by Shift" src="https://github.com/user-attachments/assets/a0708172-3df5-420d-80aa-642d2b28138c" />

**KPI cards** (all filter-aware via `SUBTOTAL`):

| Metric | Value |
|---|---|
| Total Downtime (Hrs) | ~19,098 |
| Total Cost Impact (£) | ~£38.87M |
| % Unplanned | 82% |
| Total Events | 17,739 |
| Avg Cost per Event | ~£2,191 |

**Charts:**
- Downtime by Category — which fault types drive the most lost hours
- Downtime by Line — where downtime is concentrated
- Downtime by Shift — whether time of day is a factor
- Downtime Trend — monthly downtime hours across the full 3-year period, with a linear trendline

## Key finding

Downtime has stayed roughly **flat over the full three-year period** — the trendline shows no meaningful improvement or worsening. Combined with 82% of downtime being unplanned, this points to a persistent, unaddressed root cause (largely Mechanical Failure and Material Shortage) rather than a one-off event. That's the kind of pattern that justifies a deeper root-cause investigation rather than reactive fixes.

## Method

1. Cleaned raw data (deduplication, blank removal)
2. Flattened dimension data (Category, SubCode, LineName, ShiftName) into the fact table using `XLOOKUP`
3. Built `SUBTOTAL`-based KPI cards for filter-aware reporting
4. Built four PivotCharts from the same source table
5. Connected slicers (Line, Shift) across the KPI table and all charts via Report Connections

## Files

- `Downtime_ReasonCode_Tracker.xlsx` — full workbook, all sheets and formulas intact

---
*Built by William Baffour Kyei — [GitHub Portfolio](https://github.com/william-baffour-kyei/data-portfolio)*

