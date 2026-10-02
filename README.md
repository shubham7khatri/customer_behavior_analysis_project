# customer_behavior_analysis_project
An end-to-end data analytics project that explores how 3,900 retail customers shop, which groups drive revenue, and where the business can grow. The workflow covers data cleaning and feature engineering in Python, business analysis in MySQL, and an interactive Power BI dashboard.
![Python](https://img.shields.io/badge/Python-Pandas-3776AB?logo=python&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-SQL-4479A1?logo=mysql&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black)
![License](https://img.shields.io/badge/License-MIT-green)
📊 Dashboard Preview
![Customer Behavior Dashboard](images/dashboard.png)
🎯 Business Questions
Who are our customers, and how do they differ by gender, age and loyalty?
Which product categories and items generate the most revenue?
Do subscribers spend more than non-subscribers?
How do discounts and shipping types relate to spending?
Are repeat buyers more likely to subscribe?
🔄 Workflow
```
Raw CSV  →  Python (clean + engineer)  →  MySQL (10 queries)  →  Power BI (dashboard)
```
1. Data cleaning and feature engineering (Python)
Notebook: `customer_analytics.ipynb`
Step	What was done
Inspect	`info()` and `describe()` showed 3,900 rows, 18 columns and 37 missing Review Ratings
Impute	Missing ratings filled with the median rating of the same category
Rename	Column names converted to `snake_case` for SQL and Power BI
New feature	`age_group`: four quartile groups (Young Adult, Adult, Middle-Aged, Senior) using `pd.qcut`
New feature	`purchase_frequency_days`: text frequency (Weekly, Monthly…) mapped to days
New feature	`customer_segment`: New / Returning / Loyal from previous purchases using `pd.cut`
Drop	`promo_code_used` removed, since it was identical to `discount_applied`
Export	Cleaned data loaded into MySQL table `shop` with SQLAlchemy
2. Business analysis (SQL)
File: `customer_shopping_behavior.sql`
#	Question	Technique
1	Revenue by gender	`GROUP BY`, `SUM`
2	Discount users who spent above average	Subquery
3	Top 5 products by average rating	`AVG`, `ROUND`, `LIMIT`
4	Standard vs Express shipping spend	`IN`, `AVG`
5	Subscribers vs non-subscribers	`COUNT`, `AVG`, `SUM`
6	Top 5 products by discount rate	`CASE WHEN`
7	New / Returning / Loyal customer counts	`CASE WHEN`, `BETWEEN`
8	Top 3 products in each category	CTE, `ROW_NUMBER`, `PARTITION BY`
9	Do repeat buyers subscribe?	Filtering, `GROUP BY`
10	Revenue by age group	`GROUP BY`, `ORDER BY`
3. Visualisation (Power BI)
The dashboard has six KPI cards plus visuals for sales and revenue by category, gender, age group, shipping type, subscription share and customer segment.
🔍 Key Findings
Revenue: $233K total from 3,900 customers, with an average purchase of $59.76.
Clothing leads: $104.26K (about 45% of revenue), followed by Accessories at $74.20K.
Customer mix: 2,652 male vs 1,248 female customers (about 68% / 32%).
Subscriptions: only 27% of customers are subscribed, a clear growth opportunity.
Age groups: revenue is evenly spread, from $55.76K (Senior) to $62.14K (Young Adult).
Shipping: all six shipping types hold 16–17.5% of orders.
Satisfaction: average review rating is 3.75 out of 5.
💡 Recommendations
Promote subscriptions to the 73% of non-subscribers, starting with repeat buyers.
Run targeted campaigns to grow the female customer segment.
Bundle Outerwear and Footwear with Clothing best-sellers.
Reward Loyal customers and nudge New customers toward a second purchase.
```
🚀 How to Run
Clone the repo
```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   cd <repo-name>
   ```
Install dependencies
```bash
   pip install pandas numpy sqlalchemy mysql-connector-python jupyter
   ```
Run the notebook: open `customer_analytics.ipynb`, update the CSV path if needed, and run all cells.
Load into MySQL: in the last notebook cell, set your own MySQL credentials in the connection string. Use environment variables rather than typing a password into the notebook:
```python
   import os
   from sqlalchemy import create_engine
   engine = create_engine(
       f"mysql+mysqlconnector://{os.environ['DB_USER']}:{os.environ['DB_PASS']}@localhost:3306/customer"
   )
   ```
Run the queries: execute `customer_shopping_behavior.sql` in MySQL Workbench or any MySQL client.
Dashboard: connect Power BI to the `shop` table (or the cleaned CSV) to rebuild the visuals.
🧰 Tech Stack
Python (Pandas, NumPy, SQLAlchemy) · Jupyter Notebook · MySQL · Power BI
📂 Dataset
Customer shopping behavior dataset with 3,900 transactions covering demographics, products, payment, shipping, discounts, reviews and purchase history.
Source: [add dataset link here]
👤 Author
Shubham Khatri
shubham7khatri@gmail.com
📄 License
This project is licensed under the MIT License. See the LICENSE file for details.
