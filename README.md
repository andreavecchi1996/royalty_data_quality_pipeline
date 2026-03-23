# Multi-DSP Royalty ETL & Consolidation Pipeline

## Project Overview

In the music industry, Rights Agencies like Merlin receive monthly royalty statements from DSPs with inconsistent schemas, currencies, and metadata gaps. This pipeline ingests raw reports from 5 DSPs (Q1 2024 data), standardises them into a unified fact table with USD revenue, and prepares production-ready per-label exports.

### The Challenge

- **Inconsistent Schemas:** Different CSV structures, column names, date formats across DSPs
- **Multi-Currency Revenue:** USD, EUR, GBP, JPY requiring historical FX conversion
- **Scale:** 15 reports to **2.25M rows**, **30k unique labels**

### The Solution

<img width="680" height="436" alt="Image" src="https://github.com/user-attachments/assets/193030fd-5e1b-4a5b-b39c-5b9edd867fd5" />

1. **Raw CSV Ingestion:** Amazon Music, Apple Music, Deezer, Spotify, YouTube Content ID (15 files)
2. **Data Cleaning:** Deduplication, type casting, null handling, DSP-specific transformations
3. **Schema Standardisation:** Unified columns (`artist`, `label`, `isrc`, `net_revenue_usd`, etc.)
4. **FX Normalisation:** **Historical rates** (Frankfurter API) → all revenue in USD
5. **Production Exports:** Single **2.25M-row fact table** OR **30k per-label CSVs**

### Fact Table Schema

| Column | Description |
|--------|-------------|
| `artist` | Main artist |
| `label` | Record label |
| `track` | Track title |
| `isrc` | ISRC identifier |
| `country` | ISO country code |
| `net_revenue_usd` | **Revenue (USD post-FX)** |
| `stream_rate_usd` | Revenue per unit |
| `units` | Streams/views |
| `channel` | DSP source |

### Tech Stack

- **Data Sources:** Amazon Music, Apple Music, Deezer, Spotify, **YouTube Content ID**
- **ETL & Analysis:** Python/pandas (2.25M rows processing)
- **FX API:** Frankfurter (historical rates)
- **Environment:** Jupyter Notebook, VS Code
- **Version Control:** Git/GitHub

## Notebook
[`royalty_data_quality_pipeline.ipynb`](./notebooks/royalty_data_quality_pipeline.ipynb)

## Dataset Note
**Synthetic dataset** simulating Merlin-scale royalty reports. Full fact table (~500MB) excluded from repo per GitHub limits; **sample available** in `data/`.


