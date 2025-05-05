[RETENTION ANALYSIS (improved).csv](https://github.com/user-attachments/files/20042734/RETENTION.ANALYSIS.improved.csv)[PAYMET STATUS ANALYSIS(with month).csv](https://github.com/user-attachments/files/20042619/PAYMET.STATUS.ANALYSIS.with.month.csv)[PAYMENT_ANALYSIS_METHOD.csv](https://github.com/user-attachments/files/20042550/PAYMENT_ANALYSIS_METHOD.csv)[PAYMENT_ANALYSIS_STATUS.csv](https://github.com/user-attachments/files/20042398/PAYMENT_ANALYSIS_STATUS.csv)[CUSTOMER ANALYSIS(by month and year).csv](https://github.com/user-attachments/files/20042315/CUSTOMER.ANALYSIS.by.month.and.year.csv)[CUSTOMER ANALYSIS(repeat VS non-repeat).csv](https://github.com/user-attachments/files/20041906/CUSTOMER.ANALYSIS.repeat.VS.non-repeat.csv)[ORDER AND SALES ANALYSIS (IMPROVED).csv](https://github.com/user-attachments/files/20041622/ORDER.AND.SALES.ANALYSIS.IMPROVED.csv)# ALT MOBILITY DATA ANALYSIS
In this project i had created a Dashboard of alt mobility using PowerBI and SQL .


### Dashboard Link : https://1drv.ms/u/c/df29bfb6512c5c25/EVXSLUvmS6VOr-BKrIzzMcQB_T77d4Ay9I4vUV4BUX_BTA?e=ydvLmP

## Overview
This project analyzes Alt Mobility's customer orders, payments, and retention using SQL and visual dashboards.

## Problem Statement

Alt Mobility seeks to gain better insights into its order processing, customer retention, and payment performance. The company lacks visibility into how effectively orders are fulfilled, which customers are returning, and where payment issues are occurring. This Power BI dashboard is designed to analyze order trends, track customer behavior over time, and monitor payment success vs. failure. The goal is to support data-driven decisions that improve customer retention, optimize order operations, and reduce revenue loss from failed payments.

### SQL Analysis
- **Order Analysis**: Tracked order volumes and sales by status,month and year.

-- MONTHLY, WEEKLY and YEARLY sales chart  
SELECT  
  DATE_FORMAT(order_date, '%M ') AS month,  
  DATE_FORMAT(order_date, '%W') AS week,  
  DATE_FORMAT(order_date, '%Y') as year,  
  order_date,  
  order_status,  
  COUNT(order_id) AS total_orders,  
  SUM(order_amount) AS total_order_amount  
FROM customer_orders  
GROUP BY  
  DATE_FORMAT(order_date, '%M '),DATE_FORMAT(order_date, '%W'),DATE_FORMAT(order_date, '%Y'),  
  order_status, order_date  
ORDER BY  order_status,order_date;  

[Uploading ORDER AND SALES ANALYSIS (IMPROVED).csv…]()



- **Customer Insights**: Identified repeat vs. one-time customers, segmented by spend/order count.

-- Repeat vs. new customers  
SELECT   
  customer_id,  
  COUNT(*) AS total_orders,  
   CASE  
    WHEN COUNT(*) = 1 THEN 'One-Time Customer'  
    ELSE 'Repeat Customer'  
  END AS customer_type,  
  SUM(order_amount) AS total_order_amount,  
  AVG(order_amount) AS avg_order_amount  
FROM customer_orders  
GROUP BY customer_id  
ORDER BY total_orders DESC;  

[Uploading CUSTOMER ANALYSIS(repeat VS non-repeat).csv…]()

-- Total orders and order amount within a month  
SELECT  
  customer_id,  
  DATE_FORMAT(order_date, '%M') AS order_month,  
  DATE_FORMAT(order_date, '%Y') AS order_year,  
  COUNT(*) AS total_orders,  
  SUM(order_amount) AS total_order_amount  
FROM customer_orders  
GROUP BY customer_id, DATE_FORMAT(order_date, '%M'),DATE_FORMAT(order_date, '%Y')  
ORDER BY customer_id;  

[Uploading CUSTOMER ANALYSIS(by month and year).csv…]()


- **Payment Insights**: Investigated success vs. failure rates by method and time.

-- Payment status  
SELECT  
  payment_status,  
  COUNT(*) AS payment_count, 
  ROUND(COUNT(*) * 100.0 / SUM(COUNT(*)) OVER (), 2) AS percentage  
FROM payments  
GROUP BY payment_status;  

  [Uploading PAYMENT_ANALYSIS_STATUS.csv…]()

-- Payment method with failure count  
SELECT  
  payment_method,  
  COUNT(*) AS total_attempts,  
  SUM(CASE WHEN payment_status = 'Failed' THEN 1 ELSE 0 END) AS failed_count,  
  ROUND(SUM(CASE WHEN payment_status = 'Failed' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS failure_rate_percent  
FROM payments  
GROUP BY payment_method  
ORDER BY failure_rate_percent DESC;  

[Uploading PAYMENT_ANALYSIS_METHOD.csv…]()

-- Payment status with customer type by month and year  
WITH customer_type_cte AS (  
  SELECT  
    customer_id,  
    CASE  
      WHEN COUNT(*) = 1 THEN 'One-Time Customer'  
      ELSE 'Repeat Customer'  
    END AS customer_type  
  FROM customer_orders  
  GROUP BY customer_id  
)  

SELECT  
  o.order_id,  
  o.customer_id,  
  c.customer_type,  
  o.order_date,  
  DATE_FORMAT(o.order_date, '%M') AS order_month,  
  DATE_FORMAT(o.order_date, '%Y') AS order_year,  
  o.order_status,  
  o.order_amount,  
  p.payment_id,  
  p.payment_method,  
  p.payment_status,  
  p.payment_date,  

  CASE   
    WHEN p.payment_status = 'Success' THEN ' Success'  
    WHEN p.payment_status = 'Failed' THEN ' Failed'  
    ELSE ' Pending'  
  END AS payment_outcome_label  
FROM customer_orders o  
LEFT JOIN payments p ON o.order_id = p.order_id  
LEFT JOIN customer_type_cte c ON o.customer_id = c.customer_id  
ORDER BY o.order_date DESC;  

[Uploading PAYMET STATUS ANALYSIS(with month).csv…]()


- **Order Details Report**:  Joins the orders, payments, and customers tables and includes relevant metrics like order total, payment status, customer name, and order date.

-- ORDER DETAILS REPORT  
SELECT  
  o.order_id,  
  o.order_date,  
  o.order_amount,  
  o.order_status,  
  o.customer_id,  
  p.payment_id,  
  p.payment_status,  
  p.payment_method,  
  p.payment_date  
FROM customer_orders o  
JOIN payments p ON o.order_id = p.order_id  
ORDER BY o.order_date DESC;  

[ORDER DETAILS REPORT(improved).csv](https://github.com/user-attachments/files/20042739/ORDER.DETAILS.REPORT.improved.csv)


- **Customer Retention Analysis**:  Calculated retention % of customer cohorts across months.

-- Customer Retention Analysis:  
-- Step 1: Find the first order month for each customer  
WITH first_orders AS (  
  SELECT  
    customer_id,  
    DATE_FORMAT(MIN(order_date), '%Y-%M') AS cohort_month  
  FROM customer_orders  
  GROUP BY customer_id  
),  

-- Step 2: Assign cohort to each order and calculate months since cohort  
orders_with_cohort AS (  
  SELECT  
    o.customer_id,  
    DATE_FORMAT(o.order_date, '%Y-%M') AS order_month,  
    f.cohort_month,  
   TIMESTAMPDIFF(MONTH, f.cohort_month, o.order_date) AS month_number  

  FROM customer_orders o  
  JOIN first_orders f ON o.customer_id = f.customer_id  
),  

-- Step 3: Count distinct customers per cohort and month  
cohort_counts AS (  
  SELECT   
    cohort_month,  
    month_number,  
    COUNT(DISTINCT customer_id) AS customers  
  FROM orders_with_cohort  
  GROUP BY cohort_month, month_number  
),  

-- Step 4: Total customers in each cohort  
cohort_sizes AS (  
  SELECT  
    cohort_month,  
    COUNT(DISTINCT customer_id) AS cohort_size  
  FROM first_orders  
  GROUP BY cohort_month  
)  

-- Final Output: Retention percentage  
SELECT   
  c.cohort_month,  
  c.month_number,  
  c.customers,  
  cs.cohort_size,  
  ROUND(100.0 * c.customers / cs.cohort_size, 2) AS retention_rate  
FROM cohort_counts c  
JOIN cohort_sizes cs ON c.cohort_month = cs.cohort_month  
ORDER BY c.cohort_month, c.month_number;  

[Uploading RETENTION ANALYSIS (improved).csv…]()

##POWER BI Analysis

This dashboard will help :

- Monitor Sales Performance : Track total sales .

- Understand Customer Behavior : Analyze customer demographics and purchasing patterns to enhance targeting and personalization.​

The tables are given as to build the POWER BI DASHBOARD :



### Steps followed 

-  Step 1:  Use SQL to extract, clean, and aggregate data from source      tables.
    Queries created for:

     -  Order and Sales Analysis
    -  Payment Status Analysis
    - Customer Segmentation and Retention
    -  Order Details Reporting
    These gives the output as Order counts by status, Monthly sales trends, Retention percentages by cohort and Payment success/failure breakdowns

- Step 2: Import query results into Power BI as tables. Ensure date formats, numerical fields, and relationships are correctly established.

 
- Step 3 : In the report view, under the view tab, theme was selected.

- Step 4 : A Clustured column chart was also added for representing Order_Amount by Month.


- Step 5 : Stacked bar Chart was added to represent Total Retention_percentage and cohort_month by month_number


- Step 6 :  Another Stacked bar Chart was added to represent payment_id by payment_status.
           

- Step 7 : A Clustured column chart was also added for representing Order_count by Month. 

- step 8 : A Donut chart was added to  represent Count of Order_id by Order_status. 




 # Report Snapshot (Power BI DESKTOP)
 

![Screenshot 2025-04-29 230315](https://github.com/user-attachments/assets/e28d6c0f-fdca-400a-9ea2-a24716c656d9)


## Key Insights from SQL Queries

### Order and Sales Analysis:

- Order Volume: Most orders are marked as Completed, indicating a healthy fulfillment pipeline. However, around 10–15% remain pending or failed, highlighting operational delays or customer drop-offs.

- Revenue Trends: Sales are highest during Q2 and Q4, suggesting potential seasonal patterns or effective marketing during these periods.

- Order Status Breakdown: Revenue is almost entirely driven by Completed orders, while Cancelled and Failed statuses contribute no revenue.

### Payment Status Analysis:

- Success Rate: Overall payment success rate is high (above 85%), but a growing number of failures were observed in recent months, which could signal technical issues or failed verifications.

- Payment Method Trends: Certain methods (e.g., "Pay Later" or "Wallet") have a higher failure rate, potentially due to customer error or backend limitations.

- Monthly Failure Trends: Spikes in failures are concentrated in specific months, indicating time-bound technical or customer experience issues.

### Order Details Reporting:

- Combined data from customer_orders, payments, and customers tables revealed:

- High-value customers placing repeat orders.

- Gaps between order date and payment date in some instances.

- Patterns of payment success aligned with specific customer types.

## Observations from Customer Retention Analysis

### Cohort Retention Findings:

- First-Time Buyers: Each monthly cohort has a high volume of new customers, but retention drops significantly after the first month.

- Month 1 Retention: On average, only 40–50% of customers return in the first month following their initial purchase.

- Month 3+ Retention: Falls below 20%, showing limited long-term engagement.

- Best Performing Cohorts: Some cohorts (e.g., January, March) showed higher Month 1 retention, possibly due to promotions or successful onboarding.

### Retention Visualization Insights:

 - line chart clearly show a drop-off trend in customer activity after the initial engagement.

- Most engagement is concentrated within the first 2–3 months, suggesting the need for early re-engagement campaigns.




