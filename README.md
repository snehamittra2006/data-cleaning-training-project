# E-Commerce Sales Data Cleaning & Analysis

A beginner data-analyst project focused on cleaning a messy, real-world-style e-commerce order dataset and generating business insights from it — done as part of the **"Make Data Intelligent" Masterclass**, using AI (Claude) as a data-cleaning and analysis assistant.

## Project Overview

The raw dataset simulates order-level sales data from an online retail company operating across multiple Indian cities. It arrived with the kinds of quality issues you'd expect from real operational data — inconsistent text casing, mixed currency formats, invalid dates, and missing values — and the goal was to clean it into an analysis-ready format and answer specific business questions using it.

**Workflow:** understand the data → audit it for quality issues → clean it → engineer new features → analyze and answer business questions.

## Dataset

| | |
|---|---|
| **Rows** | 2,000 orders |
| **Source sheet** | `Raw_Data` |
| **Time period** | 2026 |
| **Geography** | 7 Indian cities (Delhi, Mumbai, Bangalore, Chennai, Kolkata, Hyderabad, Pune) |
| **Unique customers** | 416 |

### Columns

| Column | Type | Description |
|---|---|---|
| `Order_ID` | Identifier | Unique order number |
| `Order_Date` | Date | Date the order was placed |
| `Customer_ID` | Identifier | Unique customer code |
| `Product` | Categorical | Item purchased |
| `Category` | Categorical | Product category (Electronics, Furniture, Apparel, Home, Beauty) |
| `Region` | Categorical | City where the order was placed |
| `Quantity` | Numerical | Units purchased |
| `Revenue` | Numerical | Order revenue |
| `Profit` | Numerical | Profit earned on the order |

Engineered during cleaning:

| Column | Description |
|---|---|
| `Month` / `Year` | Extracted from `Order_Date` for trend analysis |
| `Customer_Segment` | `New Customer` (1 order) vs. `Repeat Customer` (2+ orders) |
| `Order_Value_Category` | Order bucketed as Low / Medium / High value |

## Data Quality Issues Found & Fixed

An audit of the raw data surfaced the following problems:

- **Inconsistent category & region casing** — e.g. `Electronics` / `electronics` / `ELECTRONICS` all present as separate values (same for all 5 categories and all 7 regions). Standardized to a single consistent format.
- **Mixed currency formatting in Revenue** — values stored inconsistently as plain numbers, `₹50000`, and `374814 INR`. Stripped symbols/text and converted to a uniform numeric type.
- **Inconsistent date formats** — a mix of proper date objects and text strings (`DD-MM-YYYY`), including at least one invalid calendar date (`31-02-2026`). Standardized to a single date format and corrected/flagged invalid entries.
- **Missing values** — gaps across `Customer_ID`, `Product`, `Region`, `Quantity`, `Revenue`, and `Profit` (roughly 1–1.5% of rows per column). Reviewed and handled case-by-case rather than blanket-deleted.
- **Negative quantities** — several dozen orders with quantities below zero, which isn't physically valid for a sales record. Investigated and corrected.
- **Negative profit** — a number of orders showing a loss, flagged for review rather than treated as an error, since loss-making orders are a legitimate business signal.
- **Duplicate order records** — a small set of fully duplicated rows (same order, same values). Removed.

## Analysis & Business Questions

Using the cleaned dataset, the analysis was organized around four themes, each with specific, measurable business questions (e.g. best/worst performing products, month-over-month sales trends, high-value repeat customers, regional performance gaps):

1. **Sales** — overall and time-based trends (monthly/yearly revenue and profit movement)
2. **Product** — top and bottom performing products/categories by revenue and profit
3. **Customer** — new vs. repeat customer behavior, high-value customer identification
4. **Region** — city-level performance comparison and expansion/risk signals

## Tools & Approach

- **Cleaning:** Google Sheets, with formula-driven logic (e.g. `COUNTIF`-based logic for the `Customer_Segment` classification)
- **AI assistance:** Claude was used as a structured analyst copilot — first to explain the dataset's structure, then to audit it for specific quality issues (without altering the data), then to help generate the business-question framework used for analysis
- **Principle followed throughout:** no changes were made to the data without first reviewing AI-flagged issues — cleaning decisions stayed human-reviewed rather than automated end-to-end

## Files

- `Raw_Data` — original, uncleaned dataset
- `Cleaned_Data` *(if included)* — cleaned dataset with engineered columns
- `Prompts` — the AI prompts used at each stage of the workflow (structure understanding, quality audit, formula generation, business-question generation)

## Key Takeaways

This project is as much about the **cleaning process** as the end insights — the biggest risks in the raw data (case-inconsistent categories, mixed currency text in a numeric field, and invalid dates) are exactly the kind of silent errors that would have skewed any analysis run directly on the raw file.
