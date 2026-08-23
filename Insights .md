# E-commerce Sales Analysis — Insights Report

**Dataset:** Sample Superstore (9,994 order lines, 2014–2017)  
**Model:** Star schema — `Fact_Sales`, `Dim_Customer`, `Dim_Product`, `Dim_Date`, `_Measures`

---

## 1. Executive Summary

The business generated **$2,297,200.86** in total Sales and **$286,397.02** in Profit across **5,009 orders** and **793 unique customers** between 2014 and 2017, resulting in a blended **Profit Margin of 12.47%**.

While the overall business is profitable, product-level performance reveals a significant area requiring attention: **299 of 1,862 products (16.1%) are loss-making** based on their total recorded Profit.

Customer counts vary across the four U.S. regions, while shipping duration ranges from **0 to 7 days**.

The most actionable finding in this dataset is therefore the presence of a substantial group of loss-making products, which warrants further investigation into pricing, discounting, product mix, and other profitability drivers.

---

## 2. Business Problem

A retailer needs visibility into which products, customers, and regions actually contribute to profitability — not just revenue — and how efficiently orders are fulfilled.

Aggregate Sales figures alone can hide products that generate revenue while simultaneously producing negative Profit.

This analysis therefore focuses on understanding overall financial performance, identifying loss-making products, evaluating customer distribution and value, and assessing shipping performance.

---

## 3. Objectives

- Quantify total Sales, Profit, and Profit Margin.
- Identify loss-making products and quantify their scale.
- Understand customer distribution and value across regions and segments.
- Evaluate product and category performance.
- Assess shipping performance, including shipping duration and shipping mode distribution.
- Translate the findings into practical areas for business investigation.

---

## 4. Data Overview

| Metric | Value |
|---|---:|
| Order lines | 9,994 |
| Unique orders | 5,009 |
| Unique customers | 793 |
| Unique products (Product ID) | 1,862 |
| Date range | 2014–2017 |
| Regions | Central, East, South, West |

### Product Granularity

The dataset contains **1,862 unique Product IDs** and **1,850 unique Product Names**.

Product Name is therefore not guaranteed to be unique. For product-level analysis, **Product ID is treated as the appropriate product key and analytical grain**.

This distinction is important when calculating product counts, profitability, and loss-making products.

---

## 5. Analytical Approach

The analysis uses a Power BI star-schema model consisting of:

- `Fact_Sales` — transactional order-line data.
- `Dim_Customer` — customer attributes.
- `Dim_Product` — product and category attributes.
- `Dim_Date` — time-based analysis.
- `_Measures` — centralized DAX measures.

The analysis combines company-level KPIs with customer-, product-, regional-, and shipping-level analysis to identify areas that require further business investigation.

---

## 6. Data Quality

The source dataset contains:

- **9,994 order lines**
- No missing values
- No fully duplicated rows
- No invalid dates
- No negative Sales values
- No negative Quantity values
- No invalid Discount values
- No Ship Date values occurring before Order Date

A key modeling consideration is that **Product ID**, rather than Product Name, should be used as the unique product key because product names are not guaranteed to be unique.

---

## 7. KPI Overview

| KPI | Value |
|---|---:|
| Total Sales | **$2,297,200.86** |
| Total Profit | **$286,397.02** |
| Profit Margin | **12.47%** |
| Total Quantity | **37,873 units** |
| Total Orders | **5,009** |
| Average Order Value | **$458.61** |
| Total Customers | **793** |
| Average Sales per Customer | **$2,896.85** |
| Average Profit per Customer | **$361.16** |
| Total Products | **1,862** |
| Loss-Making Products | **299 (16.1% of catalog)** |
| Fastest Shipping | **0 days** |
| Longest Shipping | **7 days** |

---

## 8. Overall Profitability

The dataset generated approximately **$2.30M in Sales** and **$286.4K in Profit**, producing a **12.47% blended Profit Margin**.

At the company level, the business is therefore profitable.

However, the overall margin does not tell the complete story. Product-level analysis reveals substantial variation in profitability, including a meaningful number of products with negative total Profit.

This highlights an important analytical principle: **strong aggregate performance does not necessarily mean that every product contributes positively to profitability.**

---

## 9. Loss-Making Products

**299 of 1,862 products (16.1%)** are loss-making based on their total recorded Profit across the available transactions.

This is the clearest profitability issue identified in the dataset.

The finding suggests that management should not evaluate product performance using Sales volume alone. A product can generate significant revenue while still producing negative Profit.

Potential areas for further investigation include:

- Discount levels
- Product category
- Sub-category
- Sales volume
- Regional performance
- Product-level pricing and cost structure

The current dataset can identify which products are loss-making, but additional analysis is required to determine the exact cause of those losses.

---

## 10. Customer Insights

The dataset contains **793 unique customers** generating approximately **$2.30M in Sales** and **$286.4K in Profit**.

On average, each customer contributes:

- **$2,896.85 in Sales**
- **$361.16 in Profit**

These averages provide a useful high-level view of customer value, but they should not be interpreted as evidence that all customers contribute equally.

Customer-level profitability can vary substantially, so the averages should be used as an overall benchmark rather than as a representation of an individual customer's expected value.

Further segmentation by customer, Segment, and Region can provide a more detailed understanding of customer concentration and profitability.

---

## 11. Regional Customer Distribution

| Region | Unique Customers |
|---|---:|
| West | 686 |
| East | 674 |
| Central | 629 |
| South | 512 |

The **West** has the largest number of unique customers at **686**, while the **South** has the lowest at **512**.

The difference indicates that customer concentration is not identical across regions.

However, customer count alone does not establish whether one region is commercially stronger than another. A region with fewer customers could still generate higher Sales or Profit per customer.

Therefore, regional customer counts should be considered alongside Sales, Profit, and customer value before making business decisions.

---

## 12. Product Insights

Product-level analysis identifies **299 loss-making products**, representing **16.1% of the product portfolio**.

This makes product profitability one of the most important areas for deeper investigation.

A useful next step is to rank products by total Profit and total loss to identify the products creating the largest negative contribution.

The analysis should then be extended across:

- Category
- Sub-category
- Discount
- Sales volume
- Region

This would help determine whether losses are concentrated in specific product groups or are distributed broadly across the portfolio.

---

## 13. Shipping Insights

Shipping duration ranges from **0 to 7 days** across the dataset.

A shipping duration of **0 days** indicates that the Ship Date and Order Date fall on the same date.

The report also analyzes the distribution of orders across the four available shipping modes:

- Standard Class
- Second Class
- First Class
- Same Day

Shipping analysis therefore provides visibility into order-to-shipment timing and shipping-mode usage.

It is important to note that these values represent the difference between **Order Date and Ship Date**, rather than actual carrier transit time after shipment.

---

## 14. Key Findings

- The business generated **$2.30M in Sales** and **$286.4K in Profit**, resulting in a **12.47% Profit Margin**.
- **299 products (16.1% of the catalog)** are loss-making based on their total recorded Profit.
- **Product ID** is the appropriate product-level key because Product Names are not guaranteed to be unique.
- Customer counts vary across regions, with the **West having the highest count** and the **South the lowest**.
- Shipping duration ranges from **0 to 7 days**, providing a relatively compact order-to-shipment range within the dataset.
- Aggregate profitability should not be used alone to evaluate product or customer performance; deeper analysis is required to identify the specific drivers of profitability.

---

## 15. Business Recommendations

### 1. Investigate Loss-Making Products

Create a prioritized list of the **299 loss-making products**, ranked by total loss, and focus management attention on the products with the largest negative contribution.

### 2. Investigate Discount Impact

Analyze the relationship between **Discount and Profit** to determine whether aggressive discounting is associated with negative product profitability.

This analysis should distinguish correlation from causation and should be supported by additional cost information where available.

### 3. Analyze Product Profitability by Category and Sub-category

Break down loss-making products by **Category and Sub-category** to determine whether profitability issues are concentrated in specific product lines.

### 4. Evaluate Customer Value Alongside Customer Count

Customer volume should not be used as the only measure of regional or segment performance.

Sales and Profit per customer should be considered alongside customer counts when evaluating customer groups.

### 5. Monitor Shipping Performance

Continue monitoring shipping duration and shipping-mode distribution by Region and Ship Mode to identify operational differences that may warrant further investigation.

### 6. Monitor Profitability Over Time

Use time-based Sales and Profit analysis to identify changes in business performance and determine whether profitability improves or deteriorates across periods.

---

## 16. Limitations

This is the well-known **Sample Superstore demonstration dataset**. Therefore, the findings demonstrate analytical methodology rather than representing a live business situation.

The dataset does not include a separate product-cost structure. It provides Sales, Discount, and Profit, but does not expose detailed cost components required to independently determine whether a product's loss is primarily caused by high product cost, excessive discounting, or other factors.

The dataset also lacks detailed operational, marketing, inventory, and customer-acquisition information, which limits deeper root-cause analysis.

Shipping analysis is based on the difference between **Order Date and Ship Date**. Therefore, it represents order-to-shipment timing, not actual carrier transit time or customer delivery time.

---

## 17. Future Opportunities

The current analysis establishes the key profitability, customer, product, and shipping findings. Several extensions could provide deeper business value.

### Product Profitability

Break down the **299 loss-making products** by Category and Sub-category and identify where negative profitability is concentrated.

### Discount Analysis

Examine the relationship between **Discount and Profit** to determine whether higher discount levels are associated with weaker profitability.

### Time-Based Profitability

Extend the time analysis beyond Sales trends to evaluate **Profit and Profit Margin changes over time**, including Year-over-Year performance.

### Customer Profitability

Segment customers by Sales and Profit contribution to distinguish high-value customers from customers with lower profitability.

These extensions would move the analysis from identifying performance gaps toward understanding their potential drivers.

---

## Conclusion

The analysis shows a profitable business at the aggregate level, with **$2.30M in Sales**, **$286.4K in Profit**, and a **12.47% Profit Margin**.

However, the overall result hides meaningful product-level variation. The presence of **299 loss-making products, representing 16.1% of the catalog**, is the most significant finding and provides a clear starting point for further profitability analysis.

The dataset also provides useful visibility into customer distribution and shipping performance, while highlighting the importance of analyzing Sales, Profit, customer value, and operational metrics together rather than relying on a single KPI.

Overall, the project demonstrates how a structured Power BI analytical model can transform transactional data into measurable business insights and identify areas requiring further investigation.