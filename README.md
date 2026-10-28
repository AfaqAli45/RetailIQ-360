# RetailIQ 360
### End-to-End Retail Analytics, Customer Intelligence & Sales Forecasting

**Python · SQL · SQLite · Power BI · Scikit-learn · Prophet · Association Rule Mining**

RetailIQ 360 is an end-to-end retail and supply chain analytics project that transforms transactional data into a structured analytical warehouse, customer intelligence outputs, sales forecasts, and interactive Power BI reports.

The project connects data preparation, dimensional modeling, feature engineering, advanced SQL analysis, machine learning, and business intelligence in a single workflow.

Rather than stopping at dashboard creation, RetailIQ 360 explores the underlying analytical processes: how data is organized, how business metrics are calculated, how customer behavior is segmented, and how forecasting performance is evaluated.

> **Project status:** Portfolio project with implemented analytical workflows and exploratory modeling experiments. Reproducibility improvements and modeling limitations are documented below.

---

## Table of Contents

- [Project Highlights](#project-highlights)
- [Business Problem](#business-problem)
- [Solution Architecture](#solution-architecture)
- [Technology Stack](#technology-stack)
- [Repository Structure](#repository-structure)
- [Dataset Overview](#dataset-overview)
- [Data Warehouse Design](#data-warehouse-design)
- [Data Preparation and Feature Engineering](#data-preparation-and-feature-engineering)
- [Advanced SQL Analytics](#advanced-sql-analytics)
- [Customer Intelligence and Machine Learning](#customer-intelligence-and-machine-learning)
- [Sales Forecasting and Evaluation](#sales-forecasting-and-evaluation)
- [Power BI Dashboard](#power-bi-dashboard)
- [How to Explore and Run the Project](#how-to-explore-and-run-the-project)
- [Technical Considerations and Limitations](#technical-considerations-and-limitations)
- [Future Improvements](#future-improvements)
- [Skills Demonstrated](#skills-demonstrated)
- [Data Attribution and Responsible Use](#data-attribution-and-responsible-use)

---

## Project Highlights

| Area | Implementation |
|---|---|
| Data ingestion | Load DataCo supply chain data into SQLite using Python |
| Warehouse modeling | Build an order-item fact table and customer, product, shipping, location, and date tables |
| Data preparation | Inspect missing values, duplicates, distributions, and statistical outliers |
| Feature engineering | Create profitability, pricing, discount, calendar, customer, and shipping features |
| SQL analytics | Apply aggregations, joins, CTEs, ranking, cumulative calculations, and window functions |
| Customer segmentation | Standardize RFM features and apply K-Means with five clusters |
| Customer inactivity analysis | Explore a rule-derived inactivity label using Logistic Regression |
| Market basket analysis | Generate frequent itemsets and product association rules |
| Sales forecasting | Build a 90-day Prophet forecast with uncertainty intervals |
| Forecast evaluation | Implement chronological holdout testing and rolling-origin cross-validation |
| Business intelligence | Present results through six Power BI report pages |

### Selected Verified Outputs

| Output | Result | Context |
|---|---:|---|
| Initial fact-table records | 180,519 | Saved warehouse notebook output |
| Product dimension records | 118 | Saved warehouse notebook output |
| Customers in RFM output | 17,994 | Saved segmentation output |
| K-Means clusters | 5 | Configured segmentation model |
| Exported association rules | 6 | Saved market basket output |
| Prophet holdout MAPE | **7.94%** | 90-day backtest |
| Prophet holdout MAE | **2,944.04** | Sales units |
| Prophet holdout RMSE | **3,582.87** | Sales units |

These figures refer to different pipeline stages and analytical populations. They should not be interpreted as counts from one identical final dataset.

---

## Business Problem

Retail businesses need a connected view of commercial performance, customer behavior, product demand, and delivery operations.

RetailIQ 360 addresses questions such as:

- Which products generate the most sales and profit?
- Which customers contribute the most observed revenue?
- How do customers differ in purchase recency, frequency, and monetary value?
- Which products are commonly purchased together?
- How do actual shipping times compare with scheduled delivery times?
- What sales levels are expected over the next 90 days?
- How reliable are those forecasts on historical holdout data?
- How can these findings be communicated through an interactive reporting interface?

The objective is to build a traceable analytical workflow that supports these questions—not to claim that the analysis has already produced measurable business improvements.

---

## Solution Architecture

```text
DataCo Supply Chain Dataset
             |
             v
Python Ingestion + SQLite Staging
             |
             v
Fact and Dimension Tables
             |
             v
Data Quality Checks + Feature Engineering
             |
             +--------------------------+
             |                          |
             v                          v
Advanced SQL Analytics          Customer and Product Models
             |                  - RFM + K-Means
             |                  - Inactivity classification
             |                  - Association rules
             |                          |
             +-------------+------------+
                           |
                           v
                  Sales Forecasting
                  - Prophet
                  - Holdout backtesting
                  - Rolling cross-validation
                           |
                           v
                SQLite Tables + CSV Exports
                           |
                           v
                   Power BI Reporting
```

The workflow uses SQLite as a shared analytical storage layer, Python for transformation and modeling, and Power BI for reporting.

---

## Technology Stack

| Technology | Role |
|---|---|
| Python | Data preparation, transformation, modeling, and exports |
| Pandas | DataFrame operations, aggregation, joins, and SQL integration |
| NumPy | Numerical calculations and feature creation |
| SQLite | Local analytical database |
| SQL | Business queries, CTEs, joins, and window functions |
| Matplotlib | Exploratory charts and diagnostic plots |
| Scikit-learn | Scaling, clustering, classification, regression experiments, and evaluation |
| Prophet | Time-series forecasting and rolling-origin validation |
| MLxtend | Apriori frequent itemsets and association rules |
| Jupyter Notebook | Interactive development and analysis |
| Power BI | Data modeling, measures, interactive visuals, and report navigation |

---

## Repository Structure

The repository is organized by responsibility:

```text
RetailIQ_360/
│
├── README.md
│
├── Dashboard/
│   └── RetailIQ_360.pbix
│
├── Database/
│   └── RetailIQ 360.db
│
├── Meta_data/
│   ├── copy_all_code.ipynb
│   └── RetailIQ 360.docx
│
├── Modeled_data/
│   ├── backtest_forecast_vs_actual.csv
│   ├── forecast_components.csv
│   ├── forecast_with_intervals.csv
│   ├── quarterly_actuals.csv
│   ├── quarterly_forecast.csv
│   └── rolling_accuracy_metrics.csv
│
├── notebooks/
│   ├── Retail-IQ 360 WareHousing.ipynb
│   ├── feature_engineering.ipynb
│   ├── advance_sql_analytics.ipynb
│   └── machine_learning.ipynb
│
└── Raw_dataset/
    ├── DataCoSupplyChainDataset.csv
    └── DescriptionDataCoSupplyChain.csv
```

The database and raw dataset are local runtime inputs where they are not distributed with the repository.

### Folder Responsibilities

| Folder | Purpose |
|---|---|
| `Dashboard/` | Power BI report file |
| `Database/` | SQLite warehouse and analytical tables |
| `Meta_data/` | Supporting schema notes, project documentation, and code-extraction utility |
| `Modeled_data/` | Forecast outputs, evaluation results, and reporting exports |
| `notebooks/` | Main implementation notebooks |
| `Raw_dataset/` | Source dataset and field descriptions |

### Metadata Files

**`Meta_data/RetailIQ 360.docx`**

Contains supporting information about fact and dimension tables, engineered columns, and analytical outputs.

**`Meta_data/copy_all_code.ipynb`**

Contains a utility that extracts code cells from a notebook into a consolidated text representation. It supports code inspection and documentation; it is not a separate pipeline stage.

Jupyter checkpoint files are development artifacts and are not required to understand or run the main project.

---

## Dataset Overview

The project uses the **DataCo Supply Chain dataset**.

The source data includes:

| Domain | Example Fields |
|---|---|
| Customers | Customer ID, segment, city, state, and country |
| Products | Product ID, product name, category, department, and price |
| Transactions | Order ID, quantity, sales, discounts, item total, and profit |
| Shipping | Shipping mode, delivery status, actual shipping days, and scheduled shipping days |
| Geography | Order city, state, country, and region |
| Time | Order and shipping timestamps |

Field descriptions are provided in:

[`Raw_dataset/DescriptionDataCoSupplyChain.csv`](Raw_dataset/DescriptionDataCoSupplyChain.csv)

### Analytical Scope

The notebooks use different data scopes for different tasks:

- Initial warehouse outputs include 180,519 fact records.
- Some downstream fact-table variants exclude 2018 records.
- Customer modeling uses the fact-table state available at that stage.
- The revised Prophet workflow retains dates through **2017-10-01**, producing 1,005 daily observations before forecasting.

These scope differences matter when reconciling customer counts, transaction counts, revenue totals, and dashboard metrics.

---

## Data Warehouse Design

The warehouse follows a dimensional modeling approach centered on order-item transactions.

### Core Fact Table: `fact_order_items`

**Intended grain:** one source order-item record.

| Column | Description |
|---|---|
| `order_id` | Order identifier; may repeat across items in the same order |
| `customer_id` | Customer identifier |
| `product_id` | Product identifier |
| `sales` | Source sales amount |
| `quantity` | Item quantity |
| `discount` | Source discount amount |
| `profit` | Profit value mapped from the source |
| `item_total` | Source order-item total |
| `profit_ratio` | Source profit ratio |
| `order_date` | Order timestamp |

The notebooks also create enriched fact-table variants containing location attributes, shipping mode, order status, and delivery indicators.

> The source order-item identifier is not retained in the documented core fact schema. Preserving it is a planned improvement for explicit grain validation.

### Dimension Tables

| Table | Main Attributes |
|---|---|
| `dim_customer` | Customer identity, segment, and customer location |
| `dim_product` | Product name, category, department, and price |
| `dim_shipping` | Shipping mode, delivery status, risk flag, and shipping durations |
| `dim_location` | Order geography and location identifier |
| `dim_date` | Date/time attributes, month, quarter, weekday, and weekend indicator |

Customer and product identifiers support business joins. Location identifiers are introduced in enriched fact-table variants.

The current implementation contains exploratory table versions; it should not be interpreted as a fully constrained production star schema.

---

## Data Preparation and Feature Engineering

Implementation:

[`notebooks/feature_engineering.ipynb`](notebooks/feature_engineering.ipynb)

### Data Quality Checks

The notebook inspects:

- Missing values across fact and dimension tables.
- Duplicate records.
- Numeric distributions.
- Statistical outliers in profit, item totals, and discounts.
- Date conversion and calendar attributes.

Missing customer ZIP codes are filled with a placeholder value of `0`. This is a missing-data convention, not a validated postal code.

### Outlier Handling

Profit outliers are identified using the interquartile range:

```text
IQR = Q3 − Q1

Lower bound = Q1 − 1.5 × IQR
Upper bound = Q3 + 1.5 × IQR
```

The workflow creates:

| Feature | Purpose |
|---|---|
| `profit_outlier` | Flag observations outside the IQR bounds |
| `profit_capped` | Store a percentile-capped alternative to original profit |

Keeping the capped value in a separate column preserves the distinction between the source metric and a transformed analytical feature.

### Transaction Features

| Feature | Calculation or Meaning |
|---|---|
| `profit_margin_pct` | `profit / sales × 100` |
| `avg_selling_price` | `sales / quantity` |
| `dicount_pct` | `discount / sales × 100` |
| `order_month` | Month extracted from the order timestamp |
| `quarter` | Calendar quarter |
| `weekday` | Day name |
| `is_weekend` | Saturday/Sunday indicator |

`dicount_pct` retains the spelling used in the current implementation.

### Customer Aggregations

| Python Object | Persisted SQLite Table | Purpose |
|---|---|---|
| `customer_spend` | `customer_total_spend` | Observed sales per customer |
| `customer_orders` | `customer_total_orders` | Distinct orders per customer |

### Shipping Features

```text
Delivery delay = Actual shipping days − Scheduled shipping days
```

- Positive: later than scheduled.
- Zero: matches the schedule.
- Negative: earlier than scheduled.

The engineered shipping column is named `delievery_delay` in the current notebook.

---

## Advanced SQL Analytics

Implementation:

[`notebooks/advance_sql_analytics.ipynb`](notebooks/advance_sql_analytics.ipynb)

| Analytical Output | Purpose | SQL Techniques |
|---|---|---|
| `top_10_Cus_by_sales` | Identify customers with the highest observed sales | Aggregation, sorting, `LIMIT` |
| `profitability_analysis` | Compare product sales, profit, and margins | Grouped calculations |
| `rank_products_desc` | Rank products by sales | `RANK() OVER` |
| `cus_order_frequency` | Measure distinct orders per customer | `COUNT(DISTINCT ...)` |
| `high_value_customers` | Create spend-based customer tiers | `CASE WHEN` |
| `com_daily_sales` | Calculate cumulative sales | Cumulative window aggregation |
| `moving_avg_7d` | Calculate a rolling average | Window frame |
| `pareto_analysis_table` | Measure cumulative product sales contribution | CTEs and window functions |
| `cohort_table` | Identify each customer's first purchase date | `MIN()` |
| `sales_by_region` | Explore geographic sales performance | Joins and aggregation |
| `shipping_performance_new` | Compare delivery timing by shipping mode | Conditional aggregation |

### Customer Value Tiers

Customers are classified by observed cumulative sales:

```text
High Value:   sales ≥ 5,000
Medium Value: sales ≥ 2,000 and < 5,000
Low Value:    sales < 2,000
```

These are descriptive spending tiers, not predictions of future customer lifetime value.

### Cohort Foundation

`cohort_table` identifies first purchase dates. It provides a foundation for cohort analysis, but the current SQL does not calculate a complete retention matrix.

### Time-Series Aggregation Note

The cumulative-sales and moving-average SQL currently groups by `order_date`. If this field contains timestamps, a seven-row moving window is not necessarily seven calendar days.

Daily reporting should normalize timestamps with `DATE(order_date)` before aggregation.

---

## Customer Intelligence and Machine Learning

Implementation:

[`notebooks/machine_learning.ipynb`](notebooks/machine_learning.ipynb)

### 1. RFM Customer Segmentation

Customer behavior is represented using:

| Feature | Definition |
|---|---|
| Recency | Days since the customer's latest purchase |
| Frequency | Number of distinct orders |
| Monetary | Total observed sales |

The reference date is one day after the latest customer purchase date.

The workflow:

1. Aggregates customer transactions using SQL.
2. Calculates recency.
3. Standardizes RFM features with `StandardScaler`.
4. Fits K-Means with `n_clusters=5` and `random_state=42`.
5. Saves the output to `customer_segments`.

The saved output contains **17,994 customer records**.

Cluster numbers are algorithmic labels. Business personas require interpretation of each cluster's RFM profile.

### 2. Customer Inactivity Classification

The notebook defines:

```python
churn = 1 if recency > 90 else 0
```

A Logistic Regression model is then trained using recency, frequency, and monetary value.

Results are exported to `churn_predictions`.

**Important interpretation:** because recency directly defines the target and is also included as an input, the model can learn the labeling rule. The reported perfect classification score is therefore not evidence of future churn prediction.

This component is best understood as an exploratory inactivity-classification exercise. A predictive churn model would require historical feature snapshots and a separate future observation window.

### 3. Market Basket Analysis

The workflow:

- Joins transactions with product names.
- Builds an order-by-product presence matrix.
- Applies Apriori with `min_support=0.01`.
- Generates association rules using a lift threshold of `1`.
- Saves results to `market_basket_rules`.

The saved notebook output contains **six rules**.

These rules support exploration of product bundles and cross-sell opportunities. Association does not establish causation or prove that a recommendation will increase sales.

---

## Sales Forecasting and Evaluation

### Forecasting Objective

Estimate daily sales over a 90-day horizon and evaluate performance against historical observations.

### Prophet Configuration

| Parameter | Configuration |
|---|---|
| Seasonality mode | Multiplicative |
| Yearly seasonality | Enabled |
| Weekly seasonality | Explicit weekly component |
| Monthly seasonality | Period of 30.5 days |
| Daily seasonality | Disabled |
| Changepoint prior scale | `0.15` |
| Seasonality prior scale | `10` |
| Uncertainty interval | Nominal 95% |
| Forecast horizon | 90 days |

### Revised Training Scope

The notebook first experiments with a longer historical series, then retrains after applying:

```python
sales_df_1 = sales_df_1[
    sales_df_1["ds"] <= "2017-10-01"
]
```

The revised series contains **1,005 daily observations**.

The cutoff is an analytical decision made in the notebook. It does not independently prove that all later source records are corrupted.

### 90-Day Holdout Backtest

The final 90 observations are withheld from model fitting.

**Evaluation period:** July 4, 2017–October 1, 2017.

| Metric | Value |
|---|---:|
| MAPE | **7.94%** |
| MAE | **2,944.04** |
| RMSE | **3,582.87** |
| Observations inside exported forecast intervals | **95.56% — 86 of 90** |

These metrics are calculated from:

[`Modeled_data/backtest_forecast_vs_actual.csv`](Modeled_data/backtest_forecast_vs_actual.csv)

MAPE is an error measure; it is not presented as “92.06% forecasting accuracy.”

### Rolling-Origin Cross-Validation

The notebook uses Prophet cross-validation with:

```text
Initial training window: 365 days
Cutoff spacing:          90 days
Forecast horizon:       90 days
```

Selected exported rolling-window results:

| Horizon | MAPE | MAE | RMSE |
|---|---:|---:|---:|
| 30 days | 7.67% | 2,711.61 | 3,737.21 |
| 60 days | 7.15% | 2,510.36 | 3,281.04 |
| 90 days | 7.97% | 2,843.72 | 3,559.45 |

These horizon-level rolling metrics are distinct from the single 90-day holdout result.

### Forecast Exports

| File | Contents |
|---|---|
| `forecast_with_intervals.csv` | Historical actuals, fitted values, future forecasts, and uncertainty bounds |
| `backtest_forecast_vs_actual.csv` | Holdout forecasts, actuals, absolute errors, percentage errors, and signed errors |
| `forecast_components.csv` | Trend, yearly, weekly, and monthly components |
| `rolling_accuracy_metrics.csv` | Horizon-level MAPE, MAE, RMSE, and MSE |
| `quarterly_actuals.csv` | Historical quarterly aggregates from the retained series |
| `quarterly_forecast.csv` | Future-only forecast totals grouped by quarter |

With multiplicative seasonality, seasonal components represent proportional effects relative to the trend, not standalone sales amounts.

### Quarter-Level Interpretation

The exported future forecast totals approximately **3.41 million sales units** for October 2–December 30, 2017.

Although labeled Q4 in the export, this is not a complete calendar-quarter forecast: October 1 is retained as an actual, and December 31 lies outside the 90-day forecast window.

The notebook's reported 8.84% comparison against Q4 2016 should therefore be treated as an exploratory, non-like-for-like comparison—not a validated full-quarter growth estimate.

### Random Forest Experiment

A separate Random Forest regression experiment uses calendar, lag, and shifted rolling features.

Its saved output reports approximately **557.24% MAPE**.

This experiment uses a different data scope from the revised Prophet workflow and is not a controlled model comparison. It is retained as an exploratory attempt rather than presented as a successful forecasting model.

---

## Power BI Dashboard

Report file:

[`Dashboard/RetailIQ_360.pbix`](Dashboard/RetailIQ_360.pbix)

The report contains six pages:

| Report Page | Analytical Focus |
|---|---|
| Executive Overview | Revenue, profit, margin, customers, orders, and sales trends |
| Customer Intelligence | Customer personas, revenue distribution, and inactivity-related exploration |
| Product & Cross-Sell Intelligence | Product sales and association-rule outputs |
| Sales Forecasting — Next 90 Days | Actuals, forecasts, backtesting, forecast summaries, and quarter-level comparisons |
| Operational & Shipping Intelligence — 1 | Delay, cancellation, and delivery-timing indicators by mode and region |
| Operational & Shipping Intelligence — 2 | Shipping summary tables and regional delivery comparisons |

The report connects descriptive analysis with customer and forecasting outputs in one interface.

Shipping timing indicators should be interpreted alongside delivery status. A duration-based “late” flag is not identical to a business delivery-status definition, particularly for canceled records.

---

## How to Explore and Run the Project

### Quick Review Path

For a short review:

1. Open the Power BI report to explore the business-facing output.
2. Review `Retail-IQ 360 WareHousing.ipynb` for ingestion and table construction.
3. Review `advance_sql_analytics.ipynb` for SQL techniques.
4. Review `machine_learning.ipynb` for RFM, forecasting, validation, and market basket analysis.
5. Inspect the CSV exports to verify forecasting results independently.

### Prerequisites

- A Python environment compatible with the project dependencies.
- Jupyter Notebook or JupyterLab.
- Power BI Desktop for opening the `.pbix` report.
- Access to the source dataset.
- A writable location for the SQLite database.

### Install the Main Python Dependencies

```bash
pip install pandas numpy matplotlib scikit-learn prophet mlxtend jupyterlab
```

`sqlite3` is included with Python.

The repository does not currently provide a verified, version-pinned environment. Dependency compatibility may require adjustment.

### Configure Local Paths

The current notebooks contain local file paths and database connections.

Update the source CSV path to your own location. The ingestion notebook reads the CSV using:

```python
encoding="latin1"
```

Use one consistent database location across all notebooks, for example:

```python
from pathlib import Path
import sqlite3

PROJECT_ROOT = Path("/path/to/RetailIQ_360")
DB_PATH = PROJECT_ROOT / "Database" / "RetailIQ 360.db"

conn = sqlite3.connect(DB_PATH)
```

This is a suggested portable configuration; the existing notebooks require path updates.

### Recommended Execution Order

```text
1. Retail-IQ 360 WareHousing.ipynb
2. feature_engineering.ipynb
3. advance_sql_analytics.ipynb
4. machine_learning.ipynb
5. Refresh and inspect RetailIQ_360.pbix
```

The notebooks share SQLite tables, so execution order and a consistent database path matter.

> **Reproducibility note:** these are exploratory notebooks, not a packaged one-command pipeline. Some cells rely on intermediate variables or tables from earlier development states. A fresh run may require resolving those dependencies before executing every cell sequentially.

Several database writes use `if_exists="replace"`. Run against a working copy if you need to preserve an existing database.

### Open the Dashboard

Open `Dashboard/RetailIQ_360.pbix` in Power BI Desktop.

Inspect and update data-source settings before refreshing, since the report may reference the original local database or CSV locations.

---

## Technical Considerations and Limitations

| Area | Current Consideration |
|---|---|
| Notebook state | Some saved outputs and variables reflect different development stages |
| Population consistency | Fact-table variants and date filters produce different analytical populations |
| Keys and relationships | Grain, dimension-key uniqueness, and join cardinality need explicit validation |
| Date dimension | Current construction uses distinct order timestamps rather than a guaranteed continuous daily calendar |
| Naming | Legacy names include `dicount_pct`, `delievery_delay`, and several fact-table variants |
| Forecast preprocessing | Percentile clipping is calculated before holdout splitting; thresholds should be fitted on training data only |
| Forecast validation | Prophet warns that the 365-day initial window is shorter than its 365.25-day yearly period |
| Churn target | Rule-derived target and recency input prevent interpretation as genuine future churn prediction |
| Shipping metrics | Several outputs count source rows, not necessarily distinct shipments or orders |
| Dashboard aggregation | The second shipping page contains count aggregations over pre-aggregated metric fields; these require review before interpreting them as rates or totals |
| Business impact | No live deployment, controlled campaign, or realized financial improvement is claimed |

These limitations define the next engineering and analytical improvements rather than being hidden behind headline metrics.

---

## Future Improvements

### Engineering and Reproducibility

- Replace hard-coded paths with a shared configuration.
- Refactor repeated notebook logic into reusable Python modules.
- Consolidate exploratory fact-table versions into documented canonical tables.
- Preserve source order-item identifiers.
- Add tests for nulls, uniqueness, join cardinality, and aggregate reconciliation.
- Add a version-pinned dependency file.
- Validate the workflow using fresh-kernel, top-to-bottom execution.

### Modeling and Evaluation

- Redesign churn prediction using historical snapshots and future outcomes.
- Compare K-Means configurations using cluster-quality metrics.
- Fit preprocessing exclusively on training windows.
- Add naive and seasonal-naive forecasting baselines.
- Compare models using identical data scopes and forecast protocols.
- Extend cohort foundations into a retention matrix.
- Validate association rules on a separate time period.

### Reporting

- Add dashboard screenshots for browser-based review.
- Reconcile dashboard measures against SQL and exported CSVs.
- Correct aggregation settings for pre-aggregated shipping metrics.
- Align actual and forecast periods for quarter-level comparisons.
- Document metric definitions and exclusion rules.

---

## Skills Demonstrated

| Competency | Evidence |
|---|---|
| Data engineering | CSV ingestion, SQL persistence, and multi-stage transformations |
| Dimensional modeling | Fact and dimension table construction |
| Data preparation | Missing-value checks, duplicate inspection, and outlier features |
| SQL analytics | CTEs, window functions, ranking, joins, and conditional aggregation |
| Feature engineering | Financial, calendar, customer, lag, rolling, and shipping features |
| Customer analytics | RFM aggregation, scaling, and clustering |
| Product analytics | Frequent itemsets and association rules |
| Time-series analysis | Prophet, uncertainty intervals, chronological backtesting, and rolling validation |
| Business intelligence | Multi-page Power BI reporting |
| Analytical judgment | Explicit distinction between verified results, exploratory outputs, and methodological limitations |

---

## Data Attribution and Responsible Use

This project uses the DataCo Supply Chain dataset for portfolio and analytical exploration.

The repository's source-data description file documents the original fields.

Source data can contain customer-related attributes. Review raw data, notebook outputs, database files, and the embedded Power BI model before public distribution. Remove or anonymize unnecessary personal fields.

Dataset redistribution and project-code licensing are separate considerations. Follow the original dataset's usage terms and do not assume that a code license automatically covers the data.

---

**RetailIQ 360 demonstrates a connected workflow from transactional data to analytical tables, customer intelligence, forecast evaluation, and business reporting—with transparent documentation of what is implemented and what still needs improvement.**
