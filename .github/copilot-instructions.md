# Copilot Instructions — ET Operations Dashboard

These instructions apply to all work in this repository. See
[`docs/master-plan.md`](../docs/master-plan.md) for the full application
plan and [`docs/commercial-and-economics.md`](../docs/commercial-and-economics.md)
for the Commercial & Economics page specification.

## Mission

Build a world-class operational dashboard platform for Energy Transfer's
North Louisiana and East Texas gas processing assets (Cryogenic Plants,
Fractionation Facilities, Amine Plants, and future assets), starting with
the Waskom Plant. The platform must provide the same situational awareness
as control-room HMI screens, plus operational analytics, KPIs, optimization
targets, alerting, and performance trending.

## Advanced Engineering Philosophy

Always think beyond the immediate task and consider the entire operating
facility as a connected system. Continuously look for opportunities to
improve Recovery, Throughput, Reliability, Product Quality, Energy Usage,
Operating Cost, Capital Efficiency, Asset Utilization, Maintenance
Effectiveness, and Process Stability. When reviewing plant data or building
dashboard functionality, look for hidden relationships, bottlenecks,
constraints, inefficiencies, and optimization opportunities — thinking like
a Process Engineer, Production Engineer, Operations Supervisor, Reliability
Engineer, and Plant Manager simultaneously. Ask: What is limiting
throughput? What is limiting recovery? What is limiting reliability? What
would make operators more effective? What information is missing or should
be calculated but isn't? What potential problems are developing before they
become losses?

## Software Architecture Standards

Prefer modular design, reusable components, clean code, strong typing,
configurable systems, low coupling, high cohesion, clear documentation,
scalable folder structures, reusable APIs, and centralized configuration.
Avoid hardcoded plant-specific values, duplicate business logic, one-off
solutions, and temporary fixes that become permanent architecture. Design
every solution assuming dozens of facilities will eventually use the
platform.

## User Experience Philosophy

The dashboard should not merely display data — it should guide decision
making, and be intuitive for Operators, Engineers, Supervisors, Managers,
and Executives alike. Every page should answer, as fast as possible:

1. Is the plant operating normally?
2. What is limiting performance?
3. What changed recently?
4. Where is money being lost?
5. Where are the optimization opportunities?
6. What needs attention immediately?
7. What should be monitored closely?
8. Why did it change?
9. What should I do next?

Users should never have to search for critical information. Continuously
improve readability, navigation, click reduction, trend quality, KPI
visibility, mobile support, and page-load speed. Flag any page that
requires more than three clicks to reach commonly used information as an
improvement opportunity. Prioritize clarity and usefulness over complexity.

## Operational Awareness

Continuously think about equipment failures, process instability, recovery
losses, energy inefficiencies, product contamination, analyzer problems,
data quality problems, instrument failures, and compressor/pump/exchanger/
fractionation performance. Recommend dashboards and visualizations that
surface issues before operators would otherwise notice them.

## Data Quality Philosophy

Never assume data quality. Continuously consider historian integrity, tag
mappings, unit conversions, calculation accuracy, missing data, stale
values, flatlined sensors, and questionable signals. Every calculated
metric shown in the platform must clearly identify: source tags,
calculation methodology, assumptions, units, and data confidence.

## Machine Learning and Advanced Analytics

Continuously look for opportunities to apply Machine Learning, Anomaly
Detection, Predictive Analytics, Forecasting, Statistical Analysis, Pattern
Recognition, and Process Optimization Algorithms. Document potential
enhancements even when not immediately implemented, and maintain an ongoing
backlog of ML opportunities, predictive maintenance ideas, optimization
opportunities, advanced trend concepts, reliability insights, and energy
reduction opportunities.

## Economic Optimization

Always consider financial impact, and estimate it whenever practical:
revenue increases, margin increases, recovery improvements, fuel/electrical
savings, maintenance savings, downtime reduction, and throughput increases.

The **Commercial & Economics** page (see
[`docs/commercial-and-economics.md`](../docs/commercial-and-economics.md))
is the primary home for this analysis, and should let Commercial and
Operations answer "what is the most economical way to run the plant today?"
using current product prices, transportation costs, contract obligations,
and process constraints. In summary:

- **Net Margin** = Revenue (production × price, per product/destination) −
  Operating Cost (fuel, electricity, compression, transportation, storage).
- **Economic value of a constraint** = incremental product volume enabled
  by relaxing the constraint × net price of the affected product(s),
  summed across all products the constraint affects, reported as
  daily/monthly/annual value alongside confidence and implementation
  difficulty.
- **Product routing optimization** = for each product with multiple
  destinations, compute net-back margin (price − transportation − handling
  − quality penalty) per destination, honor contractual/physical
  constraints first, then route incremental volume to the highest net-back
  destination; show current vs. optimal routing and the value delta.
- **Opportunity ranking** = rank all improvement opportunities by
  `(Estimated Annual Value × Confidence Factor) / Effort Factor`, and
  re-rank automatically as pricing/production data updates.

## Continuous Improvement

Maintain active backlogs for: Dashboard Improvements (new KPIs,
visualizations, navigation, reports), Process Improvements (recovery,
throughput, energy, reliability opportunities), Commercial Opportunities
(product optimization, routing optimization, margin improvements, contract
optimization), and Data Improvements (missing tags, instrumentation gaps,
analyzer issues, data quality concerns). Every backlog item should include
potential value, estimated effort, priority, and expected impact. When work
is completed, identify the next-most-valuable step for advancing the
platform — do not wait to be asked.

## Page Design Expectations

Every page should strive to become the best possible version of itself.
Continuously improve layout, navigation, color usage, data density,
readability, trend design, KPI presentation, mobile responsiveness,
executive reporting, and operator usability. Never settle for "good
enough" — each revision should be cleaner, faster, more useful, and more
valuable than the last.

## Ultimate Objective

This is not just a set of dashboards — it is Energy Transfer's future
Operations Intelligence Platform, combining Control Room Visualization,
Historian Analytics, Operational Intelligence, Reliability Engineering,
Process Engineering, Economic Optimization, Energy Management, Product
Quality Management, Machine Learning, and Executive Reporting into a single
world-class system, built for scale from day one.

## Tooling

See [`docs/mcp-servers.md`](../docs/mcp-servers.md) for recommended MCP
servers and rationale. Keep dependencies, frameworks, and MCP servers
current as part of routine maintenance.
