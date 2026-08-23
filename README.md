# E-commerce Sales Analysis

A Power BI project analyzing sales performance, profitability, customer distribution, product performance, and shipping efficiency using the Sample Superstore dataset (2014–2017).

The project is built on a validated star-schema data model and demonstrates practical Data Analyst skills in data preparation, data modeling, DAX, KPI development, visualization, and business analysis.

## Project Overview

Raw transactional data from `Sample - Superstore.csv` is transformed through Power Query into a structured Power BI star schema consisting of fact and dimension tables.

The model supports interactive analysis of:

- Sales performance
- Profitability
- Customer value
- Product performance
- Geographic distribution
- Shipping performance
- Time-based sales trends

The final report contains four interactive Power BI pages designed to answer practical business questions and translate transactional data into actionable insights.

## Business Problem

Sales totals alone do not reveal which products, customers, or regions are contributing to profitability, nor do they provide sufficient visibility into shipping performance.

The project provides a structured analytical model that allows business performance to be analyzed consistently across time, customers, products, categories, regions, and shipping methods.

## Objectives

- Build a validated analytical model for Sales, Profit, and Profit Margin.
- Identify loss-making products requiring further investigation.
- Analyze customer value and distribution by region and segment.
- Evaluate product and category performance.
- Analyze shipping performance and delivery duration.
- Provide an interactive dashboard that supports business-oriented analysis and decision-making.

## Business Questions

- What are total Sales, Profit, and Profit Margin?
- How have Sales changed over time?
- Which products generate the highest and lowest Sales and Profit?
- Which products are loss-making?
- Which categories and sub-categories contribute most to performance?
- How are customers distributed across regions and segments?
- What are the average Sales and Profit contributions per customer?
- How many orders are placed through each shipping method?
- How quickly are orders shipped?
- Which areas require further investigation?

## Dataset

The project uses the Sample Superstore dataset covering U.S. retail transactions from 2014 to 2017.

**Source:** `Sample - Superstore.csv`

| Field Group | Columns |
|---|---|
| Order | Row ID, Order ID, Order Date, Ship Date, Ship Mode |
| Customer | Customer ID, Customer Name, Segment |
| Location | Country, City, State, Postal Code, Region |
| Product | Product ID, Category, Sub-Category, Product Name |
| Transaction | Sales, Quantity, Discount, Profit |

## Dataset Quality

- Rows: **9,994**
- Columns: **21**
- Missing values: **None**
- Fully duplicated rows: **None**
- Invalid dates: **None**
- Negative Sales values: **None**
- Negative Quantity values: **None**
- Invalid Discount values: **None**
- Ship Date before Order Date: **None**

## Data Preparation

Power Query is used to prepare and structure the source data before loading it into the analytical model.

Key preparation steps include:

- Data type validation
- Date cleaning and standardization
- Creation of Shipping Days
- Creation of Delivery Status
- Separation of transactional data from descriptive dimensions
- Deduplication of dimension tables using their appropriate business keys
- Validation of relationships and key uniqueness

`Dim_Product` is deduplicated using `Product ID`, which is the appropriate product key.

`Shipping Days` represents the difference between `Ship Date` and `Order Date`.

## Data Model

The project uses a star-schema architecture.

```text
                    ┌────────────────┐
                    │    Dim_Date    │
                    └───────┬────────┘
                            │
                            │ 1 : *
                            ▼
┌────────────────┐    ┌────────────────┐    ┌────────────────┐
│ Dim_Customer   │───▶│                │◀───│  Dim_Product   │
└────────────────┘ 1:* │   Fact_Sales  │ 1:*└────────────────┘
                       │                │
                       └────────────────┘
                         ┌──────────────┐
                         │  _Measures   │
                         │ Disconnected │
                         └──────────────┘
```

## Fact Table

`Fact_Sales` contains the transactional order-line data, including:

- Order ID
- Row ID
- Order Date
- Ship Date
- Customer ID
- Product ID
- Ship Mode
- Region
- State
- City
- Sales
- Quantity
- Discount
- Profit
- Shipping Days
- Delivery Status

## Dimension Tables

### Dim_Date

Provides the calendar structure required for time-based analysis.

### Dim_Customer

Contains unique:

- Customer ID
- Customer Name
- Segment

### Dim_Product

Contains unique:

- Product ID
- Product Name
- Category
- Sub-Category

`Dim_Product` is deduplicated using `Product ID`.

## Relationships

All dimension-to-fact relationships follow the standard star-schema pattern:

- One-to-many cardinality
- Single-direction filtering
- Dimension → Fact

`Dim_Date` has:

- An active relationship with `Fact_Sales[Order Date_Clean]`
- An inactive relationship with `Fact_Sales[Ship Date_Clean]`

This allows the same Date dimension to support both order-date and shipping-date analysis when required.

The `_Measures` table is intentionally disconnected and is used only to organize DAX measures.

## DAX & KPI Design

Analytical KPIs are implemented as DAX measures and organized in the dedicated `_Measures` table.

Row-level attributes such as `Shipping Days` and `Delivery Status` are stored as columns in `Fact_Sales`.

| KPI | Definition |
|---|---|
| Total Sales | `SUM(Fact_Sales[Sales])` |
| Total Profit | `SUM(Fact_Sales[Profit])` |
| Profit Margin | `DIVIDE([Total Profit], [Total Sales])` |
| Total Orders | `DISTINCTCOUNT(Fact_Sales[Order ID])` |
| Total Customers | `DISTINCTCOUNT(Fact_Sales[Customer ID])` |
| Total Products | `DISTINCTCOUNT(Dim_Product[Product ID])` |
| Total Quantity | `SUM(Fact_Sales[Quantity])` |
| Average Order Value | `DIVIDE([Total Sales], [Total Orders])` |
| Average Sales per Customer | `DIVIDE([Total Sales], [Total Customers])` |
| Average Profit per Customer | `DIVIDE([Total Profit], [Total Customers])` |
| Average Sales per Product | `DIVIDE([Total Sales], [Total Products])` |
| Average Profit per Product | `DIVIDE([Total Profit], [Total Products])` |
| Loss-Making Products | Products whose total profit is below zero in the current filter context |
| Average Shipping Days | `AVERAGE(Fact_Sales[Shipping Days])` |
| Fastest Shipping | `MIN(Fact_Sales[Shipping Days])` |
| Longest Shipping | `MAX(Fact_Sales[Shipping Days])` |

## Validated Results

Core project metrics were validated against the source dataset and cross-checked against the Power BI model.

| KPI | Value |
|---|---:|
| Total Sales | **$2,297,200.86** |
| Total Profit | **$286,397.02** |
| Profit Margin | **12.47%** |
| Total Quantity | **37,873** |
| Total Orders | **5,009** |
| Total Customers | **793** |
| Average Sales per Customer | **$2,896.85** |
| Average Profit per Customer | **$361.16** |
| Total Products | **1,862** |
| Loss-Making Products | **299** |
| Fastest Shipping | **0 days** |
| Longest Shipping | **7 days** |

## Customer Distribution by Region

Customer counts are calculated within each region. Because customers may purchase across multiple regions, these regional counts should not be summed to derive the total unique customer count.

| Region | Customers |
|---|---:|
| Central | 629 |
| East | 674 |
| South | 512 |
| West | 686 |

## Dashboard

The Power BI report contains four analytical pages.

### 1. Executive Overview

Provides a high-level view of business performance:

- Total Sales
- Total Profit
- Profit Margin
- Total Quantity
- Sales trend over time
- Sales by Region
- Sales by Category

### 2. Customer Analysis

Focuses on customer value and distribution:

- Total Customers
- Average Sales per Customer
- Average Profit per Customer
- Customer-level Sales performance
- Customer profitability
- Segment distribution
- Regional distribution

### 3. Product Analysis

Analyzes product and category performance:

- Total Products
- Loss-Making Products
- Average Product Sales
- Average Product Profit
- Product Sales and Profit
- Category performance
- Sub-category performance
- High- and low-performing products

### 4. Shipping Analysis

Evaluates shipping performance:

- Total Orders
- Shipping mode distribution
- Shipping-day distribution
- Average shipping duration
- Fastest and longest shipping
- Delivery Status
- Regional shipping performance

## Key Insights

The full business analysis is available in `Insights.md`.

Key findings include:

- Total Sales reached **$2.30M**, with Total Profit of **$286.4K** and a **12.47% Profit Margin**.
- **299 products** are loss-making and require further investigation.
- Customer value is unevenly distributed across the customer base, creating opportunities for targeted retention and growth strategies.
- Product and category performance varies significantly, highlighting the importance of analyzing profitability alongside sales volume.
- The business serves four regions, with customer distribution varying across Central, East, South, and West.
- Shipping performance ranges from **0 to 7 days**, providing an opportunity to evaluate shipping efficiency by region and shipping method.

## Business Recommendations

### 1. Investigate Loss-Making Products

Investigate loss-making products to identify pricing, discount, product-cost, or demand-related causes.

### 2. Analyze High-Value Customers

Analyze high-value customers and develop targeted retention strategies for customers contributing disproportionately to revenue and profit.

### 3. Review Discount and Profitability Patterns

Review discount and profitability patterns across products and categories to identify cases where higher sales do not translate into stronger profit.

### 4. Evaluate Regional Performance

Evaluate regional performance to identify underperforming markets and opportunities for targeted growth.

### 5. Monitor Shipping Efficiency

Monitor shipping efficiency by shipping mode and region to identify opportunities for reducing delivery times and improving operational performance.

## Tools & Technologies

- Power BI
- Power Query
- DAX
- Star Schema Data Modeling
- Data Quality Validation
- Business Intelligence
- Data Visualization
- Business Analysis

## Project Structure

```text
E-commerce-Sales-Analysis/

│
├── Sample - Superstore.csv
├── E-commerce sales.pbix
├── README.md
└── Insights.md
```

## Reproduction

To reproduce the project:

1. Load `Sample - Superstore.csv` into Power BI.
2. Perform the required Power Query transformations.
3. Create `Fact_Sales`, `Dim_Customer`, `Dim_Product`, and `Dim_Date`.
4. Ensure dimension keys are unique.
5. Deduplicate `Dim_Product` using `Product ID`.
6. Create one-to-many relationships between dimensions and `Fact_Sales`.
7. Use single-direction filtering from dimensions to the fact table.
8. Mark `Dim_Date` as the official Date Table.
9. Create an active relationship between `Dim_Date[Date]` and `Fact_Sales[Order Date_Clean]`.
10. Create an inactive relationship between `Dim_Date[Date]` and `Fact_Sales[Ship Date_Clean]`.
11. Create `Shipping Days` and `Delivery Status` as columns in `Fact_Sales`.
12. Create analytical KPIs as DAX measures in the disconnected `_Measures` table.
13. Bind report visuals to `Fact_Sales`, `Dim_*`, and `_Measures`.
14. Validate core KPIs against the source dataset.

## Project Outcome

This project demonstrates an end-to-end Data Analyst workflow:

```text
Raw Data
   ↓
Data Quality Validation
   ↓
Power Query Transformation
   ↓
Star Schema Data Model
   ↓
DAX Measures & KPIs
   ↓
Interactive Power BI Dashboard
   ↓
Business Analysis
   ↓
Insights & Recommendations
```

The project demonstrates practical capabilities in:

- Data preparation
- Data quality validation
- Data modeling
- Star-schema design
- DAX
- KPI development
- Power BI visualization
- Business analysis
- Analytical storytelling
- Insight generation