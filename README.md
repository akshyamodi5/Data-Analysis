## Project : Sales Insights of Data Analysis-AtliQ Hardware

AtliQ Hardware, a supplier of computer hardware and peripherals across India, is headquartered in Delhi with multiple regional offices. The Sales Director faces challenges in tracking sales amidst a dynamic market and declining overall performance.

Currently, regional managers provide verbal updates on sales figures, lacking data-backed insights. This approach leaves the Sales Director frustrated and unable to make informed decisions.

To address this, the company needs a daily accessible data visualization tool to monitor regional performance and trends accurately. This project aims to create a Power BI-based sales dashboard, enabling data-driven decisions and improving overall business growth.

## Data Discovery :
### Project Planning Using AIMS Grid
#### AIMS Grid Overview

The AIMS Grid is a project management framework comprising four key components:

* **Purpose:** Clearly define the objective of the project.

* **Stakeholders:** Identify the individuals or teams involved.

* **End Result:** Specify the desired outcome.

* **Success Criteria:** Establish measurable benchmarks, such as cost optimization and time efficiency.


 #### AIMS Grid for the Project

**Purpose:** To uncover previously unseen sales insights, support decision-making, and automate processes to reduce manual effort in data gathering.

**Stakeholders:**

* Sales Director  

* Marketing Team

* Customer Service Team

* Data and Analytics Team

* IT Department

**End Result:** Develop an automated dashboard that provides real-time insights to enable data-driven decision-making.

**Success Criteria:**

* A dashboard delivering up-to-date sales order insights.
* Improved decision-making by the sales team, leading to a 10% reduction in total expenses.
* Elimination of manual data gathering, saving 20% of operational time to reinvest in value-added activities.

### Tools Used
* MySQL
* Microsoft Power BI
* Power Query Editor

### Data Analysis Using SQL

1. Show all customer records

    `SELECT * FROM customers;`

 2. Show total number of customers
       `SELECT count(*) FROM customers;`

 3. Show transactions for Chennai market (market code for chennai is Mark001

    `SELECT * FROM transactions where market_code='Mark001';`

 4. Show distrinct product codes that were sold in chennai

    `SELECT distinct product_code FROM transactions where market_code='Mark001';`

 5. Show transactions where currency is US dollars

    `SELECT * from transactions where currency="USD";`

 6. Show transactions in 2020 join by date table

    `SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;`

 7. Show total revenue in year 2020,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";`
	
8. Show total revenue in year 2020, January Month,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");`

 9. Show total revenue in year 2020 in Chennai

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020
and transactions.market_code="Mark001";`

### Power BI Analysis and Dashboard

#### ETL (Extract, Transform, Load) & Data Cleaning - Power Query 
1. The market table has two international markets with no zones allocated. Filtering it out using the dropdown. or Market table -> Home tab -> Transform data -> Transform data 
```
= Table.SelectRows(sales_markets, each ([zone] <> ""))
```
2. The transaction table has a ton of 0 and negative values in the sales_amount column.
```
= Table.SelectRows(sales_transactions, each ([sales_amount] <> -1 and [sales_amount] <> 0))
```
3. Converting USD currency to INR [General currency conversion for now]
Add column -> Conditional column
```
= Table.AddColumn(#"Filtered Rows", "norm_sales_amount", each if [currency] = "USD" or [currency] = "USD#(cr)" then [sales_amount]*83 else [sales_amount])
```

#### Key Measures:
1. Average Sales per Transaction
```
Average Sales per Transaction = DIVIDE(SUM('atliq transactions'[norm_sales_amount]), COUNTROWS('atliq transactions'))
```
2. Profit Margin %
```
Profit Margin % = DIVIDE([Total Profit Margin],[Revenue],0)
```
3. Profit Margin Contribution %
```
Profit Margin Contribution % = DIVIDE([Total Profit Margin],CALCULATE([Total Profit Margin],ALL('atliq products'),ALL('atliq customers'),ALL('atliq markets')))
```
4. Total Revenue
```
Revenue = SUM('sales transactions'[sales_amount])
```
5. Revenue Contribution %
```
Revenue Contribution % = DIVIDE([Revenue],CALCULATE([Revenue],ALL('atliq products'),ALL('atliq customers'),ALL('atliq markets')))
```
6. Total Sales Quantity
```
Sales Quantity = SUM('atliq transactions'[sales_qty])
```
7. Total Profit Margin
```
Total Profit Margin = SUM('atliq transactions'[profit_margin])
```
8. Average Sales Amount per Customer
```
Avg Sales Amt per Customer = DIVIDE(SUM('atliq transactions'[norm_sales_amount]), DISTINCTCOUNT('atliq customers'[customer_code]))
```
9. Total Customer Types
```
Customer Types = DISTINCTCOUNT('atliq customers'[customer_type])
```
10. Total Markets
```
Markets = DISTINCTCOUNT('atliq transactions'[market_code])
```
11. Total Product Types
```
Product Types = DISTINCTCOUNT('atliq products'[product_type])
```
12. Total Customers
```
Unique Customers = DISTINCTCOUNT('atliq transactions'[customer_code])
```

![Image Alt](https://github.com/akshyamodi5/Data-Analysis/blob/2a8c137615d64b96022b8575d5de64818c786d17/Screenshot%202024-12-08%20230309.png)

![Image Alt](https://github.com/akshyamodi5/Data-Analysis/blob/f964f0c83df3f93055030eacd94bf13826b10bdb/Screenshot%202024-12-08%20235709.png)

![Image Alt](https://github.com/akshyamodi5/Data-Analysis/blob/e69ed8124d8d57e2d17111ee200b104d9200bb8e/Screenshot%202024-12-08%20235742.png)

## Insights

1. Over four years, the company generated ₹985M revenue, ₹24.7M profit (2.5% margin), and ₹2M sales. In 2020, revenue was ₹142M with ₹2.1M profit from 350K units sold.

2. Delhi NCR led in revenue with ₹520M (52.8%) but had a low 2.3% profit margin.

3. Bhubaneshwar had the highest 2020 profit margin (10.48%), while Mumbai led in total profit contribution (23.89%).

4. Bengaluru had the lowest profit margin (-20.8%) and profit contribution (-0.3%).

5. Electricalsara Stores was the top customer, generating ₹413M in revenue.

6. "Prod318" was the best-selling product with ₹69M revenue.

7. Distribution and own-brand products each generated ₹494M over four years.

8. Revenue dropped in June 2020, with the lowest profit margin in April 2020.




