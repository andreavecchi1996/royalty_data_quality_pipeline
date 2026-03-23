# Multi-DSP Royalty Data Quality & Reconciliation Pipeline
## Project Overview & Business Value
In the digital music ecosystem, Rights Agencies and Distributors manage a complex flow of revenue from dozens of Digital Service Providers (DSPs) to thousands of rights holders. A critical operational bottleneck is the monthly processing of royalty statements, which lack standardisation and frequently contain data integrity issues.

This project is a data pipeline designed to automate the ingestion, validation, and consolidation of these disparate royalty reports, ensuring accurate revenue allocation and reducing manual overhead.


### The Challenge
Managing royalty data from multiple DSPs (Spotify, Apple, YouTube, Amazon, Deezer) is operationally complex:

- Inconsistent Formats: Every DSP uses different CSV schemas, column names, and currencies.

- Data Errors: Raw reports often contain missing ISRCs, Artist, Label, Track names,  invalid country codes, or negative values that block payment systems.

- Manual Overload: Validating millions of rows by hand is slow and error-prone.


### The Solution
An automated pipeline to standardise and validate royalty data:

- Unified Ingestion: Scripts to parse and normalise diverse DSP formats into one standard schema.

- Automated QA: Instant checks for data integrity (e.g., missing metadata, currency mismatches).

- Clean Output: Produces consolidated, error-free datasets ready for royalty accounting systems (e.g., Labelcaster).

- Error Logging: Automatically separates and flags problematic rows for quick investigation.


# Note: This project is currently in development.

## Tech Stack

- Data Sources: Amazon, Apple, Deezer, Spotify, YouTube (15 CSV reports)
- Data warehouse: Google BigQuery (schema design)
- ETL: Python
- Environment: Jupyter Notebook
- Version control: Git & GitHub

## Data Structure & Initial Checks
<img width="558" height="367" alt="Image" src="https://github.com/user-attachments/assets/3230b53d-3d2b-4fe6-9e2e-19170cc30ff9" />

## Executive Summary
### Overview of Findings



## The dataset
