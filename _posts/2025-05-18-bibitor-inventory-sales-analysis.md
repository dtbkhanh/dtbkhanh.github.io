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

### 🧩 About the Dataset
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

### 🧩 Data Model
Before writing a single line of code, understanding how the different pieces of data relate to each other is paramount. An Entity-Relationship Diagram (ERD) visually represents these connections, forming the logical backbone for accurate and efficient analysis. It ensures that our joins are correct and our derived insights are reliable.

Below is the ERD that guided our analysis, illustrating the relationships between Bibitor's core transactional and master data tables:

As shown, tables like PurchasesDec and `VendorInvoicesDec` are linked by shared keys like `VendorNumber` and `PONumber`, representing the core of Bibitor's procurement. `SalesDec` connects through `InventoryId` to track items' journeys from purchase to customer. This structure ensures a cohesive flow for tracing products and understanding financial transactions across the business.

<!------------------------------ SQL  ----------------------------------->
<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>

<div style="text-align: left;">
  <h1 id="sql" style="font-weight: bold;">2. ANALYSIS WITH SQL</h1>
</div>

SQL was the primary tool for extracting, transforming, and performing the initial layers of analysis on Bibitor's vast datasets. Its power allowed us to systematically address business questions at a granular level.

## 2.1. Initial Data Health Check (`Initial Analysis.sql`)
Before any deep dive, ensuring the data's integrity was crucial. The `Initial Analysis.sql` script acted as our data auditor, meticulously checking for common pitfalls like missing entries, zero values in critical financial columns, and inconsistencies that could skew our results.

### Key actions & questions addressed:   
- **Identifying invalid entries:** Are there sales, purchase, or pricing records with missing or zero dollar/price amounts?
- **Assessing completeness:** What percentage of our data might be incomplete or erroneous?
- **Validating derived values:** Do calculated values (e.g., PurchasePrice * Quantity) consistently match recorded totals, or are there unexpected variances?
- **Cross-table consistency:** Are vendor records consistent across purchasing and sales datasets?

### A glimpse into the Code:
One vital check was identifying where the recorded `Dollars` in our `PurchasesDec` table didn't align with the simple multiplication of `PurchasePrice` and `Quantity`. While minor differences can be due to floating-point precision, larger discrepancies signal potential data entry or system issues.

<!------------------------------ DASHBOARDS  ----------------------------------->
<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>