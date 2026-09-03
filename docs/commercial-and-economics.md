# Commercial & Economics Page — Specification

## Purpose

Operations pages show *how the plant is running*. The Commercial & Economics
page shows *how the plant should run today* given current product prices,
transportation costs, contract obligations, and process constraints. It is
intended for use by both Operations/Engineering and Commercial teams, and
should recommend the most economical way to operate each day.

Every facility page should answer:

- What is the plant making today, and what is it worth?
- Where is economic value being lost?
- What is the highest-value operating mode available right now?
- What process changes would create additional profit?
- Which products/destinations should be emphasized today?
- What constraints are preventing additional value capture?

## Data Inputs

| Category | Examples |
|---|---|
| Production | Ethane, Propane, iC4, nC4, Gasoline, Residue Gas rates |
| Pricing | Daily/settlement prices per product, per destination |
| Transportation | Pipeline tariffs, trucking cost per gallon/mile, storage/handling fees |
| Operating cost | Fuel gas consumption × fuel value, electricity usage × rate, estimated compression cost |
| Constraints | Equipment/process limits (recovery, throughput, purity, compressor load) |
| Contracts | Take-or-pay obligations, minimum/maximum delivery volumes, dedicated pipeline capacity |

Every value used in a calculation must carry its source tag, unit, and a
data-confidence flag (Good / Suspect / Stale / Manual), consistent with the
platform's data quality philosophy (see `.github/copilot-instructions.md`).

## 1. Daily Margin Calculation

**Revenue** — sum of production × price across products and destinations:

```
Revenue = Σ (Production_i × Price_i)   for i in {Ethane, Propane, iC4, nC4, Gasoline, Residue Gas}
```

**Variable Operating Cost:**

```
Operating Cost = Fuel Gas Cost + Electricity Cost + Compression Cost
                + Transportation Cost + Storage/Handling Cost
```

**Net Margin:**

```
Net Margin = Revenue − Operating Cost
```

Net Margin should be shown for Hourly, Previous Day, and Month-to-Date
windows, consistent with the Plant Summary page.

## 2. Economic Value of a Constraint

A "constraint" is any process limit that, if relaxed, would change
production and therefore revenue (e.g., C2 recovery, tower temperature
limit, compressor throughput, product purity giveaway).

**Method — Marginal Value Analysis:**

1. Identify the constrained variable and the production response to a
   1-unit change in that variable (e.g., "+1% C2 Recovery → +5,000 gal/day
   Ethane"), derived from historian correlation, mass balance, or process
   simulation.
2. Multiply the incremental product volume by its current net price
   (price minus any incremental variable cost, such as transportation, that
   scales with volume):

```
Daily Value  = Incremental Volume/day × Net Price per unit
Monthly Value = Daily Value × Days in Month (or MTD actual, projected)
Annual Value  = Daily Value × 365
```

3. Where relaxing the constraint changes more than one product (e.g.,
   recovering more ethane reduces residue gas), compute the **net** value as
   the sum of all product value deltas, not just the primary product:

```
Net Constraint Value = Σ (ΔVolume_product × Net Price_product) across all affected products
```

4. Display alongside: implementation difficulty, confidence level (based on
   data quality and correlation strength), and any offsetting cost (e.g.,
   additional fuel or compression required to relax the constraint).

**Example:** Increasing C2 Recovery by 1% yields +5,000 gal/day of ethane.
At $0.42/gal, that is $2,100/day, ≈ $63,900/month (30-day), ≈ $766,500/year
— before netting any change in residue gas value or added utility cost.

## 3. Product Routing Optimization

For each product with more than one available destination (e.g., Propane
via Pipeline A, Pipeline B, Storage, Truck Rack), compute the **net-back
margin** for each option:

```
Net-Back Margin_destination = Price_destination
                             − Transportation Cost_destination
                             − Handling/Storage Cost_destination
                             − Quality/Blending Penalty_destination (if any)
```

The recommended destination for incremental volume is the one with the
highest net-back margin, subject to:

- **Contractual constraints** — take-or-pay or minimum-volume commitments
  must be satisfied first; only volume beyond those commitments is
  optimized freely.
- **Physical constraints** — pipeline nominations/capacity, truck rack
  loading capacity, storage inventory limits.

```
Routing Value = Σ over destinations of
                (Volume_allocated_to_destination × Net-Back Margin_destination)
```

The page should show current routing, the optimal routing given today's
net-back margins, and the delta in value between them, so Commercial can
act on it immediately.

## 4. Opportunity Ranking

All improvement opportunities identified across Operations, Reliability,
Energy, and Commercial pages should be ranked by **expected annualized
value**, adjusted for confidence and effort:

```
Ranking Score = (Estimated Annual Value × Confidence Factor) / Effort Factor
```

Where:

- **Estimated Annual Value** — from constraint-value or routing-value
  calculations above (or an engineering estimate if no historian
  correlation yet exists).
- **Confidence Factor** — 0.0–1.0, based on data quality, correlation
  strength/sample size, and whether the estimate is empirical or
  judgment-based.
- **Effort Factor** — relative implementation effort/cost (1 = trivial
  operating change, higher = capital project, outage required, etc.).

Each ranked opportunity should display: description, estimated value
(daily/monthly/annual), confidence level, implementation difficulty/risk,
and owning discipline (Operations, Reliability, Energy, Commercial).
Opportunities should be re-ranked automatically whenever pricing or
production data updates, so the "highest-value next step" is always current
— consistent with the platform's continuous-improvement philosophy.

## Page Layout Summary

1. **Today's Economics** — Revenue, Operating Cost, Net Margin (Hourly /
   Previous Day / MTD)
2. **Constraint Value Analysis** — ranked list of active constraints with
   daily/monthly/annual value if relaxed
3. **Product Routing Optimization** — current vs. optimal routing per
   product, with value delta
4. **Opportunity Ranking** — cross-functional backlog ranked by expected
   value

All figures must clearly state source tags, calculation methodology,
assumptions, units, and data confidence, per the platform's data quality
standard.
