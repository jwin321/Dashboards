# ET Operations Dashboard — Master Plan

## Mission

Build a world-class operational dashboard platform for Energy Transfer's North
Louisiana and East Texas gas processing assets. The platform will ultimately
cover:

- Cryogenic Plants
- Fractionation Facilities
- Amine Plants
- Future processing assets as they are added

**Initial facility:** Waskom Plant
- Cryogenic Train #1
- Cryogenic Train #2
- Cryogenic Train #3
- Fractionation Facility

The goal is a web application that provides the same situational awareness as
the plant control room HMI screens, while adding operational analytics, KPIs,
optimization targets, alerting, and performance trending.

## Immediate Priorities

1. **Project Repository** — maintain organization, remove obsolete files,
   improve project structure, document architecture decisions, and keep
   dependencies, frameworks, and MCP servers current.

## UI Design Standards

The dashboard should be modern, easy to navigate, and work on desktop,
tablet, and large screens. It should use color-coded KPI indicators and
consistent visual styling, and be optimized for operators and engineers.

Design principles: minimal clicks, maximum visibility, clean tables, highly
readable trends, fast page loads, consistent navigation — in the spirit of
modern SCADA / PI Vision / Ignition Perspective / high-performance HMI
design.

## Application Structure

### Home Page — Asset Overview Table

| Plant | Description | Cryo Count | Frac Count | Amine Count | Capacity |
|---|---|---|---|---|---|
| Waskom | 3 Cryo + 1 Frac | 3 | 1 | 0 | XXX MMSCFD |

Capacity should show both individual unit capacities and combined facility
capacity.

### Facility Pages

Each plant gets its own section:

```
Waskom
├── Summary
├── Targets
├── Control Room Screens
├── Equipment
├── Products
├── Trends
├── Reliability
├── Energy
├── Optimization
├── Commercial & Economics
└── Reports
```

### Plant Summary Page

Time windows: Hourly Average (previous rolling hour), Previous Day (prior
calendar day), Month-To-Date (current month).

Metrics: Inlet Flow, Inlet Pressure, Residue Flow, NGL Flow, C2 Recovery,
Fuel Consumption, Electricity Usage, Propane Production, Ethane Production,
Product Recoveries, Downtime, Availability, Compressor Load. This list is
expandable.

### Target Tracking Page

Initial target categories, designed to accommodate at least 20 additional
future targets:

- **Recovery** — C2 Recovery, C3 Recovery, Product Recoveries
- **Fractionation** — Depropanizer C2/C3 Ratio, Deethanizer C3/C2 Ratio
- **Energy** — Fuel %, Electric Usage, Compression Efficiency
- **Throughput** — Inlet Flow, NGL Yield, Product Yield
- **Product Quality** — Ethane Purity, Propane Purity, iC4 Purity, nC4
  Purity, Gasoline Specifications

### Control Room Screens

Approximately 70 process screens replicating control-room visualization,
enhanced with analytics and navigation. Sources: P&IDs, control room
screenshots, historian tags, operator knowledge.

### Advanced Trend Pages (3–5 pages)

- **Recovery Optimization** — C2 Recovery vs Inlet Flow, C2 Recovery vs
  Tower Temperature
- **Energy** — Fuel Usage Trends, Electric Consumption Trends, Energy
  Intensity
- **Fractionation** — Tower Differential Temperatures, Reflux Performance,
  Product Purity Trends
- **Reliability** — Compressor Run Hours, Pump Starts, Filter DP Trends
- **Plant Health** — composite KPI scoring for Throughput, Recovery, Energy,
  Reliability

### Major Process Pages

- **Inlet Separation** — Flow, Pressure, Temperature, Levels, Separator
  Data, Filter Data, DP Across Filters, Feed Split to Cryo Trains
- **Cryogenic Plant Pages** (one per train) — Tower Data, Cold Box, Cold
  Separator, Residue Gas, NGL Product, Mechanical Data
- **Fractionation Area** (per tower) — Process, Internal Data, Reflux
  System, Pumps, Product Quality

### Product Management Page

Track Ethane, Propane, i-Butane, n-Butane, Natural Gasoline: Production
(current/daily/monthly rate), Product Quality (purity, composition), and
Destinations (e.g., pipeline vs. truck rack, with rate).

### Commercial & Economics Page

See [`commercial-and-economics.md`](./commercial-and-economics.md) for the
full specification, including margin, constraint value, and product routing
calculations.

## Future Data Sources

- **P&IDs** — process flow, equipment hierarchy, instrumentation validation
- **Control Room Screens** — operator views, critical KPIs, workflows
- **Historian Tags** — live process data, trends, KPI calculations, alerts

## Ultimate Objective

Combine control room visualization, historian analytics, operational
intelligence, reliability engineering, process engineering, economic
optimization, energy management, product quality management, machine
learning, and executive reporting into a single, unified,
world-class Operations Intelligence Platform — designed from day one to
scale to dozens of facilities with minimal added effort.
