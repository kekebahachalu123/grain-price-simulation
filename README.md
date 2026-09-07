# Local Grain Market Price Simulation

**Author:** Kekeba Hachalu
**Context:** Extension of a Mathematics project originally completed with a team at ODA Special Boarding School (Maths Department), modeling teff, wheat, and maize price fluctuation in the Koye Feche sub-city market, Ethiopia.

## The problem

Staple grain prices in Ethiopia swing month to month due to seasonality, supply shocks, and demand pressure. Farmers deciding when to sell and households budgeting for food both need to reason about *risk*, not just a single predicted number. Our original school project fit a deterministic exponential growth model, `P(t) = P0 * e^(rt)`, using real data collected from the Koye Feche Trade and Agricultural Offices. That model is a solid first approximation, but it produces one number, not a range — it can't tell you how *likely* a spike or crash is.

## What this adds

This repository extends that model with a **Monte Carlo simulation** (`price_simulation.py`) built on Geometric Brownian Motion plus a seasonal adjustment, using the same growth rates (`r`) derived in the original project as the drift term. Instead of one forecast, it produces:

- A full distribution of plausible prices, 4 months out, across 10,000 simulated paths per crop
- 50% and 90% confidence intervals
- A simple, explainable **early-warning alert** (`STABLE` / price-spike / price-drop) — a rough prototype of the SMS/app-based alert idea proposed in the original project's "Future Uses" slide

## Files

| File | Purpose |
|---|---|
| `price_simulation.py` | Core simulation: GBM + seasonality, Monte Carlo runner, summary stats, CSV export |
| `plot_simulation.py` | Generates the fan chart and distribution plots |
| `simulation_summary.csv` | Example output: mean, median, 5th/95th percentile, and alert per crop |

## Running it

```bash
pip install numpy matplotlib
python price_simulation.py    # prints summary stats, writes simulation_summary.csv
python plot_simulation.py     # writes fan_chart.png and distribution.png
```

## Example output
