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
<li><a href="#1-intro">1. Introduction</a></li>
<li><a href="#2-sql">2. Analysis with SQL</a>
  <ul>
    <li><a href="#2-1-data-health-check">2.1. Initial Data Health Check</a></li>
    <li><a href="#2-2-vendor">2.2. Vendor Performance Analysis</a></li>
    <li><a href="#2-3-inventory">2.3. Inventory Turnover Analysis</a></li>
  </ul>
</li>
</ul>
</details>

<!------------ Intro ------------>
<!-- <img src="/assets/images/Cover_Bibitor.png" alt="Liquour Sales" width="800"/> -->
<hr style="width: 40%; border: none; border-top: 1px dashed lightgray; margin: 40px auto;">

<div style="text-align: left;">
  <h1 id="1-intro" style="font-weight: bold;">1. INTRODUCTION</h1>
</div>

What does it take to run a successful liquor business? It’s not just about stocking the right products — it’s about understanding what sells, how fast it moves, and which vendors help or hurt your bottom line.

This case study analyzes data from Bibitor, LLC — a fictional retail chain with 80+ locations and over $450M in annual sales — to uncover patterns patterns in vendor performance, inventory movement, and sales behavior, applying real-world retail concepts.

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

<!----------------------------------------------------------------------->
<!------------------------------ SQL  ----------------------------------->
<!----------------------------------------------------------------------->

<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>

<div style="text-align: left;">
  <h1 id="2-sql" style="font-weight: bold;">2. ANALYSIS WITH SQL</h1>
</div>

SQL was the primary tool for extracting, transforming, and performing the initial layers of analysis on Bibitor's vast datasets. Its power allowed us to systematically address business questions at a granular level.

All SQL queries used for this analysis are available in the following GitHub repository:
<div style="border: 1px solid #ccc; padding: 15px; margin: 20px 0; border-radius: 5px; text-align: center; transition: box-shadow 0.3s ease-in-out, border-color 0.3s ease-in-out;">
  <strong><a href="https://github.com/dtbkhanh/Data-Analytics-and-Reports/tree/021a7ac923e6cd4f8919e8d023981034e881d0a0/SQL%20Queries/01.%20Bibitor%20LLC%20Inventory%20Analysis" target="_blank" style="text-decoration: none;">➡️ View SQL Queries ⬅️</a></strong>
</div>

<!-------- ** 2.1. Initial Data Health Check ** -------->

<div style="text-align: left;">
  <h2 id="2-1-data-health-check" style="font-weight: bold;">2.1. Initial Data Health Check</h2>
</div>

Before any deep dive, ensuring the data's integrity was crucial. The **`Initial Analysis.sql`** script acted as our data auditor, meticulously checking for common pitfalls like missing entries, zero values in critical financial columns, and inconsistencies that could skew our results.

## 🔑 Key Actions & Questions:   
- **Identifying invalid entries:** Are there sales, purchase, or pricing records with missing or zero dollar/price amounts?
- **Assessing completeness:** What percentage of our data might be incomplete or erroneous?
- **Validating derived values:** Do calculated values (e.g., `PurchasePrice * Quantity`) consistently match recorded totals, or are there unexpected variances?
- **Cross-table consistency:** Are vendor records consistent across purchasing and sales datasets?

## 🔍 A glimpse into the Code:
### a. Missing or Zero values
**📦 Purchases:**
```sql
SELECT * FROM PurchasesDec WHERE Dollars <= 0 OR Dollars IS NULL;
```

*Sample Output:*

<div class="table-wrapper" markdown="block">

| InventoryId            | Store | Brand | ... | VendorNumber  | VendorName         | PONumber | PODate     | ReceivingDate  | InvoiceDate  | PayDate     | PurchasePrice  | Quantity | Dollars |
|------------------------|-------|-------|-----|---------------|--------------------|----------|------------|----------------|--------------|-------------|----------------|----------|---------|
| 59_CLAETHORPES_2166    | 59    | 2166  | ... | 2561          | EDRINGTON AMERICAS | 11462    | 2016-08-02 | 2016-08-10     | 2016-08-22   | 2016-10-01  | 0              | 12       | 0       |
| 38_GOULCREST_2166      | 38    | 2166  | ... | 2561          | EDRINGTON AMERICAS | 11462    | 2016-08-02 | 2016-08-11     | 2016-08-22   | 2016-10-01  | 0              | 12       | 0       |
| 34_PITMERDEN_2166      | 34    | 2166  | ... | 2561          | EDRINGTON AMERICAS | 11462    | 2016-08-02 | 2016-08-09     | 2016-08-22   | 2016-10-01  | 0              | 12       | 0       |
| 44_PORTHCRAWL_2166     | 44    | 2166  | ... | 2561          | EDRINGTON AMERICAS | 11462    | 2016-08-02 | 2016-08-08     | 2016-08-22   | 2016-10-01  | 0              | 12       | 0       |
| 56_BEGGAR'S HOLE_2166  | 56    | 2166  | ... | 2561          | EDRINGTON AMERICAS | 11462    | 2016-08-02 | 2016-08-09     | 2016-08-22   | 2016-10-01  | 0              | 12       | 0       |


</div>

This query returned 153 entries where the **`Dollars`** value is zero or null. Given that `Dollars` is calculated as `PurchasePrice * Quantity`, this directly implies that **`PurchasePrice`** for these entries is also zero, requiring further investigation. Potential reasons for these entries include:
- **Promotional or Free Goods:** Items given away as part of a promotion, marketing campaign, or bundled with other purchases.
- **Samples:** Products recorded as samples for in-store use or customer trials.
- **Data Entry Errors:** Mistakes made during data input.

**📦 Sales:**
```sql
SELECT * FROM SalesDec WHERE SalesDollars <= 0 OR SalesDollars IS NULL;
```

*Sample Output:*

<div class="table-wrapper" markdown="block">

| InventoryId            | Store | Brand | ... | SalesQuantity | SalesDollars | SalesPrice    | SalesDate  | Classification | ExciseTax  | VendorNo  | VendorName                  |
|------------------------|-------|-------|-----|----------------|---------------|-------------|------------|----------------|------------|-----------|-----------------------------|
| 38_GOULCREST_25340     | 38    | 25340 | ... | 3              | 0             | 0           | 2016-02-13 | 2              | 0.34       | 4425      | MARTIGNETTI COMPANIES       |
| 66_EANVERNESS_25340    | 66    | 25340 | ... | 3              | 0             | 0           | 2016-02-12 | 2              | 0.34       | 4425      | MARTIGNETTI COMPANIES       |
| 66_EANVERNESS_25340    | 66    | 25340 | ... | 1              | 0             | 0           | 2016-02-16 | 2              | 0.11       | 4425      | MARTIGNETTI COMPANIES       |
| 67_EANVERNESS_25340    | 67    | 25340 | ... | 12             | 0             | 0           | 2016-02-07 | 2              | 1.35       | 4425      | MARTIGNETTI COMPANIES       |
| 73_DONCASTER_25340     | 73    | 25340 | ... | 1              | 0             | 0           | 2016-02-15 | 2              | 0.11       | 4425      | MARTIGNETTI COMPANIES       |

</div>

The analysis revealed 55 entries where the **`SalesDollars`** field is zero or null. Since `SalesDollars` is derived from `SalesPrice` multiplied by `SalesQuantity`, a zero `SalesDollars` value means that the **`SalesPrice`** for these transactions is effectively zero as well. This warrants further investigation.

#### ➡️ Next steps:
To determine if these zero values are problematic, we need to:
- **Understand the business context:** Consult relevant teams (purchasing, sales, accounting, inventory) to confirm if zero-value transactions are expected and why.
- **Analyze items and vendors:** Look for patterns tied to specific products or suppliers.
- **Review promotions and pricing strategies:** Check for campaigns like "buy one, get one free" that may explain the values.
- **Examine data entry and system integration:** Investigate potential input errors or issues during data transfers.

### b. Percentage of Zero or Null in the dataset
To assess the cleanliness of the financial data, I calculated the percentage of zero or null values in the `Dollars` column of the `PurchasesDec` table, and the `SalesDollars` column of the `SalesDec` table.

```sql
SELECT
    CAST(SUM(CASE WHEN Dollars <= 0 OR Dollars IS NULL THEN 1 ELSE 0 END) AS REAL) * 100 / COUNT(*) AS ZeroPurchases
FROM PurchasesDec;
```
*Output:* `0.0064`

```sql
SELECT
    CAST(SUM(CASE WHEN SalesDollars <= 0 OR SalesDollars IS NULL THEN 1 ELSE 0 END) AS REAL) * 100 / COUNT(*) AS ZeroSales
FROM SalesDec;

```
*Output:* `0.0004`

➡️ These extremely low percentages in both the `Dollars` and `SalesDollars` columns indicate that our datasets are remarkably clean regarding zero or null monetary values. This is a positive sign for data quality.

### c. Dataset Summaries
This section summarizes the key characteristics of the datasets to gain a foundational understanding of their contents.

**📦 Purchases:**   
The `PurchasesDec` table contains 2.37 million rows, involving 126 distinct vendors and 5,543 unique purchase orders. Monetary and quantity data for purchases are as follows:

| Metric   | Quantity (units) | Dollars         |
|----------|------------------|-----------------|
| Total    | 33,584,377       | $321,900,765.50 |
| Average  | 14.16            | $135.68         |
| Minimum  | 1                | $0.00           |
| Maximum  | 3,816            | $50,175.70      |

The purchase data spans:

| Date Type      | Start Date | End Date   |
|----------------|------------|------------|
| PO Date        | 2015-12-20 | 2016-12-23 |
| Receiving Date | 2016-01-01 | 2016-12-31 |
| Invoice Date   | 2016-01-04 | 2017-01-10 |
| Pay Date       | 2016-02-04 | 2017-02-19 |

**📦 Sales:**   
The `SalesDec` table shows a total sales volume of $452,062,952, with an average sale amount of $35.25. Individual sales range from $0 to $26,061.14.

**📦 Vendors:**   
The `VendorInvoicesDec` table shares similar date ranges with `PurchasesDec` for PO, Invoice, and Pay dates.

| Metric   | Quantity (units) | Dollars         | Freight       |
|----------|------------------|-----------------|---------------|
| Total    | 33,584,377       | $321,900,765.50 | $1,640,474.69 |
| Average  | 6,058.88         | $58,073.38      | $295.95       |
| Minimum  | 1                | $4.14           | $0.02         |
| Maximum  | 141,660          | $1,660,435.88   | $8,468.22     |


<!-------- ** 2.2. Vendor Performance Analysis ** -------->

<div style="text-align: left;">
  <h2 id="2-2-vendor" style="font-weight: bold;">2.2. Vendor Performance Analysis</h2>
</div>

The next step was to understand Bibitor's important relationships with its vendors, or suppliers. The **`Vendor Analysis.sql`** script provided a 360-degree view of supplier performance, aiming to find out which vendors were performing best, how efficient shipping costs were, and how much profit each vendor's products brought in.


## 🔑 Key Actions & Questions:   
- **Top Vendor identification:** Which are the top suppliers by total spend, sales generated from their products, and quantity purchased?
- **Freight cost insights:** Which vendors contribute most to shipping costs, and how does freight impact the overall purchase cost from their goods?
- **Profitability assessment:** What is the gross margin achieved from products supplied by each vendor, highlighting their true profit contribution?
- **Temporal trends:** How do monthly purchase and sales trends look over time, indicating seasonality or growth?

## 🔍 A glimpse into the Code:  
To begin, a comprehensive list of all distinct vendors across both purchase and invoice records was compiled. A total of **128 unique vendors** were identified.

### a. Top Vendors by Spend & Revenue:
It's crucial to know where the most money is spent and which vendors' products bring in the most sales. The following query helps identify Bibitor's top suppliers based on how much was spent on their products:

```sql
-- Identifies top 5 suppliers by total spending (Dollars)
SELECT
    VendorNumber,
    VendorName,
    SUM(Dollars) AS TotalPurchaseDollars
FROM PurchasesDec
GROUP BY VendorNumber, VendorName
ORDER BY TotalPurchaseDollars DESC
LIMIT 5;
```

*Output 1:*

| VendorNumber | VendorName               | TotalPurchaseDollars |
|--------------|---------------------------|-----------------------|
| 3960         | DIAGEO NORTH AMERICA INC  | $50,959,796.85        |
| 4425         | MARTIGNETTI COMPANIES     | $27,861,690.02        |
| 12546        | JIM BEAM BRANDS COMPANY   | $24,203,151.05        |
| 17035        | PERNOD RICARD USA         | $24,124,091.56        |
| 480          | BACARDI USA INC           | $17,624,378.72        |

Similarly, the analysis also identified the top suppliers by the total revenue generated from their products:
```sql
-- Identifies top 5 suppliers by total revenue (SalesDollars)
SELECT 
  VendorNo AS VendorNumber,
  VendorName,
  SUM(SalesDollars) AS TotalSalesDollars
FROM SalesDec
GROUP BY VendorNo, VendorName
ORDER BY TotalSalesDollars DESC
LIMIT 5;
```

*Output 2:*

| VendorNumber | VendorName               | TotalSalesDollars   |
|--------------|---------------------------|----------------------|
| 3960         | DIAGEO NORTH AMERICA INC  | $68,742,416.99       |
| 4425         | MARTIGNETTI COMPANIES     | $41,047,306.30       |
| 17035        | PERNOD RICARD USA         | $32,281,247.95       |
| 12546        | JIM BEAM BRANDS COMPANY   | $31,906,320.54       |
| 480          | BACARDI USA INC           | $25,014,556.89       |

Both results revealed a similar ranking of top vendors. "DIAGEO NORTH AMERICA INC" consistently appeared as the largest supplier both in terms of total purchases and sales generated from their products. This means what Bibitor buys from them lines up well with what customers want to buy.

### b. Freight Cost Efficiency:
While higher purchase amounts often mean higher total shipping costs, it's more insightful to look at shipping costs as a percentage of the total purchase cost. This helps uncover if shipping is costing too much compared to the value of the goods.

```sql
-- Calculates and ranks vendors by freight cost as a percentage of their total purchase cost
SELECT
    VendorNumber,
    VendorName,
    SUM(Dollars) AS TotalPurchase,
    SUM(Freight) AS TotalFreight,
    ROUND(SUM(Freight) * 100.0 / NULLIF(SUM(Dollars), 0), 2) AS FreightPercent
FROM VendorInvoicesDec
GROUP BY VendorNumber, VendorName
ORDER BY FreightPercent DESC
LIMIT 5;
```

*Output:*

| VendorNumber | VendorName                      | TotalPurchase   | TotalFreight   | FreightPercent |
|--------------|----------------------------------|------------------|----------------|----------------|
| 9625         | WESTERN SPIRITS BEVERAGE CO     | $361,249.21      | $1,933.19      | 0.54%          |
| 28776        | TALL SHIP DISTILLERY LLC        | $48,445.58       | $259.90        | 0.54%          |
| 3951         | HIGHLAND WINE MERCHANTS LLC     | $5,500.32        | $29.43         | 0.54%          |
| 1590         | DIAGEO CHATEAU ESTATE WINES     | $1,365,472.83    | $7,259.75      | 0.53%          |
| 9744         | FREDERICK WILDMAN & SONS        | $759,449.24      | $3,999.93      | 0.53%          |

The result showed that vendors with the highest *percentage* of freight costs are often not the same as those with the highest *total* freight. This suggests that smaller or more specialized vendors may have less optimized shipping logistics, making freight a larger proportion of the overall cost for their products.


### c. Profitability via Gross Margin:  
A very important financial measure is gross margin by vendor. This helps identify which suppliers contribute the most to Bibitor's profit.

```sql
-- Calculates the Gross Margin (Profit) by comparing Total Cost (Purchases) to Total Revenue (Sales) for each vendor
WITH Purchases AS (
    SELECT VendorNumber, SUM(Dollars) AS TotalCost FROM PurchasesDec WHERE Dollars > 0 GROUP BY VendorNumber
),
Sales AS (
    SELECT VendorNo AS VendorNumber, SUM(SalesDollars) AS TotalRevenue FROM SalesDec GROUP BY VendorNo
)
SELECT
    s.VendorNumber,
    s.TotalRevenue,
    p.TotalCost,
    (s.TotalRevenue - p.TotalCost) AS GrossProfit,
    ROUND((s.TotalRevenue - p.TotalCost) * 100.0 / NULLIF(s.TotalRevenue, 0), 2) AS GrossMarginPercent
FROM Sales s
LEFT JOIN Purchases p ON s.VendorNumber = p.VendorNumber
ORDER BY GrossProfit DESC
LIMIT 5;
```

*Output:*

| VendorNumber | TotalRevenue     | TotalCost        | GrossProfit      | GrossMarginPercent |
|--------------|------------------|------------------|------------------|---------------------|
| 3960         | $68,742,416.99   | $50,959,796.85   | $17,782,620.14   | 25.87%              |
| 4425         | $41,047,306.30   | $27,861,690.02   | $13,185,616.28   | 32.12%              |
| 1392         | $24,469,172.93   | $15,573,917.90   | $8,895,255.03    | 36.35%              |
| 17035        | $32,281,247.95   | $24,124,091.56   | $8,157,156.39    | 25.27%              |
| 12546        | $31,906,320.54   | $24,203,151.05   | $7,703,169.49    | 24.14%              |

This clearly shows which vendors bring in the most profit. While some vendors lead in total profit, others have very strong gross margin percentages, meaning their products are very efficient at generating profit. This information is key for deciding which vendor relationships to focus on for better profits.


<!-------- ** 2.3. Inventory Turnover Analysis ** -------->

<div style="text-align: left;">
  <h2 id="2-3-inventory" style="font-weight: bold;">2.3. Inventory Turnover Analysis</h2>
</div>

Efficient inventory management is critical for any retail business, directly impacting cash flow and profitability. This analysis, conducted using the **`Inventory Analysis.sql`** script, aimed to understand how quickly purchased products are sold and to pinpoint slow-moving items that might be tying up funds and taking up too much storage space.

### a. Calculating "Days to Sell":
The main part of this analysis involved figuring out the "Days to Sell" for each unique item at every store. This number was calculated by finding the difference in days between when an item was first received and when it was first sold. This information was then saved into a new table called `InventorySaleLag` for easy access.

While the full SQL code for creating this detailed table is extensive, the core idea involved bringing together purchase and sales data to compare dates. This allowed for the calculation of how many days each specific item sat in inventory before its first sale.

### b. Identifying Slow-Moving Inventory::
Once the `InventorySaleLag` table was ready, a straightforward query was used to find items considered "slow-moving." For this analysis, an item was flagged as slow-moving if it took longer than 60 days to sell after being received.

```sql
-- Selects inventory items that took longer than 60 days to sell from the calculated data
SELECT
    InventoryId, Store, VendorName, AvgPurchasePrice, AvgSalesPrice,
    TotalPurchased, TotalSold, FirstReceived, FirstSold, DaysToSell
FROM InventorySaleLag
WHERE DaysToSell > 60
ORDER BY DaysToSell DESC
LIMIT 5;
```

*Sample Output:*

<div class="table-wrapper" markdown="block">

| InventoryId         | Store | VendorName            | ...| TotalSold | FirstReceived | FirstSold   | DaysToSell |
|---------------------|-------|-----------------------|---|-----------|---------------|-------------|------------|
| 29_AYLESBURY_42188  | 29    | MOET HENNESSY USA INC | ...| 1         | 2016-01-02    | 2016-12-31  | 364        |
| 29_AYLESBURY_2767   | 29    | DIAGEO NORTH AMERICA INC | ...| 1         | 2016-01-02    | 2016-12-29  | 362        |
| 29_AYLESBURY_8897   | 29    | MOET HENNESSY USA INC | ...| 2         | 2016-01-08    | 2016-12-31  | 358        |
| 5_SUTTON_17967      | 5     | BANFI PRODUCTS CORP   | ...| 1         | 2016-01-02    | 2016-12-22  | 355        |
| 6_GOULCREST_4574    | 6     | REMY COINTREAU USA INC | ...| 1         | 2016-01-04    | 2016-12-22  | 353        |

</div>

This output immediately points to specific items that are staying in stock for very long periods, some for almost a full year! Products that sit for extended times incur costs for storage, risk becoming outdated, and tie up money that could be used elsewhere. Pinpointing these items allows Bibitor to take direct action, such as adjusting future orders, running special sales, or rethinking their prices for these specific products.

<!------------------------------------------------------------------------------>
<!------------------------------ DASHBOARDS  ----------------------------------->
<!------------------------------------------------------------------------------>

<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>
<div style="text-align: left;">
  <h1 id="3-dashboards" style="font-weight: bold;">3. DASHBOARDS</h1>
</div>

Looking at monthly purchases and sales gives important clues about how operations flow and if demand changes with the seasons.
- Monthly purchases generally went up throughout 2016, with a peak in August, which likely means inventory was being built up.
- In contrast, monthly sales grew strongly, with big peaks in July and a huge jump in December, probably due to holiday shopping.  

These trends are vital for matching what's bought with what's expected to be sold.
