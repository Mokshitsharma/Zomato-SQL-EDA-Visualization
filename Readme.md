# 🍽️ Zomato Restaurant Intelligence — SQL EDA + Python Visualization

> A dual-layer exploratory data analysis project combining **SQL-first querying** (SQLite with Joins, CTEs, and Window Functions) with **Python visualization** (Pandas + Seaborn + Matplotlib) to surface actionable restaurant intelligence from Zomato's global dataset across 15 countries and 140+ cities.

[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python)](https://python.org)
[![SQL](https://img.shields.io/badge/SQL-SQLite-003B57?style=for-the-badge&logo=sqlite)](https://sqlite.org)
[![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-F37626?style=for-the-badge&logo=jupyter)](https://jupyter.org)
[![Dataset](https://img.shields.io/badge/Dataset-9551%20Restaurants-green?style=for-the-badge)](https://www.kaggle.com/datasets/shrutimehta/zomato-restaurants-data)

---

## 1. 🎯 Project Name

**Zomato Restaurant Intelligence — SQL EDA + Python Visualization**  
*City-wise trends · Cuisine analysis · Rating patterns · Online delivery impact · Cost benchmarking*

---

## 2. 🔍 Problem Statement

Zomato operates across 15 countries with 9,500+ listed restaurants — but raw listing data alone doesn't tell business stakeholders what they need to know:

- Which cities and countries have the **highest restaurant density** and what does average cost look like per region?
- Does offering **online delivery** measurably improve customer ratings, or is it a neutral feature?
- Does **table booking availability** correlate with higher aggregate ratings?
- Which **cuisines dominate** by city, and which command premium pricing?
- How do restaurants **rank within their own city** on rating and cost — not just globally?

Restaurant chains, food-tech investors, and market analysts need these cross-dimensional answers quickly — and a simple filter in Excel isn't sufficient for multi-table, ranked, segmented analysis.

---

## 3. 💡 My Solution

Built a **two-layer analysis pipeline**:

**Layer 1 — SQL Analysis (SQLite + `zomato.db`):**
Ingested the full `zomato.csv` into a SQLite database and wrote structured queries using:
- **JOINs** — linking restaurant data with country/city dimension tables
- **CTEs (Common Table Expressions)** — breaking complex multi-step analyses into readable, named subqueries
- **Window Functions** — `RANK() OVER(PARTITION BY city ORDER BY aggregate_rating DESC)` for city-level restaurant rankings, `AVG() OVER(PARTITION BY country_code)` for rolling country benchmarks
- Aggregations across `Average Cost for two`, `Aggregate rating`, `Votes`, `Has Online delivery`, `Has Table booking`

**Layer 2 — Python Visualization (Jupyter Notebook):**
Query results piped into Pandas DataFrames and visualized with Seaborn + Matplotlib:
- **Top cities by restaurant count** — horizontal bar charts
- **Country-wise average cost** — cross-currency cost benchmarks (`country_cost.png`)
- **Online delivery vs rating distribution** — box/violin plots (`online_delivery_rating.png`)
- **Table booking impact on ratings** — grouped comparisons
- **Cuisine-wise distribution** — frequency analysis

---

## 4. 📐 System Architecture

```
┌──────────────────────────────────────────────────┐
│              DATA LAYER                           │
│  zomato.csv (2.15 MB, ~9,551 restaurants)        │
│      │                                           │
│      ▼                                           │
│  SQLite (zomato.db)                              │
│  pandas.read_csv() → df.to_sql("restaurants")   │
└──────────────┬───────────────────────────────────┘
               │
┌──────────────▼───────────────────────────────────┐
│              SQL ANALYSIS LAYER                   │
│  sqlite3 / sqlalchemy connection                  │
│                                                   │
│  Queries using:                                   │
│  ├── JOINs (restaurant × country dimensions)     │
│  ├── CTEs (multi-step analysis pipelines)        │
│  ├── Window Functions (RANK, AVG OVER PARTITION) │
│  ├── GROUP BY aggregations                       │
│  └── CASE WHEN for feature segmentation          │
└──────────────┬───────────────────────────────────┘
               │  pd.read_sql(query, conn)
┌──────────────▼───────────────────────────────────┐
│           PYTHON VISUALIZATION LAYER              │
│  Pandas DataFrames ← SQL query results           │
│                                                   │
│  Seaborn + Matplotlib charts:                    │
│  ├── Top Cities (barplot)                        │
│  ├── Country Cost Benchmark (country_cost.png)   │
│  ├── Online Delivery vs Rating (violin/box)      │
│  │   (online_delivery_rating.png)                │
│  ├── Table Booking vs Rating (grouped bar)       │
│  └── Cuisine distribution                        │
└──────────────────────────────────────────────────┘
```

---

## 5. 🛠️ Skills Used

| Category | Technologies |
|---|---|
| **SQL** | SQLite, Joins (INNER/LEFT), CTEs (`WITH` clauses), Window Functions (`RANK()`, `AVG() OVER`, `PARTITION BY`), GROUP BY, HAVING, ORDER BY, CASE WHEN |
| **Python** | Python 3.8+, Jupyter Notebook |
| **Data Analysis** | Pandas (DataFrames, `read_sql`, `read_csv`, `to_sql`, aggregations) |
| **Visualization** | Seaborn (barplot, boxplot, violinplot, heatmap), Matplotlib (figure sizing, subplots, annotations) |
| **Database** | SQLite3 (file-based RDBMS), `zomato.db` persistence |
| **EDA Methodology** | Univariate analysis, bivariate comparisons, segmented group analysis, distribution analysis |
| **Domain Knowledge** | Food-tech industry metrics, delivery platform analysis, restaurant rating systems |

---

## 6. 📊 Project Metrics

| Metric | Value |
|---|---|
| **Dataset Size** | ~9,551 restaurants |
| **Countries Covered** | 15 countries |
| **Cities Covered** | 140+ cities |
| **Dataset File Size** | 2.15 MB (`zomato.csv`) |
| **Notebook Size** | 1,099 lines, 132 KB |
| **SQL Techniques Used** | JOINs, CTEs, Window Functions, GROUP BY, HAVING, CASE WHEN |
| **Visualizations Produced** | 5+ charts (city counts, country costs, delivery impact, rating distributions, cuisine analysis) |
| **Output Charts Committed** | `country_cost.png`, `online_delivery_rating.png` |
| **Database** | `zomato.db` (SQLite, committed to repo) |
| **Analysis Dimensions** | City, Country, Cuisine, Online Delivery, Table Booking, Rating, Cost, Votes |

---

## 7. 📦 Dataset Details

| Property | Detail |
|---|---|
| **Source** | [Kaggle — Zomato Restaurants Data](https://www.kaggle.com/datasets/shrutimehta/zomato-restaurants-data) |
| **File** | `zomato.csv` (2.15 MB, committed to repo) |
| **Rows** | ~9,551 restaurant listings |
| **Countries** | 15 (India, USA, UK, UAE, Australia, South Africa, Philippines, New Zealand, Singapore, Canada, Indonesia, Qatar, Sri Lanka, Brazil, Turkey) |
| **Key Columns** | Restaurant ID, Name, Country Code, City, Address, Locality, Cuisines, Average Cost for Two, Currency, Has Table Booking (Yes/No), Has Online Delivery (Yes/No), Is Delivering Now, Price Range (1–4), Aggregate Rating (0–5), Rating Color, Rating Text, Votes |
| **Target Metrics** | Aggregate Rating, Average Cost for Two, Votes |
| **Notable Quirks** | Multi-currency cost data (requires normalization for cross-country comparison), multi-value `Cuisines` column (comma-separated, requires parsing for cuisine-level analysis) |

---

## 8. 📁 Folder Structure

```
Zomato-SQL-EDA-Visualization/
│
├── main.ipynb                   # Full analysis notebook (1,099 lines, 132 KB)
│                                #  ├── Data ingestion (CSV → SQLite)
│                                #  ├── SQL queries (Joins, CTEs, Window Functions)
│                                #  ├── Pandas DataFrames from SQL results
│                                #  └── Seaborn + Matplotlib visualizations
│
├── zomato.csv                   # Raw dataset (2.15 MB, ~9,551 restaurants)
├── zomato.db                    # SQLite database (built from CSV)
│
├── country_cost.png             # Country-wise average cost visualization
├── online_delivery_rating.png   # Online delivery vs rating comparison chart
│
└── Readme.md                    # Project overview
```

---

## 9. ⚙️ Why This Tech Stack?

| Choice | Reason |
|---|---|
| **SQLite** | Lightweight, zero-config relational database — perfect for single-file EDA; enables real SQL syntax (including Window Functions) on a CSV dataset without needing PostgreSQL/MySQL server setup |
| **CTEs** | Named subqueries make complex multi-step analysis readable and maintainable — mirrors how real data teams write production SQL in BigQuery/Snowflake |
| **Window Functions** | `RANK() OVER(PARTITION BY)` enables per-city restaurant ranking that GROUP BY cannot express — directly maps to how business intelligence tools compute leaderboards |
| **Pandas `read_sql()`** | Bridges SQL query results into DataFrames — the standard pattern for SQL-first → Python-viz workflows in data analytics roles |
| **Seaborn** | High-level statistical visualization library built on Matplotlib — produces publication-quality charts with minimal boilerplate; ideal for distribution comparisons (delivery vs no-delivery) |
| **Jupyter Notebook** | Narrative-style analysis combining SQL queries, Python code, and embedded visualizations — the industry standard format for EDA deliverables |

---

## 10. 📌 Key Analytical Questions Answered

| Business Question | SQL Technique Used |
|---|---|
| Which cities have the most restaurants on Zomato? | `GROUP BY city ORDER BY COUNT(*) DESC` |
| What is the average cost for two by country? | `GROUP BY country_code, AVG(average_cost_for_two)` |
| Do restaurants with online delivery get higher ratings? | `GROUP BY has_online_delivery, AVG(aggregate_rating)` |
| Do table booking restaurants rate higher? | `GROUP BY has_table_booking, AVG(aggregate_rating)` |
| Which restaurant ranks #1 in each city by rating? | `RANK() OVER (PARTITION BY city ORDER BY aggregate_rating DESC)` |
| What are the most common cuisines per city? | CTE + `GROUP BY city, cuisines ORDER BY COUNT(*) DESC` |
| Which price range (1–4) has the highest avg rating? | `GROUP BY price_range, AVG(aggregate_rating)` |
| Top 10 most-voted restaurants globally? | `ORDER BY votes DESC LIMIT 10` |

---

## 11. 🚀 Future Improvements

- **Currency normalization** — Convert all `Average Cost for Two` values to USD for true cross-country cost comparison using exchange rate lookup
- **Cuisine explosion** — Parse the multi-value `Cuisines` column (comma-separated) into individual rows for proper cuisine-level analysis and ranking
- **Interactive dashboard** — Port key charts to Plotly/Dash or Power BI for drill-down city and country filtering
- **Geospatial visualization** — Use latitude/longitude columns with Folium or Plotly to plot restaurant density heatmaps on a world map
- **Rating sentiment analysis** — Correlate `Rating Text` (Excellent/Very Good/Good/Average/Poor) with vote counts and delivery availability
- **Time-series simulation** — Model how rating changes with vote accumulation using window functions on binned vote ranges
- **Streamlit app** — Build a restaurant discovery tool: input a city, get top-rated cuisines, avg cost, delivery availability stats

---

## ▶️ Run the Project

### Prerequisites
```bash
pip install pandas numpy seaborn matplotlib jupyter
# sqlite3 is included in Python standard library
```

### Launch the Notebook
```bash
jupyter notebook main.ipynb
```

The notebook will:
1. Load `zomato.csv` into a Pandas DataFrame
2. Persist it to `zomato.db` via `df.to_sql()`
3. Run SQL queries via `pd.read_sql()`
4. Generate and display all visualizations inline

---

## 📬 Contact

**Mokshit Sharma** — AI & Data Science Engineer  
📧 sharman48520@gmail.com  
🌐 [mokshitsharma27.vercel.app](https://mokshitsharma27.vercel.app)

---

*Built with Python, SQLite, Pandas, Seaborn & Matplotlib · Zomato Kaggle Dataset*
