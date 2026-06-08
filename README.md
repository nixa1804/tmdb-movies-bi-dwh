# Movie Industry Analytics & Business Intelligence System

This project presents an end-to-end Data Warehouse (DWH) and Business Intelligence (BI) solution developed to analyze trends, profitability, and overall performance within the movie industry. The project covers the entire data lifecycle: from raw data ingestion and transformation to advanced analytics and interactive visualization.

## Technologies & Tools
- **Database:** PostgreSQL (pgAdmin)
- **ETL Tool:** Apache Hop (Hop Orchestration Platform)
- **Business Intelligence & Visualization:** Microsoft Power BI Desktop (DAX)
- **Data Source:** TMDb Movies Dataset (Kaggle) – featuring over 10,000 movie records

## Architecture & Data Warehousing
The data warehouse is implemented within a PostgreSQL database and organized into two separate schemas to ensure data integrity and separation of concerns:
1. `staging` – Temporary storage used for data ingestion, initial cleaning, and deduplication.
2. `dwh` – The core dimensional model designed using the **Star Schema** principle.

### Data Model (Star Schema):
- **Fact Table:** `fact_performance` (stores metrics such as budget, revenue, profit, ROI, popularity, vote average, and runtime).
- **Dimension Tables:**
  - `dim_movie` (movie details and director information)
  - `dim_genre` (genre names and broader genre groups)
  - `dim_production` (production company names and company size categorization)
  - `dim_time` (detailed time attributes including day, month, quarter, year, and decade)

## ETL Process (Apache Hop)
The ETL workflow is fully automated and modularized into 6 sequential pipelines within Apache Hop:
1. `01_load_staging` – Ingests the raw CSV dataset, performs data type conversions, handles missing values, and removes duplicates.
2. `02_dim_time` – Generates the time dimension based on unique release dates.
3. `03_dim_genre`, `04_dim_production`, `05_dim_movie` – Populates the respective dimension tables and generates surrogate keys.
4. `06_fact_performance` – Performs database lookups to map business keys to surrogate keys, resolves null values, and calculates derived financial metrics (Profit and ROI) using calculator steps.

## Power BI Dashboards
The solution features **6 main interactive reports and a dedicated drill-through page**, seamlessly connected via a central navigation dashboard:
1. **Industry Overview** – High-level statistics and core business KPIs.
2. **Genre Analysis** – Distribution, volume, and performance across different movie genres.
3. **Profitability & ROI** – Deep dive into financial success, budgeting strategies, and returns.
4. **Top Production Companies** – Ranking and benchmarking of studios based on volume and financial performance.
5. **Trends Over Time** – Historical cinematic analysis across decades and years utilizing time hierarchies (drill-down functionality).
6. **Detailed Movie Insights** – A granular tabular view equipped with drill-through capabilities for individual movie analysis.
7. **Movie Details (Drill-through Page)** – A granular dashboard specifically designed as a drill-through destination from other reports. It allows users to right-click any movie across the solution to access deep-dive performance metrics, financial breakdowns, and specific metadata for that individual title.

*Note: Advanced DAX measures were implemented to calculate running totals, cumulative growth, percentage shares, and dynamic filtering.*

## How to Run the Project
1. Run the SQL scripts to set up the schemas and tables in your PostgreSQL database.
2. Open Apache Hop and execute the ETL pipelines (found in the `/etl` directory) to populate the data warehouse.
3. Open the Power BI file (`.pbix` in the `/power-bi` directory) and refresh the data (you will need to update the data source settings to point to your local PostgreSQL instance).
