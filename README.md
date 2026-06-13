# 🌿 EcoTrace — Personal Carbon Footprint Tracker

> **PromptWars Submission** | Vertical: **Climate & Sustainability**

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-2dd482?style=for-the-badge&logo=github)](https://dk07-glitch.github.io/carbon-footprint-promptwars/)
![HTML](https://img.shields.io/badge/Built%20with-HTML%2FCSS%2FJS-60a5fa?style=for-the-badge)
![No Dependencies](https://img.shields.io/badge/Dependencies-Zero-f59e0b?style=for-the-badge)

---

## 🎯 Chosen Vertical — Climate & Sustainability

EcoTrace targets the **individual climate action** space — one of the most underleveraged levers in the fight against climate change. While governments and corporations dominate the climate narrative, research shows that household and lifestyle choices account for **~60–70% of global greenhouse gas emissions** (IPCC AR6, 2022).

The problem: most people have no idea what their carbon footprint actually is, let alone where it comes from or how to reduce it. EcoTrace bridges that gap with a simple, beautiful, and data-driven tool that makes the invisible visible.

---

## 💡 Approach & Logic

### Design Philosophy

The core design principle is **low friction → high insight → actionable output**. The user journey follows three steps:

```
Measure  →  Understand  →  Act
```

Rather than overwhelming users with dense data, EcoTrace guides them through a **4-step questionnaire** that covers the four major emission categories, then instantly surfaces personalized insights and ranked actions.

### Why a Single HTML File?

The entire app ships as one self-contained `index.html` with zero dependencies, zero build tools, and zero server requirements. This was a deliberate choice:
- **Instant access** — open in any browser, no install needed
- **Privacy-first** — all data stays in `localStorage`, nothing leaves the device
- **Portability** — works offline, can be shared as a file attachment

### Emission Categories Covered

| Category | Examples | Typical Weight |
|---|---|---|
| 🚗 **Transport** | Car type, km driven, flights | ~30–50% of footprint |
| ⚡ **Energy** | Electricity source, kWh usage, heating | ~20–30% |
| 🍔 **Food & Diet** | Diet type, food waste habits | ~20–30% |
| 🛒 **Lifestyle** | Shopping frequency, streaming, recycling | ~10–15% |

---

## ⚙️ How the Solution Works

### 1. Carbon Calculator (4-Step Questionnaire)

The user answers questions across 4 categories using intuitive option cards and sliders. Each input updates a **live CO₂ preview** so users immediately feel the impact of their choices.

**Emission calculation formula:**

```
Transport = (km/year × car_factor / 1000) + Σ(flights × flight_factor)

Energy    = (kWh/month × 12 × electricity_factor / 1000)
          + (heating_kWh/month × 12 × heating_factor / 1000)

Food      = diet_base_emission × food_waste_multiplier

Lifestyle = shopping_emission + (streaming_hrs/day × 365 × 0.000036)
          ± recycling_bonus
```

All factors are sourced from **IPCC AR6 (2022)** and **Our World in Data (2023)**:

| Input | Factor | Source |
|---|---|---|
| Petrol car | 0.21 kg CO₂e/km | IPCC AR6 |
| Electric car | 0.05 kg CO₂e/km | IPCC AR6 |
| Hybrid car | 0.11 kg CO₂e/km | IPCC AR6 |
| Short-haul flight | 0.255 t CO₂e/flight | DEFRA 2023 |
| Medium-haul flight | 0.600 t CO₂e/flight | DEFRA 2023 |
| Long-haul flight | 1.500 t CO₂e/flight | DEFRA 2023 |
| Mixed grid electricity | 0.233 kg CO₂e/kWh | IEA 2023 |
| Renewable electricity | 0.030 kg CO₂e/kWh | IEA 2023 |
| Coal-heavy electricity | 0.820 kg CO₂e/kWh | IEA 2023 |
| Natural gas heating | 0.202 kg CO₂e/kWh | IPCC AR6 |
| Heat pump | 0.040 kg CO₂e/kWh | IPCC AR6 |
| Vegan diet | 1.5 t CO₂e/year | Poore & Nemecek 2018 |
| Vegetarian diet | 1.7 t CO₂e/year | Poore & Nemecek 2018 |
| Omnivore diet | 2.5 t CO₂e/year | Poore & Nemecek 2018 |
| Meat-heavy diet | 3.3 t CO₂e/year | Poore & Nemecek 2018 |
| Video streaming | 36 g CO₂e/hour | The Shift Project |

### 2. Dashboard

After calculation, the dashboard renders:
- **Animated donut chart** (hand-coded SVG) showing the 4-category split with smooth draw-on animation
- **Category cards** with mini progress bars showing each category's relative contribution
- **6-month trend sparkline** (SVG path) showing historical calculations
- **Planet Impact Meter** — a gradient bar placing the user on a spectrum from 🌿 Thriving → 🔥 Critical
- **Score comparison** — user's total vs. global average (4.7 t) and 1.5°C target (2.0 t)
- **Top 3 action previews** — quick-glance highest-impact actions with CO₂ savings

### 3. Personalized Action Plan

Actions are **dynamically generated and ranked** based on the user's specific profile — not generic tips. Each action's saving is calculated directly from the user's answers:

```js
// EV switch saving is personalised to the user's actual driving habits
ev_saving = (petrol_factor - ev_factor) × km_per_year / 1000

// Diet saving is personalised to the user's current diet type
diet_saving = current_diet_emissions - vegetarian_emissions
```

Users can mark actions as **Done** or **In Progress**. A live progress bar tracks total CO₂ savings unlocked vs. the full potential available.

### 4. Insights & Comparisons

- **Comparison bar chart** — user footprint vs. Global Avg (4.7 t), US Avg (14.5 t), India Avg (1.9 t), and the 1.5°C target (2.0 t)
- **Pie chart** — % breakdown by category (Transport / Energy / Food / Lifestyle)
- **Assessment history log** — tracks changes across multiple calculations over time
- **Shareable Carbon Card** — a one-click copyable summary of the user's full footprint breakdown

### 5. Achievements (Gamification)

12 badges that unlock automatically based on profile and completed actions:

| Badge | Trigger |
|---|---|
| 🌱 First Step | Complete first assessment |
| ⚡ Action Hero | Mark first action as done |
| 🦸 Green Warrior | 5+ actions completed |
| 🥦 Plant Power | Vegan or vegetarian diet |
| ☀️ Sun Rider | Renewable electricity selected |
| 🌍 Grounded | Zero flights this year |
| 🔋 EV Rider | Drives an electric vehicle |
| 🎯 Climate Hero | Footprint ≤ 2.0 t (1.5°C target) |
| 📉 Below Average | Footprint below 4.7 t global average |
| 📊 Carbon Cutter | Reduced footprint vs. previous assessment |
| ♻️ Zero Waster | Reports very little food waste |
| 🌿 Minimalist | Minimal shopping habits selected |

### Data Persistence

All data is stored in `localStorage` under the key `eco2`. No account or login required. Data survives page refreshes and browser restarts.

```json
{
  "profile": { "carType": "petrol", "kmPerYear": 12000, "dietType": "omnivore" },
  "totals":  { "transport": 2.52, "energy": 1.07, "food": 2.70, "lifestyle": 0.90, "total": 7.19 },
  "hist":    [{ "date": "13 Jun 2026", "total": 7.19 }],
  "acts":    { "renew": "done", "veg": "doing" },
  "ach":     ["first", "below_avg"]
}
```

---

## 🔧 Assumptions Made

| # | Assumption | Rationale |
|---|---|---|
| 1 | Emission factors are **global averages**, not country-specific | Country-specific grid intensities would require a backend lookup by location |
| 2 | **Flights are one-way** — users are instructed that return trips count as 2 | Standard ICAO / DEFRA convention for flight carbon accounting |
| 3 | **Heating kWh** input is a monthly average across the year, not seasonal | Avoids complex seasonal modelling for a quick-assessment tool |
| 4 | **Streaming/digital emissions** use 36g CO₂e/hr (The Shift Project) | Conservative figure; actual varies by device, resolution, and CDN location |
| 5 | **Recycling** gives a small reduction (−0.1 t/yr "always", −0.05 t/yr "sometimes") | Recycling's direct footprint impact is modest and difficult to model precisely |
| 6 | **Diet emissions** are per-person annual averages, not per-meal | Meal-level tracking requires an ingredient database — out of scope for an MVP |
| 7 | **Shopping** uses broad buckets (Minimal → Very High) instead of exact spend | Spend-to-emissions conversion requires currency, region, and supply-chain data |
| 8 | **1.5°C compatible target** is set at 2.0 t CO₂e/person/year | Based on IPCC AR6 global pathways for limiting warming to 1.5°C by 2050 |
| 9 | **6-month trend chart** shows mock variance for months before first assessment | The app has no real historical data until the user runs multiple calculations |
| 10 | **No server-side processing** — all calculations run entirely in the browser | Ensures privacy; no user data ever leaves the device |

---

## 🚀 Running Locally

No build step or package manager needed:

```bash
# Option 1 — Open directly in browser (double-click the file)
start index.html

# Option 2 — Serve with Python
python -m http.server 8080
# Then visit: http://localhost:8080
```

---

## 📁 Project Structure

```
carbon-footprint-promptwars/
├── index.html   ← Complete self-contained app (HTML + CSS + JS, ~69 KB)
└── README.md    ← This file
```

---

## 📚 Data Sources

- [IPCC Sixth Assessment Report (AR6), 2022](https://www.ipcc.ch/assessment-report/ar6/)
- [Our World in Data — CO₂ and Greenhouse Gas Emissions](https://ourworldindata.org/co2-and-other-greenhouse-gas-emissions)
- [DEFRA UK Greenhouse Gas Conversion Factors 2023](https://www.gov.uk/government/collections/government-conversion-factors-for-company-reporting)
- [Poore & Nemecek (2018) — Reducing food's environmental impacts, Science](https://www.science.org/doi/10.1126/science.aaq0216)
- [IEA Electricity Emission Factors 2023](https://www.iea.org/data-and-statistics)
- [The Shift Project — Climate impact of online video (2019)](https://theshiftproject.org/en/article/unsustainable-use-online-video/)

---

## 👤 Author

**dk07-glitch** — PromptWars 2026 Submission

---

*Built with 🌿 and zero npm installs.*