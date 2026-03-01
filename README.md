# Nigeria Food Supply Chain — Demand Forecasting & Inventory Optimization

> A Python-based system that forecasts weekly food commodity demand across major Nigerian markets and generates data-driven inventory recommendations.

---

## Overview

Nigeria's food supply chain is shaped by seasonal agricultural cycles, festive demand spikes (Ramadan, Sallah, Christmas), and frequent supply disruptions from flooding and poor road infrastructure. This project tackles the core operational challenge faced by food commodity managers: **knowing when to reorder, how much to order, and where stockout risk is highest.**

The system generates a realistic synthetic dataset, runs demand forecasts, computes optimal inventory parameters, and surfaces everything through visual dashboards — all in a single notebook.

---

## Features

-  **Demand Forecasting** — 12-week forecasts per market-commodity pair using Holt-Winters Exponential Smoothing (avg. MAPE < 15%)
-  **Inventory Optimization** — Economic Order Quantity (EOQ), safety stock, and reorder points at a 95% service level
-  **Reorder Alerts** — 5-tier colour-coded alert system: `STOCKOUT` · `CRITICAL` · `LOW` · `MODERATE` · `ADEQUATE`
-  **Visual Dashboards** — Demand trend charts, inventory heatmap, stock vs reorder point, cost breakdown, EOQ analysis
-  **Nigeria-specific** — Encodes harmattan season, rainy season, Christmas/New Year (+60%), Ramadan, Sallah, end-of-month salary effects, and random supply shocks

---

## Markets & Commodities

| Markets | Commodities |
|---|---|
| Lagos, Kano, Abuja | Rice (50kg), Maize (50kg), Yam, Tomatoes |
| Port Harcourt, Onitsha, Ibadan | Palm Oil (25L), Garri (50kg), Beans (50kg), Groundnut Oil (20L) |

---

## Tech Stack

| Tool | Purpose |
|---|---|
| `Python` | Core language |
| `Pandas` / `NumPy` | Data generation & manipulation |
| `Statsmodels` | Holt-Winters forecasting (ARIMA available) |
| `Matplotlib` / `Seaborn` | Visualizations & dashboards |
| `Google Colab` | Runtime environment |

---

## Getting Started

No installation needed. Open directly in Google Colab:

1. Upload `nigeria_food_inventory_colab.ipynb` to [colab.research.google.com](https://colab.research.google.com)
2. Click **Runtime → Run all**
3. All outputs — dataset, forecasts, alerts, and charts — generate automatically

---

## Project Structure

```
nigeria_food_inventory_colab.ipynb   ← Single notebook
nigeria_food_supply.csv              ← Auto-generated dataset 
```

---

## How It Works

```
Generate Dataset → Exploratory Analysis → Demand Forecasting
       ↓
Inventory Optimization (EOQ + Safety Stock + ROP)
       ↓
Reorder Alerts → Visual Dashboards → Summary Report
```

### Demand Patterns Built Into the Data

| Pattern | Effect |
|---|---|
| Harmattan (Nov–Feb) | −15% demand |
| Rainy season (Apr–Oct) | +10% demand |
| Christmas / New Year | +60% demand spike |
| Ramadan & Sallah | +25–35% demand spike |
| End-of-month salary effect | +10% demand |
| Supply disruptions | −25% to −50% stock availability |

### Inventory Formulas

```
EOQ  = √(2 × Annual Demand × Ordering Cost / Holding Cost)
Safety Stock  = Z × σ_demand × √(lead time in weeks)    [Z = 1.645 for 95% service level]
Reorder Point = Avg demand × lead time + Safety stock
```

---

## Sample Outputs

**Reorder Alert Table**
```
🚨 URGENT   | Lagos         | Rice (50kg bag)    | OUT OF STOCK — order 540 units
🔴 CRITICAL | Kano          | Tomatoes (basket)  | 0.8 wks left — order 1,200 units
🟡 REORDER  | Port Harcourt | Palm Oil (25L)     | Below ROP (140 < 210) — order 320 units
✅ OK       | Abuja         | Garri (50kg bag)   | 3.1 weeks of stock remaining
```

---

## Limitations

- Dataset is synthetic — validate against real transaction data before live deployment
- Commodity prices and ordering costs are held constant; real Naira fluctuations are not modelled
- Ramadan/Sallah dates use fixed approximations (lunar calendar shifts yearly)
- Single-echelon model only (market level); does not optimise across the full supply chain
