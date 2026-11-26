# Regional Sales Analysis

**Analysis of $1.24 billion in B2B sales (2014 to Feb 2018) across 47 US states, 3 sales channels and 30 products, using Python and Power BI.**

![Python](https://img.shields.io/badge/Python-pandas-blue) ![Power BI](https://img.shields.io/badge/Dashboard-Power%20BI-F2C811) ![Excel](https://img.shields.io/badge/Source-Excel-217346)

---

## 📌 Table of Contents
1. [Business Problem](#-business-problem)
2. [About the Data](#-about-the-data)
3. [Approach and Tools](#-approach-and-tools)
4. [Analysis Results](#-analysis-results)
5. [Power BI Dashboard](#-power-bi-dashboard)
6. [Recommendations](#-recommendations)
7. [Limitations](#-limitations)
8. [Repository Structure](#-repository-structure)

---

## 🎯 Business Problem

A company sells 30 products to 175 business customers through three channels (Wholesale, Distributor and Export) across the United States. Management has sales records but no single view of **where revenue and profit come from** or **whether performance is growing**.

This project answers:

- How have revenue, profit and profit margin changed over time? Is there seasonality?
- Which sales channels, regions and states drive the business, and how profitable is each?
- Which products and customers matter most, and which sell well but earn weak margins?
- How is order value distributed, and does a higher unit price mean a higher margin?
- How did 2017 actual sales compare with the 2017 product budgets?

**Goal:** give leadership a clear, interactive picture of sales performance so they can focus sales, pricing and product decisions.

---

## 🗂 About the Data

**Source:** `Regional_Sales_Dataset.xlsx`, a workbook of six linked sheets.

| Sheet | Content |
|---|---|
| Sales Orders | 64,104 order lines with date, customer, channel, product, delivery region, quantity, unit price, line total and unit cost |
| Customers | 175 business customers |
| Products | 30 products (Product 1 to Product 30) |
| Regions | 994 US cities with state, coordinates, population, households and median income |
| State Regions | Maps each state to a US region (West, South, Midwest, Northeast) |
| 2017 Budgets | Budget by product for 2017 |

**Analysis-ready dataset:** `Regional_Sales_data_EDA_Exported_.csv` (64,104 rows × 21 columns) after joining the sheets and adding calculated fields.

| Group | Fields |
|---|---|
| Order | order_number, order_date, channel, quantity, unit_price |
| Who and what | customer_name, product_name |
| Where | state, state_name, us_region, lat, lon |
| Financials | revenue, cost (per unit), total_cost, profit, profit_margin_pct, budget |
| Time | order_month, order_month_name, order_month_num |

**Calculated fields**

- `revenue` = quantity × unit price
- `total_cost` = quantity × unit cost
- `profit` = revenue − total_cost
- `profit_margin_pct` = profit ÷ revenue × 100

**Data quality checks**

| Check | Result |
|---|---|
| Duplicate rows | None |
| Missing values | Only `budget`, which exists for 2017 orders only (by design) |
| Revenue = quantity × unit price, profit = revenue − total cost | Holds for every row |
| Date range | 1 Jan 2014 to 28 Feb 2018 (2018 is a partial year) |
| Coverage | 175 customers, 30 products, 46 states plus Washington DC |

**Key figures:** Revenue **$1,235,968,899** · Profit **$461,772,560** · Profit margin **37.4%** · Order lines **64,104** · Average order line **$19,281**.

---

## 🛠 Approach and Tools

1. **Excel:** the source workbook with orders and lookup tables (customers, products, regions, budgets).
2. **Python (pandas):** joined the lookup tables to the orders, created revenue, cost, profit, margin and month fields, ran exploratory analysis and exported the analysis-ready CSV.
3. **Power BI:** built a three-page interactive dashboard with DAX measures (Total Revenue, Total Profit, Profit Margin %, Total Orders, Revenue per Order) and slicers for channel, region, month and year.

---

## 📊 Analysis Results

### 1. Revenue and profit over time

| Year | Revenue | Profit | Margin | Order lines |
|---|---|---|---|---|
| 2014 | $297.5M | $111.2M | 37.4% | 15,453 |
| 2015 | $298.4M | $111.9M | 37.5% | 15,473 |
| 2016 | $298.1M | $111.2M | 37.3% | 15,437 |
| 2017 | $293.8M | $109.6M | 37.3% | 15,263 |
| 2018 (Jan-Feb) | $48.1M | $17.9M | 37.1% | 2,478 |



**Insight:** the business is **flat, not growing**. Revenue stayed around $298M a year from 2014 to 2016 and slipped 1.4% in 2017. Margin held steady at about 37% throughout. The Jan-Feb 2018 figure ($48.1M) is in line with the same months of previous years ($45.3M to $48.9M).

### 2. Seasonality



**Insight:** seasonality is **mild**. Using full years only (2014-2017), the average month brings in $22.8M to $25.6M. February is the lowest (it is the shortest month) and May the highest, a spread of only 12% between best and worst month. There is no strong peak season.

### 3. Sales channels

| Channel | Revenue | Share | Profit margin | Order lines |
|---|---|---|---|---|
| Wholesale | $668.2M | 54.1% | 37.0% | 34,596 |
| Distributor | $387.1M | 31.3% | 37.7% | 19,968 |
| Export | $180.6M | 14.6% | 38.0% | 9,540 |



**Insight:** Wholesale is the backbone of the business with more than half of revenue. Export is the smallest channel but has the **highest margin** (38.0%), while Wholesale has the lowest (37.0%). The gaps are small, and the channel mix has not changed over the years.

### 4. Regions and states

| Region | Revenue | Share | Profit margin |
|---|---|---|---|
| West | $372.1M | 30.1% | 37.4% |
| South | $335.1M | 27.1% | 37.3% |
| Midwest | $320.3M | 25.9% | 37.5% |
| Northeast | $208.4M | 16.9% | 37.1% |



| Top 10 states | Revenue | Share | Margin |
|---|---|---|---|
| California | $228.8M | 18.5% | 37.4% |
| Illinois | $111.1M | 9.0% | 37.4% |
| Florida | $90.2M | 7.3% | 37.3% |
| Texas | $84.0M | 6.8% | 37.4% |
| New York | $55.5M | 4.5% | 37.0% |
| Indiana | $54.6M | 4.4% | 37.4% |
| New Jersey | $46.8M | 3.8% | 36.9% |
| Connecticut | $44.3M | 3.6% | 37.3% |
| Michigan | $39.0M | 3.2% | 37.9% |
| Massachusetts | $35.0M | 2.8% | 37.2% |


**Insight:** revenue is **geographically concentrated**. California alone is 18.5% of sales and the top 5 states make up 46%. The five smallest locations (Delaware at $1.2M, Maine, Washington DC, South Dakota and Wyoming at $1.7M) each contribute only about 0.1%. Margins are almost identical across regions, so geography affects *how much* is sold, not how profitable it is. The Northeast is the smallest region despite having the highest average order line ($19,578).

### 5. Products

| Top 10 products | Revenue | Share | Margin |
|---|---|---|---|
| Product 26 | $117.3M | 9.5% | 37.9% |
| Product 25 | $109.5M | 8.9% | 38.0% |
| Product 13 | $78.3M | 6.3% | 36.7% |
| Product 14 | $75.4M | 6.1% | **35.7%** |
| Product 5 | $70.8M | 5.7% | 37.5% |
| Product 15 | $67.3M | 5.4% | 36.8% |
| Product 2 | $57.4M | 4.6% | **35.8%** |
| Product 4 | $56.7M | 4.6% | 37.6% |
| Product 1 | $56.0M | 4.5% | 38.3% |
| Product 3 | $51.8M | 4.2% | 36.8% |




**Insight:**
- The top 2 products bring in 18.3% of revenue and the top 10 bring in 59.9%.
- Margins range from **34.4% (Product 12)** to **40.0% (Product 9)**.
- **Products 14 and 2 are big sellers with below-average margins** (35.7% and 35.8% against a 37.4% average). They are the clearest candidates for a pricing or cost review.
- The highest-margin products (Products 9, 30, 28, 7 and 21) are all small sellers, each under 2% of revenue, so there is room to grow them.

### 6. Customers

- 175 customers, each ordering in every year, with an average of **$7.1M** in revenue per customer.
- Revenue is **not dependent on a few accounts**: the top 10 customers are only 8.8% of revenue.
- Top 5: Aibox Company ($12.6M), State Ltd ($12.2M), Pixoboo Corp ($11.0M), Organon Corp ($11.0M), Realbuzz Ltd ($10.8M).
- Bottom 5: BB17 Company ($4.0M), Yodoo Ltd ($4.4M), Mycone Ltd ($4.5M), Voonyx Group ($4.7M), SEINDNI Corp ($4.8M). **Voonyx Group's margin is only 32.8%**, the weakest among them.

### 7. Order value and pricing

| Order line value | Lines | Share |
|---|---|---|
| Under $5K | 7,692 | 12.0% |
| $5K to $10K | 14,322 | 22.3% |
| $10K to $20K | 18,084 | 28.2% |
| $20K to $40K | 17,004 | 26.5% |
| Over $40K | 7,002 | 10.9% |



**Insight:** most order lines fall between $5K and $40K. **Unit price has no relationship with profit margin** (correlation of −0.005), so expensive items are not more profitable per dollar of sales. There is no "high-margin price band" to target.

### 8. 2017 budget vs. actual

Actual 2017 revenue was **$293.8M** against a total product budget of **$62.7M**, which is **+369%**. Every one of the 30 products exceeded its budget, by between 239% and 532%.

**Insight:** a gap this large means the budget figures are not on the same basis as the order data (see Limitations), so they should not be used to judge performance.

---

## 📈 Power BI Dashboard



The dashboard (`Regional_Sales_Analysis_Dashboard.pbix`) has three pages, each with slicers for **channel, region, month and year** and navigation buttons:

| Page | Contents |
|---|---|
| **1. Executive Overview and Trends** | KPI cards (total revenue, total profit, profit margin %, total orders, revenue per order), monthly revenue and profit line charts, unit price vs. margin scatter, order value distribution |
| **2. Product and Channel Performance** | Best-selling products, highest-margin products, revenue vs. profitability by product, donut charts of revenue, profit and margin by channel |
| **3. Geographic and Customer Insights** | Top and bottom 5 states and customers by revenue and margin, revenue and margin by region, profit map by state |

---

## ✅ Recommendations

1. **Look for growth, not just efficiency.** Revenue has been flat for four years and dipped in 2017. Set growth targets and review what is limiting it: new customers (the customer count has been fixed at 175) and new regions.
2. **Review pricing and costs on Products 14 and 2.** They are among the largest sellers but earn about 1.6 to 1.7 points less margin than average. Lifting them to the 37.4% average would add profit without needing more sales.
3. **Grow the highest-margin products.** Products 9, 30, 28, 7 and 21 earn 38.6% to 40.0% margins but are each under 2% of revenue. Promote them to existing customers through sales bundles.
4. **Reduce reliance on California and a handful of states.** Five states provide 46% of revenue. Protect these accounts, and build presence in under-served areas. The Northeast has the highest average order value but the lowest share of revenue, so more customers there could pay off.
5. **Give the Export channel more attention.** It has the best margin (38.0%) but only 14.6% of revenue. Even a modest increase in share would lift overall profitability.
6. **Review the weakest accounts.** Voonyx Group has a 32.8% margin on $4.7M of revenue. Check whether discounts or product mix explain it.
7. **Plan operations around mild seasonality.** There is no major peak, so staffing and inventory can be planned evenly through the year. February is the one consistently softer month.
8. **Fix the budgeting process.** Rebuild the product budgets on the same basis as actual sales so that variance reporting becomes meaningful.

---

## ⚠️ Limitations

- **Budget data is not comparable.** The 2017 budgets total $62.7M against $293.8M in actual sales, and exist only for 2017. They may be in different units or cover a subset of sales, so no performance conclusions were drawn from them.
- **`order_number` is not a unique ID.** There are 10,684 distinct order numbers across 64,104 rows, each appearing exactly 6 times with the same customer and product but different dates and states. "Total Orders" in this project therefore counts **order lines (rows)**, not distinct order numbers. This should be clarified with the data owner.
- **Partial final year.** 2018 covers only Jan and Feb, so it was excluded from year-on-year comparisons and from the seasonality calculation.
- **Anonymised data.** Products and customers are labelled generically ("Product 26"), so product-level recommendations cannot be tied to real items or categories.
- **Coverage gaps.** Four states (Alaska, Hawaii, Vermont and West Virginia) have no sales, so they do not appear in the analysis.
- **Very uniform data.** Margins, order sizes and channel mix barely change over time or across groups, and each customer appears in every year. The dataset may be simulated, so findings are illustrative rather than a real business diagnosis.
- **Demographic data unused.** The Regions sheet includes population, households and median income, which were not used. Linking them to sales could show whether revenue follows market size.
- **No customer or product attributes.** There is no information on customer size, industry or product category, which limits segmentation.

---

## 📁 Repository Structure

```
├── Regional_Sales_Dataset.xlsx                 # Source workbook (6 sheets)
├── Regional_Sales_data_EDA_Exported_.csv       # Cleaned, analysis-ready data
├── Regional_Sales_Analysis_Dashboard.pbix      # Power BI dashboard
├── images/                                     # Charts and dashboard screenshots
└── README.md
```

