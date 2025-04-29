# ALT MOBILITY DATA ANALYSIS
In this project i had created a Dashboard of alt mobility using PowerBI and SQL .


### Dashboard Link : https://1drv.ms/u/c/df29bfb6512c5c25/EVXSLUvmS6VOr-BKrIzzMcQB_T77d4Ay9I4vUV4BUX_BTA?e=ydvLmP

## Overview
This project analyzes Alt Mobility's customer orders, payments, and retention using SQL and visual dashboards.

## Problem Statement

Alt Mobility seeks to gain better insights into its order processing, customer retention, and payment performance. The company lacks visibility into how effectively orders are fulfilled, which customers are returning, and where payment issues are occurring. This Power BI dashboard is designed to analyze order trends, track customer behavior over time, and monitor payment success vs. failure. The goal is to support data-driven decisions that improve customer retention, optimize order operations, and reduce revenue loss from failed payments.

### SQL Analysis
- **Order Analysis**: Tracked order volumes and sales by status and month.
 
[ORDER_AND_SALES__ANALYSIS.csv](https://github.com/user-attachments/files/19964270/ORDER_AND_SALES__ANALYSIS.csv)
[ORDER_AND_SALES__ANALYSIS.csv](https://github.com/user-attachments/files/19965016/ORDER_AND_SALES__ANALYSIS.csv)

order_status,order_count,total_order_amount

pending, 5069, 1278400.0400000038

delivered, 5057, 1284616.0099999984

shipped, 4874, 1245883.1399999997


[ORDER_AND_SALES__ANALYSIS(WEEKLY).csv](https://github.com/user-attachments/files/19964275/ORDER_AND_SALES__ANALYSIS.WEEKLY.csv)


- **Customer Insights**: Identified repeat vs. one-time customers, segmented by spend/order count.

 [CUSTOMERR_ANALYSIS_1.csv](https://github.com/user-attachments/files/19964097/CUSTOMERR_ANALYSIS_2.csv)

[CUSTOMERR_ANALYSIS1.csv](https://github.com/user-attachments/files/19964111/CUSTOMERR_ANALYSIS1.csv)

- **Payment Insights**: Investigated success vs. failure rates by method and time.
  
[PAYMENT_ANALYSIS_METHOD.csv](https://github.com/user-attachments/files/19964125/PAYMENT_ANALYSIS_METHOD.csv)

[PAYMENT_ANALYSIS_STATUS.csv](https://github.com/user-attachments/files/19964163/PAYMENT_ANALYSIS_STATUS.csv)

[PAYMENT_ANALYSIS_STATUS_COUNT.csv](https://github.com/user-attachments/files/19964175/PAYMENT_ANALYSIS_STATUS_COUNT.csv)

- **Order Details Report**:  Joins the orders, payments, and customers tables and includes relevant metrics like order total, payment status, customer name, and order date.

[sql_details_report.csv](https://github.com/user-attachments/files/19964247/sql_details_report.csv)

- **Customer Retention Analysis**:  Calculated retention % of customer cohorts across months.

[sql_details_report_RE**CuTENTION_ANALYSIS1.csv](https://github.com/user-attachments/files/19965215/sql_details_report_RETENTION_ANALYSIS1.csv)

[RETENTION_ANALYSIS(WEEKLY).csv](https://github.com/user-attachments/files/19965461/RETENTION_ANALYSIS.WEEKLY.csv)


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




