Project Overview
This project aims to develop a comprehensive credit card financial dashboard using Power BI. The dashboard provides real-time insights into key performance metrics and trends, enabling stakeholders to monitor and analyze credit card operations effectively.

Project Objective
The objective of this project is to create an interactive and informative dashboard that integrates transaction and customer data from a SQL database. This dashboard allows stakeholders to:

Monitor weekly and yearly revenue trends.
Analyze customer demographics and their contributions to revenue.
Identify key performance metrics and trends.
Key Features
Data Integration: Data is imported from CSV files into SQL, processed, and analyzed using DAX queries in Power BI.
Real-time Insights: The dashboard provides real-time updates on revenue, transaction amounts, and customer counts.
Actionable Insights: Identifies significant trends and contributions from different customer demographics and regions.
Data Processing
Import Data to SQL Database:

Prepare CSV files with transaction and customer data.
Create tables in SQL and import the CSV data.
Data Processing & DAX:

Use DAX queries to create calculated columns and measures for analysis.
Example DAX queries:
DAX
Copy code
AgeGroup = SWITCH(
  TRUE(),
  'public cust_detail'[customer_age] < 30, "20-30",
  'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
  'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
  'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
  'public cust_detail'[customer_age] >= 60, "60+",
  "unknown"
)

IncomeGroup = SWITCH(
  TRUE(),
  'public cust_detail'[income] < 35000, "Low",
  'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] <70000, "Med",
  'public cust_detail'[income] >= 70000, "High",
  "unknown"
)

week_num2 = WEEKNUM('public cc_detail'[week_start_date])

Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]

Current_week_Reveneue = CALCULATE(
  SUM('public cc_detail'[Revenue]),
  FILTER(
    ALL('public cc_detail'),
    'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
  )
) 

Previous_week_Reveneue = CALCULATE(
  SUM('public cc_detail'[Revenue]),
  FILTER(
    ALL('public cc_detail'),
    'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1
  )
)
Insights & Findings
Weekly Overview:

Revenue increased by 28.8% in Week 53 (31st Dec).
Total Transaction Amount and Count showed significant growth.
Customer count increased.
Year-to-Date (YTD) Overview:

Overall revenue: $57M
Total interest earned: $8M
Total transaction amount: $46M
Male customers contributed $31M in revenue; female customers $26M.
Blue and Silver credit cards contributed 93% of overall transactions.
Top contributing states: TX, NY, and CA with 68% of transactions.
Overall activation rate: 57.5%
Overall delinquent rate: 6.06%
Conclusion
The Credit Card Financial Dashboard provides stakeholders with valuable insights into the performance and trends of credit card operations. By leveraging real-time data and advanced analytics, the dashboard supports informed decision-making and strategic planning.

Repository
The project repository can be found at: Credit Card Financial Dashboard
