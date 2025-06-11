---
layout: post
title: "Inside Retail Operations: A Case Study on Sales, Inventory, and Vendors"
date: 2025-05-28
excerpt: "What does it take to run a successful retail business? It's knowing what sells, how fast inventory moves, and which vendors truly impact your bottom line. "
cover: /assets/images/Cover_Bibitor.png
---

<!----------------- Table of Contents ----------------->
<details>
  <summary><strong>Table of Contents</strong></summary>
  <ul>
    <li><a href="#1-intro">1. Introduction</a></li>
    <li><a href="#2-sql">2. Analysis with SQL</a>
      <ul>
        <li><a href="#2-1-data-health-check">2.1. Initial Data Health Check</a></li>
        <li><a href="#2-2-vendor">2.2. Vendor Performance Analysis</a></li>
        <li><a href="#2-3-inventory">2.3. Inventory Turnover Analysis</a></li>
        <li><a href="#2-4-MAC">2.4. Inventory Valuation: Moving Average Cost (MAC)</a></li>
      </ul>
    </li>
    <li><a href="#3-dashboards">3. Dashboard Visualizations</a></li>
      <ul>
        <li><a href="#3-1-vendor-overview">3.1. Vendor Performance & Financial Overview</a></li>
        <li><a href="#3-2-inventory-impact">3.2 Inventory Efficiency & Product-Level Insights</a></li>
      </ul>
  </ul>
</details>

<!------------------------------------------------------>
<!------------------------ Intro ----------------------->
<!------------------------------------------------------>

<!-- <img src="/assets/images/Cover_Bibitor.png" alt="Liquour Sales" width="800"/> -->
<hr style="width: 40%; border: none; border-top: 1px dashed lightgray; margin: 40px auto;">

<div style="text-align: left;">
  <h1 id="1-intro" style="font-weight: bold;">1. INTRODUCTION</h1>
</div>

What does it take to run a successful liquor business? It’s not just about stocking popular products — it’s about understanding what sells, how fast it moves, and which vendors help or hurt your bottom line.

This case study analyzes data from Bibitor, LLC — a fictional retail chain with 80+ locations and over $450M in annual sales, to uncover patterns patterns in vendor performance, inventory movement, and sales behavior, applying real-world retail concepts.

### 🧾 About the Dataset
The dataset, sourced from the **[HUB of Analytics Education](https://www.hubae.org)**, simulates operational data from a large-scale liquor retailer located in Lincoln, USA, for the month of December 2016. It consists of six key data tables that collectively represent purchasing, inventory, sales, and vendor transactions.
- **Inventory**
  - **`BegInvDec`**: Inventory at the start of December 2016.
  - **`EndInvDec`**: Inventory remaining at the end of December 2016.

- **Purchases**
  - **`PurchasesDec`**: What Bibitor bought from vendors (quantities, total cost, vendor info).
  - **`PricingPurchasesDec`**: Reference prices Bibitor expects from suppliers.

- **Vendor Invoices**
  - **`VendorInvoicesDec`**: The bills Bibitor received from their suppliers (vendors).

- **Sales**
  - **`SalesDec`**: Item-level sales data including price, quantity, and total revenue.

These tables, when combined, allow us to track products from purchase to sale, understand vendor relationships, and monitor financial flows, all essential for optimizing retail operations.

### 🔑 Key Business Questions
- Which vendors provide the most value?
- Are we overstocking or underutilizing inventory?
- How do purchase prices compare to actual sales?
- What’s the average time it takes to sell received stock?

### 🧩 Data Model
Before diving into the code, we first need to understand how all the different pieces of data connect. An *Entity-Relationship Diagram (ERD)* visually represents these connections, providing the logical framework for accurate and efficient analysis. This ensures our data joins are correct and our derived insights are reliable.

The ERD below guided our analysis, showing the relationships between Bibitor's core transactional and master data tables:

<a href="https://dbdiagram.io/d/Bibitor-LLC-6817a73d1ca52373f5661284" target="_blank" rel="noopener noreferrer">
  <img src="/assets/images/DataModel_Bibitor.png" alt="Data Model" width="800"/>
</a>
<br/>

<div style="border: 1px solid #ccc; padding: 15px; margin: 20px 0; border-radius: 5px; text-align: center; transition: box-shadow 0.3s ease-in-out, border-color 0.3s ease-in-out;" class="dashboard-box">
  <strong><a href="https://dbdiagram.io/d/Bibitor-LLC-6817a73d1ca52373f5661284" target="_blank" style="text-decoration: none;">➡️ View Data Model ⬅️</a></strong>
</div>

As shown, tables like **`PurchasesDec`** and **`VendorInvoicesDec`** are linked by a shared key like `VendorNumber`, representing the core of Bibitor's procurement. Table **`SalesDec`** connects through `InventoryId` to track items' journeys from purchase to customer. This structure ensures a cohesive flow for tracing products and understanding financial transactions across the business.


<!--===========================================================================-->
<!-------------------------------**** SQL ****----------------------------------->
<!--===========================================================================-->

<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>

<div style="text-align: left;">
  <h1 id="2-sql" style="font-weight: bold;">2. ANALYSIS WITH SQL</h1>
</div>

SQL was the primary tool used to extract, transform, and conduct the initial layers of analysis on Bibitor’s extensive datasets. Its robust querying capabilities enabled a systematic and granular approach to addressing critical business questions.

All SQL scripts used in this analysis are available in the following GitHub repository:
<div style="border: 1px solid #ccc; padding: 15px; margin: 20px 0; border-radius: 5px; text-align: center; transition: box-shadow 0.3s ease-in-out, border-color 0.3s ease-in-out;" class="dashboard-box">
  <strong><a href="https://github.com/dtbkhanh/Data-Analytics-and-Reports/tree/021a7ac923e6cd4f8919e8d023981034e881d0a0/SQL%20Queries/01.%20Bibitor%20LLC%20Inventory%20Analysis" target="_blank" style="text-decoration: none;">➡️ View SQL Queries ⬅️</a></strong>
</div>

<!------------------------------------------------------>
<!-------- ** 2.1. Initial Data Health Check ** -------->
<!------------------------------------------------------>
<div style="text-align: left;">
  <h2 id="2-1-data-health-check" style="font-weight: bold;">2.1. Initial Data Health Check</h2>
</div>

#### 📜 **SQL Script:** `01. Initial Analysis.sql`

Ensuring data integrity was a crucial first step before deeper analysis. This involved systematically checking for missing values, zero amounts in key financial fields, and inconsistencies that could affect the reliability of the insights.

## 🔑 Key Objectives:  
- Identify any records with missing or zero monetary values in sales, purchases, or pricing data.
- Assess the completeness and overall cleanliness of the dataset.
- Verify that calculated fields (e.g., `PurchasePrice * Quantity`) align with recorded totals.
- Confirm consistency of vendor information across related tables.

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

This query returned 153 records where the `Dollars` value is zero or null. Since `Dollars` is derived from `PurchasePrice * Quantity`, a zero value implies a zero purchase price for these items. Possible explanations include:
- **Promotional or Free Goods:** Items given away as part of a promotion, marketing campaign, or bundled with other purchases.
- **Samples:** Products recorded as samples for in-store use or customer trials.
- **Data Entry Errors:** Mistakes made during data input.

**📦 Sales:**
```sql
SELECT * FROM SalesDec WHERE SalesDollars <= 0 OR SalesDollars IS NULL;
```

*Sample Output:*

<div class="table-wrapper" markdown="block">

| InventoryId            | Store | Brand | ... | SalesQuantity  | SalesDollars  | SalesPrice  | SalesDate  | Classification | ExciseTax  | VendorNo  | VendorName                  |
|------------------------|-------|-------|-----|----------------|---------------|-------------|------------|----------------|------------|-----------|-----------------------------|
| 38_GOULCREST_25340     | 38    | 25340 | ... | 3              | 0             | 0           | 2016-02-13 | 2              | 0.34       | 4425      | MARTIGNETTI COMPANIES       |
| 66_EANVERNESS_25340    | 66    | 25340 | ... | 3              | 0             | 0           | 2016-02-12 | 2              | 0.34       | 4425      | MARTIGNETTI COMPANIES       |
| 66_EANVERNESS_25340    | 66    | 25340 | ... | 1              | 0             | 0           | 2016-02-16 | 2              | 0.11       | 4425      | MARTIGNETTI COMPANIES       |
| 67_EANVERNESS_25340    | 67    | 25340 | ... | 12             | 0             | 0           | 2016-02-07 | 2              | 1.35       | 4425      | MARTIGNETTI COMPANIES       |
| 73_DONCASTER_25340     | 73    | 25340 | ... | 1              | 0             | 0           | 2016-02-15 | 2              | 0.11       | 4425      | MARTIGNETTI COMPANIES       |

</div>

This identified 55 sales records with zero or missing sales amounts, indicating that the sales price was recorded as zero for these transactions.

#### ➡️ Next steps:
To determine if these zero-value entries are valid, further actions include:
- Consulting business teams to confirm if such transactions are expected under specific contexts (e.g., promotions).
- Analyzing patterns by product or vendor to identify systematic issues.
- Reviewing pricing and promotional strategies that may explain zero-dollar transactions.
- Investigating potential data entry or system integration errors.

### b. Percentage of Zero or Null in the dataset
The percentage of zero or null monetary values in the datasets was calculated to evaluate overall data quality:

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

➡️ These very low percentages indicate that the financial data is remarkably clean with respect to zero or missing monetary values — a positive indicator for the quality of subsequent analysis.

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
The `SalesDec` table shows a total sales volume of $452,062,952 with an average sale amount of $35.25. Individual sales range from $0 to $26,061.14.

**📦 Vendors:**   
The `VendorInvoicesDec` table shares similar date ranges with `PurchasesDec` for PO, Invoice, and Pay dates.

| Metric   | Quantity (units) | Dollars         | Freight       |
|----------|------------------|-----------------|---------------|
| Total    | 33,584,377       | $321,900,765.50 | $1,640,474.69 |
| Average  | 6,058.88         | $58,073.38      | $295.95       |
| Minimum  | 1                | $4.14           | $0.02         |
| Maximum  | 141,660          | $1,660,435.88   | $8,468.22     |


<!-------------------------------------------------------->
<!-------- ** 2.2. Vendor Performance Analysis ** -------->
<!-------------------------------------------------------->

<div style="text-align: left;">
  <h2 id="2-2-vendor" style="font-weight: bold;">2.2. Vendor Performance Analysis</h2>
</div>

#### 📜 **SQL Script:** `02. Vendor Analysis.sql`

The next phase of the analysis focused on Bibitor’s key relationships with its vendors and suppliers. This comprehensive evaluation aimed to provide a 360-degree view of vendor performance — identifying top suppliers, assessing shipping cost efficiency, and measuring profitability contributions from each vendor’s products.

## 🔑 Key Objectives:   
- **Top Vendor identification:** Which vendors rank highest by total purchase spend, sales generated, and quantity purchased?
- **Item-level sales performance:** What are the best-selling products supplied by each vendor?
- **Freight cost insights:** How significant are shipping costs relative to purchase value for each vendor?
- **Profitability assessment:** What is the gross margin achieved from products supplied by each vendor, highlighting their true profit contribution?
- **Temporal trends:** How do purchase and sales volumes vary over time, indicating seasonality or growth patterns?

## 🔍 A glimpse into the Code:  
The first step involved compiling a comprehensive list of unique vendors by combining purchase and invoice data, yielding a total of **128 distinct suppliers**.

<!-----------------#-#----------------->
### a. Top Vendors by Spend & Revenue:
<!-----------------#-#----------------->
Understanding where the most capital is invested and which vendors drive sales revenue is critical. The query below ranks suppliers based on total purchase expenditure:
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

Both results showed consistent leaders in both purchase spend and sales revenue. Notably, **DIAGEO NORTH AMERICA INC** emerged as the largest supplier, indicating strong alignment between what Bibitor buys and what customers actually purchase.

<!-----------------#-#----------------->
### b. Top-Selling Products by Vendor:
<!-----------------#-#----------------->
To drill down into product-level insights, the analysis identified the highest-selling inventory item per vendor. This involved aggregating sales quantities and revenues across all items supplied by each vendor and ranking them accordingly.

*Sample Output:*

| VendorNumber | InventoryId          | TotalSold  | TotalSales  |
|--------------|----------------------|------------|-------------|
| 2            | 76_DONCASTER_90609   | 23         | $574.77     |
| 60           | 73_DONCASTER_3979    | 9282       | $158,247.18 |
| 105          | 76_DONCASTER_8412    | 450        | $22,495.50  |
| 200          | 12_LEESIDE_20789     | 76         | $1,367.24   |
| 287          | 65_LUTON_24922       | 20         | $281.80     |

This granular data supports targeted inventory management, promotional planning, and refining the product mix for each vendor.

<!-----------------#-#----------------->
### c. Freight Cost Efficiency:
<!-----------------#-#----------------->
Shipping costs can significantly impact overall product costs. Instead of looking only at total freight expenses, freight was evaluated as a percentage of total purchase cost to identify inefficiencies:

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
|--------------|---------------------------------|-----------------|----------------|----------------|
| 9625         | WESTERN SPIRITS BEVERAGE CO     | $361,249.21     | $1,933.19      | 0.54%          |
| 28776        | TALL SHIP DISTILLERY LLC        | $48,445.58      | $259.90        | 0.54%          |
| 3951         | HIGHLAND WINE MERCHANTS LLC     | $5,500.32       | $29.43         | 0.54%          |
| 1590         | DIAGEO CHATEAU ESTATE WINES     | $1,365,472.83   | $7,259.75      | 0.53%          |
| 9744         | FREDERICK WILDMAN & SONS        | $759,449.24     | $3,999.93      | 0.53%          |

The result showed that vendors with the highest percentage of freight costs often differ from those with the highest total freight. This suggests that smaller or more specialized vendors may have less optimized shipping logistics, making freight a larger proportion of the overall cost for their products.

<!-----------------#-#----------------->
### d. Profitability via Gross Margin:  
<!-----------------#-#----------------->
One of the most important financial measures for evaluating vendors is Gross Margin. This metric compares how much revenue (sales) a vendor generates against the cost of the products purchased from them. It helps Bibitor understand which suppliers are not just efficient but also contribute the most to the company’s overall profitability — showing real dollars earned, not just percentages.

The SQL query below calculates both **Gross Profit** (the dollar amount earned after costs) and **Gross Margin Percentage** (profit as a share of revenue) for each vendor. This helps Bibitor focus on the top-performing suppliers:

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

| VendorNumber | TotalRevenue     | TotalCost        | GrossProfit      | GrossMarginPercent  |
|--------------|------------------|------------------|------------------|---------------------|
| 3960         | $68,742,416.99   | $50,959,796.85   | $17,782,620.14   | 25.87%              |
| 4425         | $41,047,306.30   | $27,861,690.02   | $13,185,616.28   | 32.12%              |
| 1392         | $24,469,172.93   | $15,573,917.90   | $8,895,255.03    | 36.35%              |
| 17035        | $32,281,247.95   | $24,124,091.56   | $8,157,156.39    | 25.27%              |
| 12546        | $31,906,320.54   | $24,203,151.05   | $7,703,169.49    | 24.14%              |

For example, Vendor 3960 has a lower Gross Margin Percentage than Vendor 1392, but because it sells a much larger volume, it contributes the most profit overall.

By looking at both absolute profit (Gross Profit dollars) and efficiency (Gross Margin Percentage), this analysis gives Bibitor a balanced view to guide smart decisions in managing vendor relationships — prioritizing suppliers that maximize profitability and support strong negotiation.


<!-------------------------------------------------------->
<!-------- ** 2.3. Inventory Turnover Analysis ** -------->
<!-------------------------------------------------------->

<div style="text-align: left;">
  <h2 id="2-3-inventory" style="font-weight: bold;">2.3. Inventory Turnover Analysis</h2>
</div>

#### 📜 **SQL Script:** `03. Inventory Turnover Analysis.sql`

Managing inventory efficiently is essential for any retail business because it directly affects cash flow and profits. In this analysis, we focused on understanding how quickly products move from purchase to sale, helping identify items that linger too long on the shelves — which can tie up money and take up valuable storage space.

<!-----------------#-#----------------->
### a. Calculating "Days to Sell":
<!-----------------#-#----------------->
The key metric here is the “Days to Sell” — how many days it takes for an item to go from the moment it arrives in the store to when it’s sold for the first time. To find this, we compared the date the product was received with the date it was sold. This calculation was then stored in a new table called `InventorySaleLag`, making it easy to review later.

While the full SQL script behind this table is detailed, the basic idea is straightforward: combine purchase and sales data to find the time gap between arrival and sale for each product at every store.

<!-----------------#-#----------------->
### b. Identifying Slow-Moving Inventory:
<!-----------------#-#----------------->
With the `InventorySaleLag` data ready, we ran a simple query to flag slow-moving items — those that took more than 60 days to sell after arriving. Identifying these products helps the business take action, like discounting or reevaluating stock levels, to free up cash and space.

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

| InventoryId         | Store | VendorName               | ...| TotalSold | FirstReceived | FirstSold   | DaysToSell |
|---------------------|-------|--------------------------|----|-----------|---------------|-------------|------------|
| 29_AYLESBURY_42188  | 29    | MOET HENNESSY USA INC    | ...| 1         | 2016-01-02    | 2016-12-31  | 364        |
| 29_AYLESBURY_2767   | 29    | DIAGEO NORTH AMERICA INC | ...| 1         | 2016-01-02    | 2016-12-29  | 362        |
| 29_AYLESBURY_8897   | 29    | MOET HENNESSY USA INC    | ...| 2         | 2016-01-08    | 2016-12-31  | 358        |
| 5_SUTTON_17967      | 5     | BANFI PRODUCTS CORP      | ...| 1         | 2016-01-02    | 2016-12-22  | 355        |
| 6_GOULCREST_4574    | 6     | REMY COINTREAU USA INC   | ...| 1         | 2016-01-04    | 2016-12-22  | 353        |

</div>

The result quickly highlights specific products that remain in stock for unusually long periods — some even close to a full year! Items that sit on shelves for too long can increase storage costs, risk becoming outdated or unsellable, and tie up valuable funds that could be better invested elsewhere. By identifying these slow-moving products, Bibitor can take targeted steps such as adjusting future purchase orders, launching special promotions, or revising prices to improve sales and free up resources.

<!--------------------------------------------------------------------------->
<!-------- ** 2.4. Inventory Valuation: Moving Average Cost (MAC) ** -------->
<!--------------------------------------------------------------------------->

<div style="text-align: left;">
  <h2 id="2-4-MAC" style="font-weight: bold;">2.4. Inventory Valuation: Moving Average Cost (MAC)</h2>
</div>

#### 📜 **SQL Script:** `04. Inventory MovingAvgCost.sql`

Knowing the true cost of inventory is just as important as knowing how quickly it sells. Bibitor can estimate this using the Moving Average Cost (MAC) method. This approach continuously updates the average cost of each item whenever new stock is purchased, reflecting the most current value of inventory.

The process combines data on what’s currently in stock, what was purchased, and what was sold — then calculates an up-to-date average cost for every product.

### Calculating MAC:

To determine the Moving Average Cost, we followed a few key steps:
1. **Tracked sales and purchases:** Sales are counted as negative quantities (items leaving inventory), and purchases as positive quantities (items coming in), to accurately represent stock changes.
2. **Combined Transactions:** All inventory movements — both incoming and outgoing — are merged into one dataset for analysis.
3. **Added Beginning Inventory:** The inventory at the beginning of the month is added to provide a complete picture of stock availability.
4. **Calculated Moving Average:** For each product at each store, the total cost of inventory is divided by the total quantity on hand, resulting in a dynamic average cost that adjusts as new purchases and sales happen.
5. **Compared with Ending values:** Finally, the calculated average cost is compared with the recorded value at the end of the period to ensure accuracy.

The goal is to maintain a precise and current average cost for every product, helping Bibitor make informed decisions about pricing, budgeting, and profitability.

```sql
-- Calculate Moving Average Cost (MAC)
SELECT
    InventoryId,
    Store,
    Brand,
    SUM(Quantity) AS Quantity,
    SUM(Price) AS TotalCost,
    (SUM(Price) / NULLIF(SUM(Quantity), 0)) AS MAC
FROM temp.BegInv_andTrans_proc
GROUP BY InventoryId, Store, Brand;
```

*Sample Output:*

<div class="table-wrapper" markdown="block">

| Inventory ID          | Store | City     | Brand  | Description                   | Size      | On Hand  | Price ($) | End Date   | MAC ($)            | Difference ($)       |
|-----------------------|-------|----------|--------|-------------------------------|-----------|----------|-----------|------------|--------------------|----------------------|
| 10_HORNSEY_1001       | 10    | HORNSEY  | 1001   | Baileys 50mL 4 Pack           | 50mL 4 Pk | 0        | 5.99      | 2016-12-31 | 0.5445             | 5.4455               |
| 10_HORNSEY_1003       | 10    | HORNSEY  | 1003   | Crown Royal VAP Glass+Coaster | 750mL     | 73       | 22.99     | 2016-12-31 | 3.1519             | 19.8381              |
| 10_HORNSEY_10058      | 10    | HORNSEY  | 10058  | F Coppola Dmd Ivry Cab Svgn   | 750mL     | 24       | 14.99     | 2016-12-31 | 0.5915             | 14.3985              |
| 10_HORNSEY_10062      | 10    | HORNSEY  | 10062  | B de Beauchene CDR Rouge      | 750mL     | 15       | 8.99      | 2016-12-31 | 0.8173             | 8.1727               |
| 10_HORNSEY_10164      | 10    | HORNSEY  | 10164  | Andre Bourgogne Pnt Nr RSV    | 750mL     | 19       | 15.99     | 2016-12-31 | 1.4536             | 14.5364              |

</div>

<!--===========================================================================-->
<!--------------------------***** DASHBOARDS *****------------------------------->
<!--===========================================================================-->

<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>
<div style="text-align: left;">
  <h1 id="3-dashboards" style="font-weight: bold;">3. DASHBOARD VISUALIZATIONS</h1>
</div>

<div style="border: 1px solid #ccc; padding: 15px; margin: 20px 0; border-radius: 5px; text-align: center; transition: box-shadow 0.3s ease-in-out, border-color 0.3s ease-in-out;" class="dashboard-box">
  <strong><a href="https://lookerstudio.google.com/reporting/85a4eec4-8ecb-48e9-babd-d3117a5b6580" target="_blank" style="text-decoration: none;">➡️ View Live Dashboards ⬅️</a></strong>
</div>


<!------------------------------------------------------>
<!------------- ** 3.1. Vendor Overview ** ------------->
<!------------------------------------------------------>
<div style="text-align: left;">
  <h2 id="3-1-vendor-overview" style="font-weight: bold;">3.1. Vendor Performance & Financial Overview</h2>
</div>

<!-----------------#-#----------------->
### a. Understanding Business Flow
<!-----------------#-#----------------->
<img src="/assets/images/Screenshot_Bibitor_01_Timeline.png" alt="Overview Dashboard Screenshot" width="800"/>

Monthly trends in purchases and sales reveal key patterns in Bibitor’s business flow. These insights support smarter inventory planning and financial forecasting:

- Purchases steadily increased through 2016, peaking in August, which likely means inventory was being built up.
- Sales showed sharper growth, particularly in July and December, indicating strong seasonality, likely tied to summer and holiday demand.

Understanding these rhythms helps ensure the right products are stocked at the right times.

<!-----------------#-#----------------->
### b. Visualizing Vendor Dominance
<!-----------------#-#----------------->
<img src="/assets/images/Screenshot_Bibitor_01_Top.png" alt="Top Vendors Performance" width="800"/>

This section showcases top-performing vendors through key financial metrics: **Purchase Spend**, **Sales Revenue**, and **Gross Profit/Margin**. As noted earlier (<a href="#2-2-vendor">Section 2.2</a>), **DIAGEO NORTH AMERICA INC** consistently ranks highest, clearly standing out across all metrics.

The bar charts visually rank vendor performance, making it easy to compare their contribution to Bibitor’s bottom line. In parallel, the "Top 10 Vendor by Freight % of Purchase" table surfaces shipping efficiency issues — revealing that some smaller vendors may have disproportionate freight costs relative to their order volumes.

<!-----------------#-#----------------->
### c. Vendor Inventory Insights
<!-----------------#-#----------------->
<img src="/assets/images/Screenshot_Bibitor_01_EndingInv.png" alt="Vendor Inventory Insights" width="800"/>

A new dimension of analysis focuses on inventory allocation across vendors:
- **Ending Inventory Value:** The "Top 10 Vendor by Ending Inventory Value ($)" bar chart shows where most of Bibitor’s current stock value is concentrated. Diageo again leads, followed by Martignetti Companies — reflecting both their high purchase volumes and slower turnover.
- **Inventory vs. Purchases:** The scatter plot "Ending Inventory Value vs. Total Purchases" brings an important correlation to light. Vendors with higher purchase totals generally hold more ending inventory. Large bubbles in the upper-right corner (e.g., DIAGEO NORTH AMERICA INC) signal significant capital investment and highlight the need to monitor stock efficiency.

### 📝 Summary
This dashboard turns complex vendor data into actionable insights. By spotlighting top vendors across purchasing, sales, profit, and inventory, Bibitor can prioritize key relationships, assess capital allocation, and refine stock strategies — all crucial for driving sustainable growth.


<!------------------------------------------------------------------------------->
<!---------- ** 3.2. Inventory Efficiency & Product-Level Insights ** ----------->
<!------------------------------------------------------------------------------->
<div style="text-align: left;">
  <h2 id="3-2-inventory-impact" style="font-weight: bold;">3.2. Inventory Efficiency & Product-Level Insights</h2>
</div>

To further support strategic vendor relationships, this dashboard focuses on Bibitor’s inventory health and product flow. It provides clear insights into product movement speed, identifies bottlenecks, and highlights both strong performers and areas needing immediate attention.

<!-----------------#-#----------------->
### a. Highlighting Product Successes
<!-----------------#-#----------------->
<img src="/assets/images/Screenshot_Bibitor_02_TopSelling.png" alt="Top-Selling Product by Vendor" width="800"/>

The “Top-Selling Product by Vendor” table shows each vendor’s best-selling product by both quantity and total sales. This highlights specific high-performing items that warrant consistent stocking and potential marketing focus. It complements the overall vendor performance by showing which product contributes most to a vendor's success for Bibitor.

<!-----------------#-#----------------->
### b. Inventory Velocity
<!-----------------#-#----------------->
<img src="/assets/images/Screenshot_Bibitor_02_SaleLag.png" alt="Inventory Velocity" width="800"/>

This section visualizes how quickly products sell after arriving in inventory, based on the “Days to Sell” metric introduced in <a href="#2-3-inventory">Section 2.3</a>.

- **Overall Sales Lag Distribution:** The "Inventory Sales Lag Distribution" chart provides a high-level overview of inventory turnover. It clearly shows that the majority of Bibitor's products sell within a relatively short timeframe (e.g., within 30 days). However, it also visually highlights the presence of a tail — a smaller, but significant, number of products that sit in inventory for extended periods (e.g., 90 days or more), tying up capital and storage space.
- **Identifying Slow Movers:** The accompanying table lists the ten products with the longest sales lag, including product and vendor details. These are ideal candidates for promotions, pricing changes, or stock review.

<!-----------------#-#----------------->
### c. Performance Drivers: By Vendor and By Store
<img src="/assets/images/Screenshot_Bibitor_02_Performance.png" alt="Performance Drivers: By Vendor and By Store" width="800"/>
<!-----------------#-#----------------->
To pinpoint where slow-moving inventory originates:

- **Vendor Performance:** The "Top 10 Vendors by Average Days to Sell" chart reveals which suppliers, on average, are associated with slower inventory turnover. Identifying vendors like TRUETTI HURST and WALPOLE MTN VIEW WINERY with significantly higher average days to sell (119 and 115 days, respectively) can lead to discussions about product assortment, demand alignment, or purchasing quantities with these specific partners.
- **Store Performance:** The "Top 10 Stores by Average Days to Sell" chart highlights locations where inventory tends to linger. Stores such as Store #44 and Store #74 show higher average days to sell (around 36-37 days), indicating potential localized demand issues, merchandising challenges, or inefficiencies in inventory management specific to those branches.

<!-----------------#-#----------------->
### d. Inventory Cost & Valuation
<!-----------------#-#----------------->
<img src="/assets/images/Screenshot_Bibitor_02_MAC.png" alt="Vendor Inventory Insights" width="800"/>

Beyond tracking inventory movement, understanding its true cost is paramount for accurate financial reporting and pricing strategies. This section leverages the Moving Average Cost (MAC) method (introduced in <a href="#2-4-MAC">Section 2.4</a>) to detect cost variances. 

- **Inventory Cost Variance:** The bar chart “Top Products by Inventory Cost Variance” identifies items with the largest gaps between their recorded cost and MAC. Products like 69_MOUNTMEND_20063 and 38_GOULCREST_20063 show notable differences (e.g., $1.83K), signaling potential data errors or unexpected price shifts that warrant investigation to ensure correct inventory valuation.
- **Cost Alignment Check:** The scatter plot “Recorded vs. MAC per Product” visually compares recorded costs to MAC across products. Most products align well (near the diagonal), while outliers indicate inconsistencies that could impact profitability and require review.


<!-----------------#-#----------------->
### 📝 Summary
<!-----------------#-#----------------->
This comprehensive dashboard provides an integrated view of Bibitor's inventory dynamics. It highlights not only product sales velocity, problematic slow-movers, and performance drivers by vendor and store, but also crucial insights into inventory cost accuracy. By visually exposing movement trends, efficiency bottlenecks, and potential valuation discrepancies, this powerful tool empowers Bibitor to optimize inventory levels, refine procurement, ensure financial integrity, and ultimately enhance overall profitability.

<!--===========================================================================-->
<!-------------------------***** FINAL TAKEWAYS *****---------------------------->
<!--===========================================================================-->
<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>
<h1 id="final-takeaways">📌 Final Takeaways</h1>

Through a combination of robust SQL analysis and intuitive interactive dashboards, this case study provided Bibitor with deep, actionable insights into its core operations. By translating complex data into clear visuals, it offers a comprehensive understanding of:
- Vendor performance
- Inventory movement
- Product-level cost accuracy

Key insights such as identifying top-performing and slow-moving products, evaluating vendor efficiency, and highlighting cost variances empower Bibitor to make more informed decisions. Whether it's improving stock turnover, refining purchasing strategies, or ensuring accurate financial reporting, the findings presented here offer a strong foundation for optimizing operations, boosting efficiency, and driving sustainable profitability.

This data-driven approach not only reveals what’s happening — but crucially guides Bibitor on where to take action next.


<!------------------------------------------------------------------------ JavaScript ------------------------------------------------------------------------>
<script>
  const dashboardBoxes = document.querySelectorAll('.dashboard-box');
  dashboardBoxes.forEach((box) => {
    box.addEventListener('mouseenter', () => {
      box.style.boxShadow = '0 4px 8px rgba(0, 0, 0, 0.2)';
      box.style.borderColor = '#3498db';
    });
    box.addEventListener('mouseleave', () => {
      box.style.boxShadow = 'none';
      box.style.borderColor = '#ccc';
    });
  });
</script>