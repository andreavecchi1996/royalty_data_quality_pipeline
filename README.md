# Multi-DSP Royalty ETL & Consolidation Pipeline

## Project Overview

In the music industry, Royalty agencies receive monthly royalty statements from DSPs with inconsistent schemas, currencies, and metadata gaps. This pipeline ingests raw reports from 5 DSPs (Q1 2024 data), standardises them into a unified fact table with USD revenue, and prepares production-ready per-label exports.

### The Challenge

- **Inconsistent Schemas:** Different CSV structures, column names, and date formats across DSPs
- **Multi-Currency Revenue:** USD, EUR, GBP, JPY requiring historical FX conversion
- **Scale:** 15 reports to **2.25M rows**, **30k unique labels**

### The Solution

<img width="680" height="436" alt="Image" src="https://github.com/user-attachments/assets/193030fd-5e1b-4a5b-b39c-5b9edd867fd5" />

1. **Raw CSV Ingestion:** Amazon Music, Apple Music, Deezer, Spotify, YouTube Content ID (15 files)
2. **Data Cleaning:** Deduplication, type casting, null handling, DSP-specific transformations
3. **Schema Standardisation:** Unified columns (`artist`, `label`, `isrc`, `net_revenue_usd`, etc.)
4. **FX Normalisation:** **Historical rates** (Frankfurter API) → all revenue in USD
5. **Production Exports:** Single **fact table**

### Fact Table Schema

| Column           | Type    | Description                            |
| ---------------- | ------- | -------------------------------------- |
| artist           | str     | Main performing artist                 |
| label            | str     | Record label name                      |
| track            | str     | Track title                            |
| isrc             | str     | ISRC identifier                        |
| album            | str     | Album/release title                    |
| upc              | int64   | UPC/EAN release identifier             |
| country          | str     | ISO country code                       |
| configuration    | str     | Tier/format (Free, Premium, Unlimited) |
| units            | int64   | Streams/plays/views                    |
| sales_start_date | str     | Reporting period start                 |
| sales_end_date   | str     | Reporting period end                   |
| channel          | str     | DSP source                             |
| net_revenue_usd  | float64 | Net revenue (USD post-FX)              |
| stream_rate_usd  | float64 | Revenue per unit (USD)                 |
| report_month     | str     | Monthly reporting period (YYYY-MM)     |

### Tech Stack

- **Data Sources:** Amazon Music, Apple Music, Deezer, Spotify, **YouTube Content ID**
- **ETL & Analysis:** Python/pandas
- **FX API:** Frankfurter (historical rates)
- **Environment:** Jupyter Notebook, VS Code
- **Version Control:** Git/GitHub

## Notebook
[`royalty_data_quality_pipeline.ipynb`](./royalty_data_quality_pipeline.ipynb)

## Dataset Note
Synthetic dataset modelled after digital rights agency royalty workflows (Amazon Music, Spotify, YouTube, ...). Final dataset (royalties_fact_clean_2024_q1.csv) excluded per GitHub limits; DSPs CSV available in folder `inbound_reports`.

# Note: Synthetic dataset for demonstration. Does not reflect real royalty data.



