# Awesome-Predictive-AI-Sales-Forecasting

# Awesome Predictive AI & Sales Forecasting

> A curated list of top Predictive AI and Sales Forecasting platforms — both SaaS/Hosted commercial revenue intelligence suites and open-source alternatives for forecasting pipeline, predicting deal outcomes, and modeling B2B revenue.
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
  - [Clari](#clari)
  - [BoostUp.ai](#boostupai)
  - [Salesforce Einstein Forecasting](#salesforce-einstein-forecasting)
  - [Gong](#gong)
  - [Aviso](#aviso)
  - [Revenue.io](#revenueio)
- [Open-Source Software](#-open-source-software)
  - [b2b-revenue-forecasting](#b2b-revenue-forecasting)
  - [pipeline-diff](#pipeline-diff)
  - [overnight-gtm](#overnight-gtm)
  - [SalesIQ](#salesiq)
- [Comparison at a Glance](#-comparison-at-a-glance)
- [Contributing](#-contributing)

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted Predictive AI and Sales Forecasting platforms. These are not open-source but are included as reference points for feature comparison.

### Clari
**Type:** Revenue orchestration with AI forecast projections
Clari is the long-standing enterprise standard for revenue forecasting, claiming **95%+ forecast accuracy** by triangulating CRM data, email, calendars, and third-party signals into a single time-series model [citation:6]. Its **Forecast Projections** and **Deal Inspection** agents predict slipping deals, surface hidden trends, and flag risks before they impact the number [citation:6]. Clari supports subscription, usage, enterprise, and hybrid models in one forecast, with **Revenue Cadences** to standardize forecasting rhythms across teams [citation:6]. Gartner reviewers praise its real-time pipeline visibility and Salesforce integration, though some note activity tracking complexity and a desire for deeper AI-native insights [citation:13].  
**Best for:** Enterprises needing a mature, explainable forecast that holds up in board reviews, with AI agents for risk detection and cadence workflows.

### BoostUp.ai
**Type:** AI forecasting for PLG and consumption-based revenue
BoostUp specializes in **product-led growth (PLG) and consumption-based forecasting**, unifying usage patterns, credits, API calls, and workload-level data with sales pipeline [citation:7]. It can interface directly with data warehouses to access consumption data outside the CRM, with read-write CRM access and custom hierarchy rollups [citation:7]. Its **machine forecasting** projects consumption at workload and account level based on historical trends and cohort benchmarks, blending ML with human judgment [citation:7]. Claims up to **95% forecasting accuracy** across subscriptions, consumption, renewals, and PLG, with 20-30% higher renewal/expansion rates and 25% higher quota attainment [citation:7][citation:14].  
**Best for:** SaaS and usage-based businesses where revenue is driven by consumption metrics rather than seat counts, particularly those with data warehouse-resident usage data.

### Salesforce Einstein Forecasting
**Type:** Native AI forecasting within Sales Cloud
Einstein Forecasting provides prediction columns and panels inside Salesforce, available only to **Forecast Managers** (not individual reps) [citation:5]. Activation requires **12+ months of Opportunity history**, at least **80% of open Opportunities with Amount populated**, standard fiscal year, and User Role forecast hierarchy (Territory forecasts are not supported) [citation:5]. Predictions are generated for the **current period only** and purged when the next period begins [citation:5]. It surfaces anomalies and trend insights but is positioned as assistance rather than autonomous planning [citation:12].  
**Best for:** Salesforce customers already running Collaborative Forecasts who meet the data prerequisites and want native AI predictions without a separate vendor.

### Gong
**Type:** Revenue intelligence with conversation-based forecasting
Gong analyzes sales calls, emails, and meetings to surface deal risks and forecast insights, combining conversation intelligence with revenue analytics. It is frequently compared to Clari, with a strong reputation for conversation depth.

### Aviso
**Type:** AI-first forecasting and revenue operations
Aviso is one of the earliest AI-first RevOps platforms (founded 2012), covering AI forecasting, deal inspection, pipeline analytics, and basic AI coaching. It targets enterprise revenue ops teams wanting AI depth without Clari's bundling pressure.

### Revenue.io
**Type:** Revenue operations with real-time guidance
Revenue.io provides real-time guidance and conversation analytics for sales teams, with forecasting capabilities layered on top of its engagement data.

---

## 🟩 Open-Source Software

Self-hosted, community-driven Predictive AI and Sales Forecasting tools. The open-source ecosystem is **fragmented** — most projects are libraries, CLIs, or narrow pipelines rather than full revenue intelligence platforms.

### b2b-revenue-forecasting
**Stack:** Python / pandas | **License:** Open Source (PyPI)
b2b-revenue-forecasting is a Python library for **B2B revenue forecasting and quota cascading** with hierarchical sales organizations [citation:2][citation:4]. Key capabilities include:
- **Metric weighting via Pearson correlation**: `suggest_weights()` proposes magnitudes and explains the rationale, with a `direction_matches_data` check 
- **Quota cascading** through multi-level hierarchies, with **brand-new IC carve-outs** (equal-share before proportional split) 
- **Commit reconciliation**: `CommitReconciler` detects and corrects forecasting bias (e.g., a sandbagging manager whose commits consistently understate actuals by 1.5x gets their commit inflated automatically) 
- **Gate handling**: fully-gated subtrees either redistribute to siblings or strand at the deepest non-gated ancestor, with `unallocated` reporting 
- **Every output is a pandas DataFrame** for CSV, SQL, or dashboard export 

The library has evolved through multiple versions with robust handling of dirty hierarchies (self-loops, blank cells, cyclic graphs) that previously crashed the cascade [citation:4].  
**Best for:** RevOps and finance teams wanting programmatic, auditable quota and forecast modeling with bias correction, particularly where custom hierarchy logic or sandbagging detection is needed.

### pipeline-diff
**Stack:** Python / HubSpot & Salesforce connectors | **License:** Open Source (PyPI)
pipeline-diff is a CLI and dashboard tool for **pipeline change analysis**, tracking how deals move between forecast categories over time [from previous context]. It syncs deal snapshots from HubSpot or Salesforce, then answers questions like "which deals were pushed out this quarter" or "what changed since the last sync." It includes a demo mode generating two years of synthetic pipeline history, and exports reports designed for AI agent consumption.  
**Best for:** RevOps analysts wanting to understand **why pipeline changed** rather than just seeing a static forecast, with local-first operation.

### overnight-gtm
**Stack:** Python / PostgreSQL / Supabase | **License:** MIT
overnight-gtm is an open-source **AI operating layer for go-to-market**, built on Atomic CRM (MIT) with agent loops for RevOps functions governed in Postgres [citation:10]. It focuses on **governance and autonomy for AI agents**: twelve loops (account planning, conversation capture, territory design, comp ops) start at low autonomy and earn promotion only when their record clears a bar (reviewed decisions, replay evals, holdout experiments, zero policy violations) [citation:10]. An independent adversarial review found 14 of 15 attacks allowed on stock Atomic CRM versus **0 of 15 with overnight-gtm's migrations**, with high-severity RLS findings reduced from 33 to 0 [citation:10]. It explicitly states it is **not** a maintained AI-native CRM for a small team without a GTM engineer—the honest answer is usually to buy one and borrow the method [citation:10].  
**Best for:** Technical GTM teams wanting a governed, auditable foundation for AI agents operating on CRM data, particularly those with a GTM engineer who can configure the ledger and permission model.

### SalesIQ
**Stack:** Python / Flask / SQLite or MySQL | **License:** Open Source
SalesIQ is a clean, modular Flask app for sales management and forecasting, with CRUD for products, customers, and sales, plus a dashboard showing KPIs, monthly sales, and a **6-month forecast** using ARIMA (statsmodels SARIMAX) with fallback to Linear Regression if statsmodels is unavailable [citation:9]. It includes CSV export and a Bootstrap/Chart.js UI.  
**Best for:** Small businesses and developers wanting a lightweight, self-hosted sales forecasting dashboard with minimal setup, accepting basic statistical models rather than advanced ML.

---

## 📊 Comparison at a Glance

| Software | License | Stack | B2B/Quota Focus | Bias Correction | Agent Governance | Self-Hosted | Best For |
|----------|---------|-------|-----------------|-----------------|------------------|-------------|----------|
| **Clari** | Proprietary | Cloud | ✅ | (AI projections) | (Deal agents) | ❌ | Enterprise forecast accuracy |
| **BoostUp.ai** | Proprietary | Cloud | ✅ PLG/consumption | (ML + judgment) | (AI agents) | ❌ | Usage-based forecasting |
| **Einstein** | Proprietary | Salesforce | ✅ (Forecast Managers) | ❌ | ❌ | ❌ | Native Salesforce predictions |
| **b2b-revenue-forecasting** | Open Source | Python/pandas | ✅ Hierarchical quotas | ✅ CommitReconciler | ❌ | ✅ | Programmatic quota + bias fix |
| **pipeline-diff** | Open Source | Python | (Pipeline changes) | ❌ | (Agent export) | ✅ | Why pipeline moved |
| **overnight-gtm** | MIT | Python/Postgres | (RevOps loops) | ❌ | ✅ Earned autonomy | ✅ | Governed AI agent ledger |
| **SalesIQ** | Open Source | Flask/SQLite | ❌ | ❌ | ❌ | ✅ | Small business sales forecast |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source Predictive AI or Sales Forecasting tool that should be listed here, please open a pull request with:

- Project name and URL
- Brief description (1–2 sentences)
- Stack and license
- Why it stands out

Please ensure the project is actively maintained (releases within the last 12 months) and genuinely open-source. Note that the open-source ecosystem for **full revenue intelligence** is essentially nonexistent—commercial platforms like Clari and BoostUp remain far more capable for end-to-end pipeline inspection, conversation intelligence, and board-ready forecasting. The available open-source projects fill specific gaps: **b2b-revenue-forecasting** provides rigorous, auditable quota math with bias correction , **pipeline-diff** explains pipeline movement , **overnight-gtm** offers a governed ledger for AI agents operating on CRM data , and **SalesIQ** provides a lightweight small-business forecasting dashboard .

---

## 📄 License

This list is released under CC0 1.0 Universal (Public Domain). The software projects listed retain their respective licenses.

---

⭐ **If this list helped you discover a useful tool, please star the repo!** ⭐
