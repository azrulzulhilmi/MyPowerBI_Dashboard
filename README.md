<p align="center">
  <img src="https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black" alt="Power BI"/>
  <img src="https://img.shields.io/badge/Data%20Analytics-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white" alt="Data Analytics"/>
  <img src="https://img.shields.io/badge/Dashboard-FF6F61?style=for-the-badge&logo=tableau&logoColor=white" alt="Dashboard"/>
</p>

# 📊 Power BI Dashboard Portfolio

A collection of interactive Power BI dashboards built for data-driven decision making. Each dashboard demonstrates different analytical approaches — from customer service analytics to project portfolio management and insurance policy monitoring.

---

## 🗂️ Dashboards Overview

### 1. 🛡️ Customer Complaint Dashboard

> **File:** `Customer Complaint Dashboard.pbix`

![Customer Complaint Dashboard](Customer_Complaint_Dashboard.png)

#### What It's About
This dashboard provides a **comprehensive view of customer complaint management** across multiple service channels. It helps support teams and management identify complaint patterns, prioritize resolution efforts, and monitor customer satisfaction in real-time.

#### Key Metrics & Visuals
| Component | Description |
|---|---|
| **Total Complaints** | Overall complaint count — **2,073** tickets tracked |
| **Complaints Resolved** | Number of successfully resolved cases — **674** |
| **Complaints by Ticket Priority** | Donut chart breaking down tickets by severity: Critical, High, Medium, and Low |
| **Complaints by Type** | Bar chart showing categories: Technical Issue (453), Refund Request (426), Cancellation Request (408), Billing Inquiry (398), Product Inquiry (388) |
| **Complaints by Product Purchased** | Horizontal bar chart highlighting top products with most complaints: Philips Hue Lights (64), Amazon Kindle (61), Apple AirPods (59), Autodesk AutoCAD (59), Canon DSLR Camera (59) |
| **Complaint Channel Filter** | Interactive slicer to filter by channel: Chat, Email, Phone, Social Media |
| **Complaint Trends (2020 & 2021)** | Line chart comparing monthly complaint volumes year-over-year |
| **Complaints by State** | Geographic map visualizing complaint distribution across US states |
| **Customer Satisfaction Rating** | Gauge chart showing average rating — **3.08 / 5** |

#### Insights
- Ticket priority is evenly distributed (~24-26% each), suggesting no single severity dominates
- Technical issues are the leading complaint type
- Customer satisfaction sits at 3.08 — below the midpoint of 3.5, indicating room for improvement
- Complaint volumes show seasonal fluctuation with peaks mid-year

---

### 2. ⚡ Project Management Dashboard

> **File:** `Project Management Dashboard.pbix`

![Project Management Dashboard](Project_Management_Dashboard.png)

#### What It's About
This dashboard serves as a **project portfolio command center** for tracking project performance, costs, and benefits across multiple initiatives. It enables project managers and executives to monitor completion rates, compare cost vs. benefit by region, and assess project phases — all within a selected time period.

#### Key Metrics & Visuals
| Component | Description |
|---|---|
| **Project Completion** | Overall completion rate — **0.87%** (early-stage portfolio) |
| **Project Benefit** | Total aggregated benefit value — **8.84M** |
| **Project Cost** | Total aggregated project cost — **4.09M** |
| **Select Period** | Interactive slider to filter data between **2022–2025** |
| **Project Benefits (by Region)** | Donut chart: South (8.74M), West (8.9M), East (8.89M), North (8.87M) |
| **Project Cost (by Region)** | Donut chart: South (3.38M), North (4.54M), West (3.92M), East (4.81M) |
| **Project Phases** | Horizontal bar chart: Develop (6), Implement (4), Explore (3), Plan (3), Measure (2) |
| **Project Summary Table** | Detailed table with Name, Type, Status, Benefit, and Cost per project |
| **Cost and Benefits (by Year)** | Clustered bar chart comparing annual benefit vs. cost from 2022–2025 |
| **Select Project / Project Type** | Left-panel filters for individual projects and types: Cost Reduction, Income Generation, Process Improvement, Working Capital Improvement |

#### Insights
- The portfolio has a healthy **2.16:1 benefit-to-cost ratio** (8.84M benefit vs. 4.09M cost)
- Benefits are evenly distributed across regions (~25% each)
- "Develop" phase has the most active projects, suggesting strong pipeline activity
- Project types span across Cost Reduction, Income Generation, Process Improvement, and Working Capital Improvement
- 2025 shows a significant spike in both cost (30M) and benefit (62M)

---

### 3. 📋 Reinstatement Policy Holders — Lapse Intelligence Dashboard

> **File:** *(Power BI file not included — screenshot only due to data privacy)*

![Reinstatement Policy Holders Dashboard](Reinstatement_Policy_Holders_Dashboard.png)

#### What It's About
This dashboard serves as the front-end **Lapse Intelligence tool for Tokio Marine Life Insurance (Malaysia) Bhd**, designed to monitor, forecast, and prevent policy lapses. Behind this dashboard lies a comprehensive, end-to-end data science and AI pipeline that cleans raw demographic data, forecasts macroeconomic indicators, predicts individual policyholder reinstatement probability, and uses an on-premise Large Language Model (LLM) to generate plain-language explanation notes for front-line agents.

#### 🧠 Data Science & AI Pipeline Architecture
The dashboard is powered by a multi-stage machine learning and natural language processing backend structured as follows:

```
[Raw Policy CRM Data]
       │
       ├─► [Postcode Cleaning & Spatial KNN Imputation] ──► (Imputes missing districts)
       ├─► [Macromonetary Time-Series Models] ───────────► (SARIMA CPI & Holt-Winters OPR forecasts)
       │
[Feature Engineering] (Affordability Ratio, Premium Burden Ratio, Sunk Cost Proxy)
       │
[XGBoost Classifier (SMOTE + ENN)] ──► (Calibrated probability score for Reinstatement)
       │
       ▼
[Daily Pipeline Scoring] ──► [On-Premise RAG Pipeline (Ollama AIrein)] ──► [Power BI Dashboard]
                                    ▲
                                    │ (Retrieves news context)
                            [News Vector DB (ChromaDB)]
```

##### 1. Theoretical Foundations & Hypotheses
Lapsation and reinstatement behaviors are modeled through three distinct financial hypotheses:
- **Policy Replacement Hypothesis (PRH)**: Policyholders lapse active policies when better or cheaper market alternatives become available.
- **Interest Rate Hypothesis (IRH)**: Fluctuations in systemic interest rates alter the opportunity cost of savings components, driving lapses in yield-sensitive products.
- **Emergency Fund Hypothesis (EFH)**: Personal financial distress forces policyholders to lapse policies as a cash-conservation measure, utilizing them as emergency funds.

##### 2. Demographic & Spatial Enrichment
- **Spatial Standardization (KNN)**: Cleaned and standardized Malaysian postcodes using OSM and `pgeocode`. Trained a K-Nearest Neighbors (KNN) model on coordinates to impute missing districts, states, latitudes, and longitudes to establish a reliable spatial-demographic baseline.
- **Socioeconomic Enrichment**: Standardized districts were mapped to e-Statistik Malaysia / Department of Statistics Malaysia (DOSM) data. Piecewise linear interpolation was applied to fill historical gaps in district-level median household income and cost-of-living expenditures.
- **Occupational Normalization**: Standardized raw occupation fields against the JobStreet Salary Guide and Suruhanjaya Perkhidmatan Awam (SPA) schemes, collapsing titles into four major professional groups.

##### 3. Macromonetary Time-Series Forecasting
To capture EFH and IRH dynamics, we retrieved historical Bank Negara Malaysia (BNM) indicators and trained time-series models to forecast macroeconomic trends up to December 2026:
- **Consumer Price Index (CPI)**: Modeled using a **SARIMA(1, 1, 0) x (0, 1, 1, 12)** configuration (RMSE = 0.2008). Projections were upsampled to daily frequency using a forward-fill (ffill) method.
- **Overnight Policy Rate (OPR)**: Modeled using the **Holt-Winters Exponential Smoothing** method (RMSE = 0.1283), which captures central bank rate steps and plateaus more effectively than standard stochastic models.

##### 4. Advanced Feature Engineering
Predictors are engineered by combining customer demographics, local socioeconomic baselines, and forecasted macroeconomic trends:
- *Affordability Ratio*: $\text{Annual Premium} / (\text{Monthly Household Income} \times 12)$ (income portion consumed by the policy).
- *Premium Burden Per Person*: $\text{Annual Premium} / (\text{Dependents} + 1)$.
- *Premium Burden Ratio*: $\text{Premium Burden Per Person} / (\text{Median District Expenditure} \times 12)$.
- *Sunk Cost Proxy (Estimated Total Paid)*: $\text{Months Inforce} \times \text{Premium Amount}$ (captures historical capital investment).
- *Missed Relative Tenure*: $\text{Months Missed Payment} / \text{Months Inforce}$.

##### 5. Predictive Machine Learning (XGBoost + SMOTE-ENN)
- **Validation Strategy**: Deployed an **Out-of-Time (OOT)** validation split (Training: 2021-2024; Testing: 2025) to prevent over-optimism and simulate real-world chronological forecasting.
- **Handling Class Imbalance**: The raw dataset exhibits extreme class imbalance (97.4% lapse vs. 2.6% reinstatement). We applied a hybrid **SMOTE + ENN (Edited Nearest Neighbors)** technique, which synthesizes minority instances (SMOTE) and aggressively cleans noisy, overlapping borderline data points (ENN) to establish a clear decision boundary.
- **Model Tuning & Calibration**: Trained an **XGBoost Classifier** (PR-AUC = 0.2580) using a Stratified 5-Fold Cross-Validation loop within an `ImbPipeline` to prevent data leakage. Raw outputs were calibrated using **Sigmoid Calibration** (final PR-AUC = 0.2628).
- **Threshold Optimization (F1-Max)**: Adjusted the operational threshold to **0.0846** to prioritize Recall over Precision due to the high cost of omission (losing a customer vs. making a phone call).
  - *Recall*: **37.20%** (capturing nearly 40% of all potential premium recovery).
  - *Precision*: **25.58%** (ensuring approximately 1 in 4 outbound outreach calls results in a successful reinstatement).

##### 6. On-Premise Retrieval-Augmented Generation (RAG)
To make predictions actionable, scores are fed into a secure local LLM agent (**AIrein** based on a custom `gemma3:12B` Modelfile via Ollama). This setup prevents customer data leakage by executing all inferences locally on on-premise hardware.
- **Vector Storage**: News reports, bank interest rate changes, and healthcare inflation documents are chunked and stored in a local Chroma DB using `nomic-embed-text` embeddings.
- **SHAP Translation**: For each high-probability candidate, the system extracts the top three local SHAP feature drivers (e.g., *Affordability*, *Agent Tenure*, *Total Claims*) and translates them into layman terms, combining them with retrieved vector database contexts to generate personalized outreach scripts for agents.

#### Key Metrics & Visuals
| Component | Description |
|---|---|
| **Policy Count** | Total policies tracked — **90.9K** |
| **Total Premium (RM)** | Combined premium value — **139.4M** (Malaysian Ringgit) |
| **Average Lapse Premium (RM)** | Average premium at lapse — **1.5K** |
| **Total Average Lapse Premium by Time** | Line chart showing lapse premium trends from 2021 to 2027 with notable peaks and a recent uptick at **3.1K** |
| **MoM (Month-over-Month)** | Mar 2026 vs Feb 2026 — **3.1K** (Prior: 3.0K, +3.59%) |
| **MSM (Month-Same-Month)** | Mar 2026 vs Mar 2025 — **3.1K** (Prior: 3.0K, +1.11%) |
| **SPLY (Same Period Last Year)** | 2026 vs 2025 — **2.7K** (Prior: 1.6K, +31.45%) |
| **12-Month Rolling Average** | Area chart with rolling average overlaid against monthly premiums from 2020–2022 |
| **State-Level Lapse Performance** | Horizontal bar chart ranking Malaysian states — Negeri Sembilan leads at **2,275**, followed by Pulau Pinang and Kedah |
| **Filters** | Policy Status, Date Range, State, Year, and Product Code slicers |
| **Navigation** | Sidebar with sections: Overview, Customer, Agency and Product, Others Lapse Driver |

#### Insights
- **Macroeconomic Correlation**: Lapses show strong statistical correlation with upward movements in the time-series OPR and CPI indexes, pointing to macroeconomic stress (EFH) as a primary driver.
- **Geographic Vulnerability**: Negeri Sembilan exhibits the highest average lapse premium, matching areas where the affordability ratio (premium burden relative to district-level disposable income) is elevated.
- **Lapse Momentum**: Lapse premiums have been trending upward since mid-2024, reaching 3.1K — a **31.45% YoY increase**.
- **Actionable AI Support**: Embedding the on-prem local RAG explanations in the workflow enables agents to offer context-aware retention support (e.g. suggesting policy adjustment or premium holidays based on the specific driver identified by the LLM).

#### Remarks
- The value above is all dummy data.

---

## 🛠️ Tools & Technologies

- **Microsoft Power BI Desktop** — Dashboard development and data modeling
- **DAX (Data Analysis Expressions)** — Calculated measures and KPIs
- **Power Query (M Language)** — Data transformation and ETL
- **Bing Maps / Microsoft Maps** — Geographic visualizations

## 📁 Repository Structure

```
📦 dashboard/
├── 📄 README.md
├── 📊 Customer Complaint Dashboard.pbix
├── 🖼️ Customer_Complaint_Dashboard.png
├── 📊 Project Management Dashboard.pbix
├── 🖼️ Project_Management_Dashboard.png
└── 🖼️ Reinstatement_Policy_Holders_Dashboard.png
```

## 🚀 How to Use

1. **Clone** this repository
   ```bash
   git clone https://github.com/azrulzulhilmi/MyPowerBI_Dashboard.git
   ```
2. **Open** the `.pbix` files in [Power BI Desktop](https://powerbi.microsoft.com/desktop/)
3. **Interact** with the slicers, filters, and visuals to explore the data

> **Note:** Some dashboards may require reconnecting to their original data sources. Sample data is embedded where available.

## 👤 Author

**Azrul Zulhilmi**  
📧 [azrulzulhilmi@users.noreply.github.com](mailto:azrulzulhilmi00@gmail.com)  
🔗 [GitHub Profile](https://github.com/azrulzulhilmi)

---

<p align="center">
  <i>Built with 💡 data storytelling and Power BI</i>
</p>
