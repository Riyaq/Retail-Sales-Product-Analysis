# Data Preparation:
--------------------------------------------------

# Power BI Dashboards:

### Top-Selling Products – Last Quarter : What are the top-selling products by quantity or revenue in the last quarter?
- Cluster Column Chart: X axis- Product_name, Product_id | Y axis- Measure | Filter TOPN
  ```
  Top Products by Units Sold(Quantity Leaders – Last Quarter) =
  CALCULATE(
    SUM(Transactions_append[quantity]),
    DATESINPERIOD(
        'Calendar'[date],
        MAX('Calendar'[date]),  -- reference current date
        -1,                     -- last quarter
        QUARTER
    )
  )
  
  ```
  
  ```
  Revenue Leader - last quarter = 
  CALCULATE( [Total Sales Amount], PREVIOUSQUARTER('Calendar 1'[date]))
  ```
<img width="1243" height="447" alt="Capture1" src="https://github.com/user-attachments/assets/594550a3-467e-4dcf-aa39-5f9272a3e95f" />

### How does purchasing behavior vary by gender, marital status, and income level?
- The company wants to know which customer segments (by gender, marital status, or yearly income) contribute most to sales
```
Total Sales =
SUMX(Transactions, Transactions[Quantity] * RELATED(Products[product_retail_price]))

Total Profit =
SUMX(Transactions, (RELATED(Products[product_retail_price]) - RELATED(Products[product_cost])) * Transactions[Quantity])

Average Order Value =
DIVIDE([Total Sales], COUNTROWS(Transactions))

Purchase Frequency =
DISTINCTCOUNT(Transactions[Transaction_date])
```
<img width="671" height="352" alt="Captureu" src="https://github.com/user-attachments/assets/fbca368a-1808-4b3f-9a31-fbe922425719" />
<br>
**Gender-Based Purchasing Behavior**
<br>
Bar Chart: <br>
X-axis: Customers[Gender]
Y-axis: [Total Sales]
Tooltip: [Average Order Value], [Purchase Frequency]
<br>
Donut Chart: <br>
Values: [Total Sales]
Legend: Customers[Gender]
<br>
**Marital Status Analysis**
<br>
Clustered Column Chart:
X-axis: Customers[Marital_Status]
Y-axis: [Total Sales]
Legend: Customers[Gender]
Tooltip: [Average Order Value], [Purchase Frequency]
Table / Matrix:
Rows: Customers[Marital_Status]
Columns: Customers[Gender]
Values: [Total Sales], [Total Profit], [Purchase Frequency]
