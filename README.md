# Sales Performance Analysis Dashboard

An interactive 3-page **Power BI** dashboard that analyzes retail sales, profit, shipping and discounts across customers, regions, categories and time (2018–2021).


## Business Questions

1. How are sales and profit trending year over year?
2. Which categories, regions and states drive the most revenue and profit?
3. Who are the top customers, products and sub-categories?
4. How do shipping modes affect order volume and profit?
5. Where is discounting concentrated, and how does it relate to profit?
6. Are we on track to hit the profit target?


## Dashboard Pages

### 1. Overview
High-level KPIs and performance trends.

![Overview page](screenshots/Overview.png)

- **KPI cards:** total sales, total profit, profit margin and customer count
- **Total sales and profit by order year** (combo chart)
- **Sales by category**, **profit by ship mode**, **profit by region**
- **Sales by region map**
- **Profit target achievement** gauge against a 300K target
- Slicers: Order Year, Month Name, Region, Segment

### 2. Sales & Profit
Product, state and customer performance.

![Sales and Profit page](screenshots/Sales%20and%20Profit.png)

- Top 5 products by sales
- Top 5 sub-categories by profit
- Top 5 and bottom 5 states by sales
- Top 10 customers by profit (sales and profit side by side)

### 3. Ship & Discount
Shipping behavior and discount patterns.

![Ship and Discount page](screenshots/Ship%20and%20Discount.png)

- Orders by ship mode
- Ship days by ship mode
- Number of orders by year
- Discount by category
- Top 5 sub-categories by discount, with profit


## Key Insights

Based on the full dataset (all filters cleared):

- **Total sales of about $2.30M** and **total profit of about $286K**, a profit margin of roughly **12.5%**.
- **Profit grew from about $50K (2018) to about $93K (2021)**, and the number of orders grew from **1,993 to 3,312** over the same period.
- **Technology** has the largest share of sales (36.4%), ahead of Furniture (32.3%) and Office Supplies (31.3%).
- **West ($98K) and East ($95K)** generate the most profit. **South ($30K)** is the weakest region.
- **Standard Class** shipping accounts for about 60% of orders and 57% of profit.
- Profit reached **286.36K against a 300K target**, about 95% of target.
- **Office Supplies** receives the most discounting (948 total discount units), well ahead of Furniture (369) and Technology (244). **Binders** have the highest total discount among the top 5 sub-categories.



## Data Model

Star-style model with one dimension table and one fact table.

| Table | Rows | Description |
|---|---|---|
| `Customer Name` (dimension) | 793 | Customer ID, name, segment, country, city, state, postal code, region |
| `Orders` (fact) | 9,993 | Order and ship dates, ship mode, product, category, sub-category, sales, quantity, discount, profit |

**Relationship:** `Orders[Customer ID]` → `Customer Name[Customer ID]` (many-to-one, single direction).

**Calculated fields:**
- `Order Year`, `Order Month Name` (from Order Date)
- `Ship Days` = Ship Date − Order Date
- `Profit Margin` = Profit / Sales
- `Target` = 300,000 (used for the profit target gauge)


## Data Preparation (Power Query)

- Loaded `Orders` and `Customer Name` sheets from an Excel workbook
- Promoted headers and set correct data types (dates, numbers, text)
- Removed blank rows
- Standardized region labels (for example `W` → `West`)
- Added Order Year, Ship Days and Profit Margin columns



## Tools

- **Power BI Desktop** (data modeling, DAX, report design)
- **Power Query** (data cleaning and transformation)
- **Excel** (source data)



*Note: the dataset is a sample retail dataset used for learning and portfolio purposes.*
