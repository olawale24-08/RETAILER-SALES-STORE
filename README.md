## Overview

This project presents an end-to-end data analytics solution for analyzing retail store sales and customer purchasing activity.

The objective was to transform raw retail transaction data into actionable business insights by evaluating sales performance, order volume, quantity sold, payment methods, product categories, store locations, and purchasing patterns across different days and hours.

The project covers the complete analytics workflow, from dataset loading and cleaning using SQL to exploratory data analysis, business-focused SQL analysis, interactive Power BI dashboard development, and analytical reporting.

## Business Problem

Retail businesses generate large volumes of transaction data across customers, products, payment methods, locations, and time periods.

Without effective analysis, it can be difficult to:

Monitor overall sales and order performance.

Identify sales trends across different periods.

Understand customer purchasing patterns.

Compare product category performance.

Evaluate payment method usage.

Identify peak sales days and hours.

Compare weekday and weekend purchasing activity.

Monitor month-over-month changes in order volume.

This project addresses these challenges by transforming raw retail transaction data into structured analysis and an interactive Power BI dashboard.

## Project Objectives

Analyze total sales, orders, and quantity sold.

Identify sales trends over time.

Evaluate month-over-month order performance.

Compare sales across product categories.

Analyze payment method performance.

Compare weekday and weekend sales.

Identify sales patterns by day and hour.

Analyze payment activity across store locations.

Present findings through an interactive Power BI dashboard and supporting report.

## Dataset

The project uses a retail transaction dataset containing customer, transaction, product, payment, location, and sales information.

## Key Data Categories

Category

Examples

Transaction Data

Transaction date, sales amount, quantity

Customer Data

Customer ID

Product Data

Product category

Payment Data

Cash, PayPal, Credit Card, Debit Card

Location Data

Store/location information

Time Dimensions

Year, month, day, weekday/weekend, hour


## Tools & Technologies

SQL Server / SSMS – Data loading, cleaning, transformation, and analysis.

SQL – CTEs, aggregations, date functions, CASE statements, and window functions.

Power BI – Interactive dashboard development and data visualization.

Power Query – Data preparation where applicable.

Excel / CSV – Dataset inspection and initial data handling, where applicable.

Data Analysis Techniques – Exploratory data analysis, trend analysis, time-based analysis, and performance comparisons.

## Project Workflow

1. Data Loading

Loaded the raw retail sales dataset into SQL Server and reviewed the available fields, data types, and transaction-level records.

2. Data Cleaning & Transformation

Performed data preparation activities using SQL, including:

Checking for missing and inconsistent values.

Reviewing duplicate records where applicable.

Validating data types.

Standardizing relevant fields.

Preparing transaction dates for time-based analysis.

Validating sales, quantity, and customer fields.

Creating structured datasets for analysis.

3. Exploratory Data Analysis (EDA)

Performed EDA to identify trends, relationships, and purchasing patterns.

Key areas explored included:

Sales performance over time.

Monthly order volume.

Product category sales.

Payment method performance.

Weekday versus weekend sales.

Sales by day and hour.

Store/location-level payment activity.

Quantity sold and order activity.

4. SQL Business Analysis

Developed SQL queries to answer key business questions and calculate analytical metrics.

Examples include:

Total sales and order volume.

Sales by product category.

Sales by payment method.

Sales by weekday/weekend.

Sales by day and hour.

Monthly order analysis.

Month-over-month order difference.

Month-over-month order growth percentage.

A key analysis used the LAG() window function to compare each month's order volume with the previous month.

5. Power BI Dashboard Development

Built an interactive Power BI dashboard to communicate the main findings and provide an easy-to-use view of retail performance.

The dashboard includes KPI cards, trend analysis, category comparisons, payment analysis, time-based visuals, and location-level analysis.

6. Analytical Reporting

Prepared a supporting report documenting the analysis process, key findings, trends, and business insights identified from the dataset.

Dashboard

The Power BI dashboard provides an interactive overview of retail sales performance.

Retail Sales Overview

The dashboard includes:

Total Sales

Total Orders

Total Quantity Sold

Sales Trend Over Time

Sales by Weekday / Weekend

Sales by Payment Method

Top 10 Payment Methods by Store Location

Sales by Product Category

Sales by Day and Hour

Monthly/date filtering

The dashboard allows users to filter the analysis by month and explore changes in sales performance across different dimensions.



## Key Results & Insights

The analysis provides visibility into several important areas of retail performance.

1. Sales Performance

Analyzes overall sales performance and how revenue changes across the reporting period.

2. Order Trends

Month-over-month analysis was used to identify increases and decreases in order activity and provide a clearer view of changes in customer purchasing volume.

3. Product Category Performance

Compares sales across product categories to identify categories contributing different levels of sales.

4. Payment Method Analysis

Evaluates sales contribution from payment methods, including PayPal, Cash, Credit Card, and Debit Card.

5. Customer Purchasing Patterns

Compares weekday and weekend sales and analyzes sales activity across different hours of the day.

6. Location-Level Analysis

Examines payment activity across store locations to provide a more detailed view of transaction behavior.

The dashboard is designed to support business discussions and further investigation. Specific recommendations should be based on validated calculations and the underlying dataset.

## SQL Analysis Example

One of the key analyses calculates month-over-month order differences and growth using the LAG() window function.

WITH MonthlyOrders AS (
    SELECT
        DATEPART(YEAR, TransactionDate) AS Year,
        DATEPART(MONTH, TransactionDate) AS Month,
        COUNT(DISTINCT CustomerID) AS TotalOrders
    FROM RETAILER_SALES
    GROUP BY
        DATEPART(YEAR, TransactionDate),
        DATEPART(MONTH, TransactionDate)
)

SELECT
    Year,
    Month,
    TotalOrders,

    TotalOrders - LAG(TotalOrders, 1)
        OVER (ORDER BY Year, Month) AS MoMDifference,

    CASE
        WHEN LAG(TotalOrders, 1)
            OVER (ORDER BY Year, Month) IS NULL
        THEN NULL

        ELSE
            (TotalOrders - LAG(TotalOrders, 1)
                OVER (ORDER BY Year, Month))
            * 100.0
            / LAG(TotalOrders, 1)
                OVER (ORDER BY Year, Month)
    END AS MoMGrowth

FROM MonthlyOrders
ORDER BY
    Year,
    Month;

This analysis makes it possible to monitor whether order activity increased or decreased compared with the previous month.

Additional SQL queries used for data cleaning, EDA, and business analysis can be included in the sql/ folder.

## Project Deliverables

Deliverable

Description

Cleaned Dataset

Prepared and validated retail transaction data

SQL Analysis

Data cleaning, EDA, and business analysis queries

Exploratory Data Analysis

Investigation of sales and customer purchasing patterns

Power BI Dashboard

Interactive retail sales performance dashboard

Analytical Report

Documentation of methodology, findings, and insights

Project Structure

Retail-Store-Sales-Analytics/
│
├── data/
│   └── retail_sales.csv
│
├── sql/
│   ├── data_cleaning.sql
│   ├── eda.sql
│   └── monthly_analysis.sql
│
├── powerbi/
│   └── retail_sales_dashboard.pbix
│
├── images/
│   ├── dashboard.png
│   └── sql_queries/
│       ├── query_01.png
│       ├── query_02.png
│       ├── query_03.png
│       └── ...
│
├── report/
│   └── retail_sales_analysis.pdf
│
└── README.md

## How to Run the Project

Prerequisites

To explore or reproduce this project, you will need:

Microsoft SQL Server

SQL Server Management Studio (SSMS)

Microsoft Power BI Desktop

The original retail sales dataset

Power BI report file (.pbix), if available

## Steps

Clone or download this repository.

git clone https://github.com/yourusername/retail-store-sales-analytics.git

Open the project folder.

Create a database in SQL Server.

Load the retail sales dataset into SQL Server.

Run the data-cleaning SQL scripts.

Run the EDA and business analysis queries.

Review the SQL results and calculated metrics.

Open the Power BI .pbix file.

If required, update the data source connection in Power BI.

Refresh the dataset.

Explore the dashboard using the available filters and visualizations.

Review the analytical report for the detailed findings.

Skills Demonstrated

## SQL Data Cleaning

Exploratory Data Analysis (EDA)

SQL Server

Common Table Expressions (CTEs)

Window Functions

LAG() and Month-over-Month Analysis

Data Aggregation

Date & Time Analysis

Business Intelligence

Power BI Dashboard Development

Power Query

Data Visualization

KPI Development

Trend Analysis

Customer Purchasing Analysis

Business Reporting

Data-Driven Decision Support


## Recommendations

Based on the analysis and dashboard findings, the following business recommendations can be considered:

### 1. Monitor Sales Trends Regularly

Regular monitoring helps management investigate changes in demand and respond to emerging patterns using monthly sales and order trends to identify periods of growth and decline.

### 2. Focus on High-Performing Product Categories

Review product categories that contribute strongly to overall sales and investigate the factors driving their performance. This can support inventory planning, promotional activities, and product strategy.

### 3. Optimize Peak Sales Periods

Using the day and hour analysis to identify periods of higher customer activity. Staffing, inventory availability, and promotional campaigns can be aligned with these periods where appropriate.

### 4. Review Payment Method Performance

Monitor sales across different payment methods to understand customer preferences and ensure commonly used payment options remain reliable and convenient.

### 5. Investigate Month-over-Month Declines

Where the analysis identifies a decline in monthly orders or sales, investigate the underlying causes by breaking the results down by product category, payment method, location, and time period.

### 6. Analyze Location-Level Performance

Use store or location-level analysis to identify differences in transaction and payment activity. Locations with unusual patterns can be investigated further to understand potential operational or customer-related factors.
