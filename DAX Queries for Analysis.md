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
