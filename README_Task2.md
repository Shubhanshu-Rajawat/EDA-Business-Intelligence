# Task 2: Exploratory Data Analysis & Business Intelligence

Internship: ApexPlanet Data Analytics
Input: `ApexPlanet_Cleaned_Dataset.xlsx` (output of Task 1)

## Purpose

This task builds on the cleaned sales dataset from Task 1. The goal was to move past data preparation and start extracting patterns, trends, and relationships from the data, while building SQL proficiency and putting together a first pass at a metrics dashboard.

## Dataset

1,000 sales records, 16 columns after Task 1's cleaning and feature engineering (includes `Order_Month`, `Order_Year`, `Age_Group`, and a `Name_Mismatch_Flag` carried over from the earlier data quality review).

## 1. Descriptive Statistics & Univariate Analysis

Summary statistics were generated for the four numerical fields (Age, Quantity, Unit_Price, Total_Sales) and frequency counts for the categorical fields (Gender, City, Product, Category).

Notable points:
- Total_Sales has a mean of ₹1,39,399 against a median of ₹1,08,594 — the distribution is right-skewed, meaning a smaller number of high-value orders pull the average above the typical order.
- Age is spread fairly evenly across the 18–65 range with no single group dominating.
- City distribution is led by Patna, Kolkata, and Mumbai; the "Unknown" bucket (filled during Task 1's cleaning) accounts for only 13 of 1,000 orders, so it doesn't distort city-level comparisons.

Histograms for the numerical columns and a bar chart of orders by city are included in the supporting notebook/script.

## 2. SQL for Business Questions

A SQLite instance was built from the cleaned dataset (table `sales`), with a second table `city_region` added to practice joins. Seven business questions were answered — see `Task2_Step2_SQL_Business_Questions.md` for the full set of queries and results. Summary:

| Question | Finding |
|---|---|
| Top 5 products by revenue | Laptop, Mobile, and Book are within ₹4 lakh of each other at the top |
| Monthly revenue trend | Ranges ₹92L–₹1.3Cr per month through 2025; Jan 2026 is partial data, not a real drop |
| Revenue by city | Patna leads; "Unknown" city is a small enough share to ignore |
| Avg order value by gender | ₹1,36,883 (F) vs ₹1,41,807 (M) — no meaningful difference |
| Revenue by age group | 36–45 is the strongest segment |
| Orders with Quantity > 5 | 481 orders (48%) account for ₹9.93 Cr |
| Revenue by region (join) | East leads, driven by Patna and Kolkata |

## 3. Multivariate Analysis & Correlation

Correlation matrix across the four numerical fields:

|  | Age | Quantity | Unit_Price | Total_Sales |
|---|---|---|---|---|
| Age | 1.00 | -0.03 | -0.01 | 0.00 |
| Quantity | -0.03 | 1.00 | 0.02 | 0.65 |
| Unit_Price | -0.01 | 0.02 | 1.00 | 0.69 |
| Total_Sales | 0.00 | 0.65 | 0.69 | 1.00 |

Age shows no linear relationship with any other field. Quantity and Unit_Price both correlate moderately with Total_Sales (expected, since Total_Sales is derived from both), but not with each other — customers don't consistently buy more units of cheaper items or vice versa.

A boxplot of Total_Sales by Category shows similar medians across all five categories (~₹1.0–1.1L), with Electronics showing the most high-value outliers — occasional large orders (e.g. multiple laptops) rather than a consistently higher price point.

## 4. Static Dashboard Mock-up

`ApexPlanet_Dashboard_Mockup.pptx` — a 3-slide mock-up proposing the metrics for a future interactive dashboard:

- **Slide 2** — the dashboard layout itself: four headline KPIs (Total Revenue, Total Orders, Avg Order Value, Top Category) plus a monthly revenue trend line and a top-5-products bar chart.
- **Slide 3** — rationale for each KPI, tied to a specific business decision it supports.

KPIs were chosen to cover both scale (revenue, order count) and behavior (average value, category and product mix, trend over time) rather than listing every number the dataset could produce.

## Files

| File | Contents |
|---|---|
| `ApexPlanet_Cleaned_Dataset.xlsx` | Input dataset (from Task 1) |
| `Task2_Step2_SQL_Business_Questions.md` | Full SQL queries and answers |
| `ApexPlanet_Dashboard_Mockup.pptx` | Dashboard mock-up (3 slides) |
| `README_Task2.md` | This file |

## Tools

Python (Pandas, Matplotlib, Seaborn), SQLite, PowerPoint.
