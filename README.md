# Multi-DSP Royalty ETL & Consolidation Pipeline

## Project Overview

In the music industry, Rights Agencies and Distributors receive monthly royalty statements 
from dozens of DSPs, each with its own CSV schema, column naming conventions, and currency. 
Reconciling these reports manually is slow, error-prone, and doesn't scale. This pipeline 
was built to solve that: it ingests raw reports from 5 DSPs across Q1 2024, cleans and 
enriches the data against a BigQuery master reference table, standardises revenue into USD 
via historical FX rates, and outputs a unified fact table ready for royalty accounting and 
per-label distribution.

### The Challenge

- **Inconsistent Schemas:** Every DSP delivers different CSV structures, column names, and date formats.
- **Missing Metadata:** Raw reports frequently contain nulls across critical fields: ISRC, Artist, Label, Track Title, that block downstream payment systems.
- **Multi-Currency Revenue:** Reports arrive in USD, EUR, GBP, and JPY, requiring accurate historical FX conversion before any aggregation.

### The Solution

<img width="680" height="436" alt="Image" src="https://github.com/user-attachments/assets/9148d270-329c-41f2-b9f2-6e380ac7c183" />

- **Structured Ingestion:** 15 raw CSV reports (5 DSPs × 3 months) loaded and inspected for null counts and schema issues before any transformation.
- **Data Enrichment via BigQuery:** Missing fields recovered by joining against `dim_track`, a master reference table, using ISRC or UPC as the lookup key.
- **Per-DSP Cleaning:** Deduplication, type casting, whitespace stripping, DSP-specific column drops, and date normalisation applied to each dataframe.
- **Schema Standardisation:** All DSP column names mapped to a unified schema (`artist`, `label`, `track`, `isrc`, `album`, `upc`, `country`, `units`, `net_royalty_revenue`, `channel`…).
- **Currency Normalisation:** Historical FX rates fetched from the Frankfurter API per reporting period, converting all revenue to USD.
- **Royalty Reporting Fields:** `report_month`, `stream_rate_usd`, `agency_commission_usd` (12%), `label_revenue_usd` (88% post-commission).
- **Flexible Export:** Fact table exportable as a single CSV or split into per-label files.

### Fact Table Schema

| Column | Description |
|---|---|
| `artist` | Main performing artist |
| `label` | Record label name |
| `track` | Track title |
| `isrc` | ISRC code |
| `album` | Album or release title |
| `upc` | UPC/EAN for the release |
| `country` | ISO country code of the sale |
| `configuration` | Format/type (Free, Premium, etc.) |
| `units` | number of Streams / plays / views |
| `net_revenue_usd` | Revenue converted to USD |
| `report_month` | Reporting period (monthly) |
| `stream_rate_usd` | Revenue per unit |
| `agency_commission_usd` | 12% agency fee |
| `label_revenue_usd` | 88% net to label |
| `channel` | Source DSP |
| `sales_start_date` / `sales_end_date` | Reporting window |

## Tech Stack

## Tech Stack
- **Data Sources:** Amazon Music, Apple Music, Deezer, Spotify, YouTube (15 CSV reports, Q1 2024)
- **Data Warehouse:** Google BigQuery (`dim_track` master reference table)
- **ETL:** Python (pandas, numpy, requests)
- **FX Conversion:** Frankfurter API (historical rates)
- **Environment:** Jupyter Notebook
- **Version Control:** Git & GitHub

## Notebook
[`royalty_data_quality_pipeline.ipynb`](./royalty_data_quality_pipeline.ipynb)

## The dataset
The dataset used in this project is synthetic and was generated for personal project 
purposes only. Any resemblance to real label names is coincidental. All revenue figures, 
stream counts, and metadata are fabricated and do not reflect actual royalty data.

