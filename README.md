# Alt_moobility

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


This dashboard will help :

- Monitor Sales Performance : Track total sales and profit margins.

- Analyze Product Performance : Identify top-selling products and categories to optimize inventory and marketing strategies.​


- Understand Customer Behavior : Analyze customer demographics and purchasing patterns to enhance targeting and personalization.​




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
 
![Screenshot 2025-04-29 230059](https://github.com/user-attachments/assets/595ccfd5-a558-4f56-a5b9-1e180ddf5aa1)
