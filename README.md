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



