---
layout: post
title: "Inside Retail Operations: A Case Study on Sales, Inventory, and Vendors"
date: 2025-05-18
excerpt: "What does it take to run a successful retail business? It's knowing what sells, how fast inventory moves, and which vendors truly impact your bottom line. "
cover: /assets/images/Cover_Bibitor.png
published: false
---

<!----------- Table of Contents ----------->
<details>
<summary><strong>Table of Contents</strong></summary>
<ul>
<li><a href="#intro">1. Introduction</a></li>
<li><a href="#sql">2. Analysis with SQL</a></li>
</ul>
</details>

<!------------ Intro ------------>
<!-- <img src="/assets/images/Cover_Bibitor.png" alt="Liquour Sales" width="800"/> -->
<hr style="width: 40%; border: none; border-top: 1px dashed lightgray; margin: 40px auto;">

<div style="text-align: left;">
  <h1 id="intro" style="font-weight: bold;">1. INTRODUCTION</h1>
</div>

What does it take to run a successful liquor business? It’s not just about stocking the right products — it’s about understanding what sells, how fast it moves, and which vendors help or hurt your bottom line.

In this case study, I analyze data from Bibitor, LLC — a fictional retail chain with 80+ locations and over $450M in annual sales — to uncover patterns patterns in vendor performance, inventory movement, and sales behavior, applying real-world retail concepts.

### 🧾 About the Dataset
The dataset come from the **[HUB of Analytics Education](https://www.hubae.org)** and mimics operations in a large-scale liquor retailer in Lincoln, USA. It spans December 2016 and includes 6 key tables:
- **Inventory**
  - `BegInvDec`: Inventory at the start of December 2016.
  - `EndInvDec`: Inventory remaining at the end of December 2016.

- **Purchases**
  - `PurchasesDec`: What Bibitor bought from vendors (quantities, total cost, vendor info).
  - `PricingPurchasesDec`: Reference prices Bibitor expects from suppliers.

- **Vendor Invoices**
  - `VendorInvoicesDec`: The bills Bibitor received from their suppliers (vendors).

- **Sales**
  - `SalesDec`: Item-level sales data including price, quantity, and total revenue.

These tables, when combined, allow us to track products from purchase to sale, understand vendor relationships, and monitor financial flows, all essential for optimizing retail operations.

### 🔑 Key Business Questions
- Which vendors provide the most value?
- Are we overstocking or underutilizing inventory?
- How do purchase prices compare to actual sales?
- What’s the average time it takes to sell received stock?

### 🧩 Data Model
Before diving into the code, we first need to understand how all the different pieces of data connect. An *Entity-Relationship Diagram (ERD)* visually represents these connections, providing the logical framework for accurate and efficient analysis. This ensures our data joins are correct and our derived insights are reliable.

The ERD below guided our analysis, showing the relationships between Bibitor's core transactional and master data tables:

As shown, tables like PurchasesDec and `VendorInvoicesDec` are linked by shared keys like `VendorNumber` and `PONumber`, representing the core of Bibitor's procurement. `SalesDec` connects through `InventoryId` to track items' journeys from purchase to customer. This structure ensures a cohesive flow for tracing products and understanding financial transactions across the business.


<!------------------------------ SQL  ----------------------------------->
<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>

<div style="text-align: left;">
  <h1 id="sql" style="font-weight: bold;">2. ANALYSIS WITH SQL</h1>
</div>

SQL was the primary tool for extracting, transforming, and performing the initial layers of analysis on Bibitor's vast datasets. Its power allowed us to systematically address business questions at a granular level.

## 2.1. Initial Data Health Check (`Initial Analysis.sql`)
Before any deep dive, ensuring the data's integrity was crucial. The `Initial Analysis.sql` script acted as our data auditor, meticulously checking for common pitfalls like missing entries, zero values in critical financial columns, and inconsistencies that could skew our results.

### 🔑 Key actions & questions addressed:   
- **Identifying invalid entries:** Are there sales, purchase, or pricing records with missing or zero dollar/price amounts?
- **Assessing completeness:** What percentage of our data might be incomplete or erroneous?
- **Validating derived values:** Do calculated values (e.g., `PurchasePrice * Quantity`) consistently match recorded totals, or are there unexpected variances?
- **Cross-table consistency:** Are vendor records consistent across purchasing and sales datasets?

### 🔍 A glimpse into the Code:
#### a. Missing or Zero values
**📦 Purchases:**
```sql
SELECT * FROM PurchasesDec WHERE Dollars <= 0 OR Dollars IS NULL;
```

*Sample Output:*

| InventoryId        | Store | ... | PurchasePrice | Quantity | Dollars |
|--------------------|-------|-----|---------------|----------|---------|
| 59_CLAETHORPES_2166| 59    | ... | 0             | 12       | 0       |
| 38_GOULCREST_2166  | 38    | ... | 0             | 12       | 0       |
| 34_PITMERDEN_2166  | 34    | ... | 0             | 12       | 0       |

This query returned 153 entries where the **`Dollars`** value is zero or null. Given that `Dollars` is calculated as `PurchasePrice * Quantity`, this directly implies that **`PurchasePrice`** for these entries is also zero, requiring further investigation. Potential reasons for these entries include:
- **Promotional or Free Goods:** Items given away as part of a promotion, marketing campaign, or bundled with other purchases.
- **Samples:** Products recorded as samples for in-store use or customer trials.
- **Data Entry Errors:** Mistakes made during data input.

**📦 Sales:**
```sql
SELECT * FROM SalesDec WHERE SalesDollars <= 0 OR SalesDollars IS NULL;
```

*Sample Output:*

| InventoryId           | Store | Brand | SalesQuantity | SalesDollars | ... |
|------------------------|-------|--------|----------------|---------------|-----|
| 38_GOULCREST_25340     | 38    | 25340  | 3              | 0             | ... |
| 66_EANVERNESS_25340    | 66    | 25340  | 3              | 0             | ... |
| 66_EANVERNESS_25340    | 66    | 25340  | 1              | 0             | ... |

Our analysis revealed 55 entries where the **`SalesDollars`** field is zero or null. Since `SalesDollars` is derived from `SalesPrice` multiplied by `SalesQuantity`, a zero `SalesDollars` value means that the **`SalesPrice`** for these transactions is effectively zero as well. This warrants further investigation.



<!------------------------------ DASHBOARDS  ----------------------------------->
<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>