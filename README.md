# Loan Default & Risk Analysis — Power BI Dashboard

An interactive Power BI report analyzing loan applicant data to surface default risk patterns across employment type, age group, credit score, and income bracket — built end-to-end from SQL Server ingestion through a scheduled Power BI Service refresh.

📄 **[View the full report (PDF export)](./loan_default_project.pdf)**

## Project Overview

This project analyzes a loan portfolio dataset to answer questions like:
- Which employment types and age groups carry the highest default risk?
- How does loan amount vary by purpose, credit score, and marital status?
- How has the default rate trended year-over-year (2013–2018)?
- Where is loan volume concentrated by income bracket and employment type?

## Tech Stack

- **SQL Server** — data storage and initial import
- **Power BI Dataflows** — data staging with scheduled + incremental refresh
- **Power BI Desktop** — data modeling, DAX measures, report design
- **Power BI Service** — published report with scheduled refresh
- **On-premises Data Gateway** — configured to connect the Service to local SQL Server

## Pipeline

1. Loan data imported into **Microsoft SQL Server**
2. Data staged via a **Power BI Dataflow**, connected through a **Standard Mode Gateway**
3. Dataflow loaded into **Power BI Desktop**, with data types and profiling done in Power Query
4. DAX measures and visuals built out (see below)
5. Report published to **Power BI Service** with **scheduled refresh** on the dataflow

## Dashboard Pages

### 1. Loan Default & Overview
- Loan Amount by Purpose (Home, Business, Education, Auto, Other)
- Average Income by Employment Type
- Default Rate by Employment Type
- Average Loan Amount by Age Group
- Default Rate by Year (2013–2018)

### 2. Applicant Demographics & Financial Profile
- Median Loan Amount by Credit Score bucket
- Average Loan Amount (High Credit) by Age Group & Marital Status
- Total Loan by Credit Score Bins, split by Mortgage/Dependents status
- Loans by Education Type

### 3. Financial Risk Metrics
- YoY Loan Amount Change (%)
- YoY Default Loans Change (%)
- YTD Loan Amount by Credit Score Bins & Marital Status
- Decomposition Tree: Loan Amount by Income Bracket → Employment Type

## Key Insights

- **Unemployed applicants have the highest default rate (~3.4%)**, notably above full-time (3.0%) and self-employed (2.9%) borrowers.
- Default rate has stayed fairly stable year-over-year (~11.5–11.75%), with **2015 marking a slight peak** before a gradual decline.
- **High-income applicants account for the majority of loan volume** (₹32.58bn of the total), roughly 3x the medium-income segment.
- Average loan amount is fairly consistent across age groups and marital status, suggesting loan sizing is driven more by credit/income factors than demographics alone.

## DAX Highlights

Some of the DAX patterns used across the report:
- `CALCULATE`, `ALLEXCEPT`, `FILTER`, `COUNTROWS`, `DIVIDE` — for default rate calculations segmented by category
- `SUMX`, `NOT`, `ISBLANK` — for purpose-based loan amount aggregation
- `AVERAGEX`, `VALUES` — for average loan by age group
- `MEDIANX` — for median loan amount by credit score category
- `SWITCH` — powering the decomposition tree

## Dataset

The full dataset used for this project is available here: 
[Loan Default Dataset (Google Drive)](https://drive.google.com/file/d/1LxdlX7Yh6IrifvobCMpdk9i0jH-raSqF/view?usp=sharing)

## Files in this Repo

| File | Description |
|---|---|
| `loan_default_project.pdf` | Full exported report (all 3 pages) |
| `loan_default_project.pbix` | Power BI source file |
