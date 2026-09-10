# European Inflation Decomposition Dashboard

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live%20Dashboard-brightgreen?logo=github)](https://jakubrybacki.github.io/shapiro-decomposition-inflation-dashboard/)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Data: BigQuery](https://img.shields.io/badge/Data-Google%20BigQuery-4285F4?logo=googlecloud)](https://cloud.google.com/bigquery)

Interactive research dashboard decomposing European headline inflation into **Supply**, **Demand**, and **Ambiguous** shock contributions using sign-restricted Bayesian Vector Autoregressions (BVAR) following **Adam Shapiro (2022, FRBSF)** and **European Central Bank (Gonçalves & Koester, 2022)** methodologies.

🌐 **Live Interactive Dashboard:** [https://jakubrybacki.github.io/shapiro-decomposition-inflation-dashboard/](https://jakubrybacki.github.io/shapiro-decomposition-inflation-dashboard/)

---

## 📊 Methodology & Analytical Framework

For each country and granular consumer basket category ($i$):
1. **Structural BVAR Estimation**: A 2-variable VAR(12) model is estimated linking monthly annualized inflation $\pi_{i,t}$ and real activity/output changes $\Delta q_{i,t}$.
2. **Sign-Restriction Identification**:
   - **Demand Shock**: Unexpected price and unexpected volume move in the **same direction** ($\text{sign}(\nu^p) = \text{sign}(\nu^q)$).
   - **Supply Shock**: Unexpected price and unexpected volume move in **opposite directions** ($\text{sign}(\nu^p) \neq \text{sign}(\nu^q)$).
3. **Ambiguity Band & Residual Identity**:
   - Unidentified/neutral innovations define the ambiguous zone.
   - Ambiguous shocks are computed as the exact residual between official Eurostat headline HICP inflation and identified shocks:
     $$\text{Ambiguous Shock} \equiv \text{Headline Inflation} - (\text{Supply Shock} + \text{Demand Shock})$$
   - This guarantees that $\text{Supply} + \text{Demand} + \text{Ambiguous} \equiv \text{Official Headline HICP}$ at all points in time.

---

## 🔍 Key Dashboard Features

- **Headline Inflation Decomposition**:
  - 12-Month Rolling Sum (YoY) & Month-over-Month (MoM) contributions.
  - Interactive country switch across 19 European economies.
- **Supply Shock Drivers**:
  - Breakdown into **Household Energy** (CP045), **Transport Fuels** (CP0722), **Food & Non-Alcoholic** (CP01), and **Other Supply Pressures**.
- **Demand Shock Pillars**:
  - Decomposition across **Services**, **Industrial Goods**, **Food & Beverages**, and **Energy Demand**.
- **Data Quality Safeguard**:
  - Displays periods with $\ge 50$ modeled COICOP categories, filtering out incomplete transition periods.
- **Client-Side CSV Export**:
  - Download publication-ready filtered CSV data directly from each chart card via `[ 📥 CSV ]`.

---

## ☁️ Data Infrastructure

The underlying data is prepared and partitioned in **Google BigQuery**:
- **Project:** `macroeconomic-dashboards`
- **Dataset:** `shapiro_inflation_decomposition`
- **Tables:**
  - `hicp_headline_inflation`
  - `hicp_shock_contributions`
  - `hicp_supply_drivers`
  - `hicp_demand_drivers`

---

## 🛠️ Built With

- [Quarto](https://quarto.org/) - Next-generation technical publishing system
- [Plotly R](https://plotly.com/r/) - High-performance interactive data visualization
- [Google BigQuery](https://cloud.google.com/bigquery) - Cloud data warehouse
