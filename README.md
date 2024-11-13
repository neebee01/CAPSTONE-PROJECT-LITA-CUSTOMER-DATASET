# CAPSTONE-PROJECT-LITA-CUSTOMER-DATASET

The customer dataset comprises information on over 1,500 subscribers,
including demographic details, subscription preferences, and revenue metrics.
This dataset offers insights into customer behavior, subscription patterns, 
and regional trends, providing a foundation for data-driven decisions on customer acquisition,
retention, and revenue growth.

 Here's a brief project overview:

*Project Title:* Customer Subscription Analysis

*Objective:* Analyze customer subscription data to identify trends, patterns, and insights for informed business decisions.

*Scope:* Examine 1,500+ customer records, focusing on subscription types, regional distribution, revenue, and cancellation rates.

*Goals:*

- Identify top-performing subscription types
- Determine regional customer distribution
- Analyze cancellation rates and revenue trends
- Inform data-driven business strategies
- 
 The primary goals of the Customer Subscription Analysis project are:

*Main Goal:*
Improve Customer Acquisition and Retention through Data-Driven Insights

*Specific Objectives:*

1. Identify the most profitable subscription types and packages.
2. Analyze customer distribution and trends across different regions.
3. Determine factors influencing subscription cancellations.
4. Optimize pricing strategies based on revenue analysis.
5. Inform marketing strategies to enhance customer engagement and retention.

*Key Performance Indicators (KPIs):*

1. Subscription growth rate
2. Customer retention rate
3. Revenue increase
4. Cancellation rate reduction
5. Return on Investment (ROI) improvement

By achieving these goals, the project aims to enhance the overall customer subscription experience, drive business growth, and increase revenue.

GOAL 
The goal is to produce an interactive and understandable analysis for an informed growth strategy for the Capstone and Package subscription company.

DATA SOURCES The primary source of Data used here is an Excel data file, CSV file.

TECHNOLGY USED Excel sheet excel SUM and AVERAGE functions Excel pivot table SQL SERVER (SQL)

Data cleaning Data Visualization Calcutions Analysis SQL- (structured query language) for data querrying

Github- for porfolio Building SKILLS

Data Cleaning Data EXPLORATION Data Analysis Data Visualisation

DATA CLEANING AND PREPARATION On the initial phase of Data cleaning and preparations,

I performed the following action; Data loading and inspection Handling missing variables Data cleaning and formatting

EXPLORATORY DATA ANALYSIS   

Find the most popular subscription type by the number of customers.*
SELECT 
  Top 1 SubscriptionType, 
  COUNT(CustomerID) AS TotalCustomers
FROM 
  [dbo].[LITA CUSTOMERDATA ]
GROUP BY 
  SubscriptionType
ORDER BY 
  TotalCustomers

  
 Retrieve the total number of customers from each region.*`
SELECT 
  Region, 
  COUNT(CustomerID) AS TotalCustomers
FROM 
  [dbo].[LITA CUSTOMERDATA ]
GROUP BY 
  Region;


 Find customers who canceled their subscription within 6 months.*```
SELECT 
  CustomerID,
  CustomerName ,
  SubscriptionStart, 
  SubscriptionEnd 
FROM 
  [dbo].[LITA CUSTOMERDATA ]
WHERE 
  Canceled = 1 
  AND SubscriptionEND >= 
  DATEADD(month, -6,GETDATE())


   find the top three regions by subscription cancellation:
  
SELECT TOP 3 
  Region,
  SUM(CASE WHEN Canceled = 1 THEN 1 ELSE 0 END) AS CancellationCount,
  (SUM(CASE WHEN Canceled = 1 THEN 1 ELSE 0 END) * 1.0 / 
   COUNT(CustomerID)) * 100 AS CancellationRate
FROM 
  [dbo].[LITA CUSTOMERDATA ]
GROUP BY 
  Region
ORDER BY 
  CancellationCount DESC;
```
find the total number of active and canceled subscriptions

*Total Active Subscriptions*
```
SELECT 
  COUNT(CustomerID) AS TotalActiveSubscriptions
FROM 
  [dbo].[LITA CUSTOMERDATA ]
WHERE 
  Canceled = 0;


*Total Canceled Subscriptions*

SELECT 
  COUNT(CustomerID) AS TotalCanceledSubscriptions
FROM 
  [dbo].[LITA CUSTOMERDATA ]
WHERE 
  Canceled = 1;
```

*Combined Result
SELECT 
  SUM(CASE WHEN Canceled = 0 THEN 1 ELSE 0 END) AS TotalActiveSubscriptions,
  SUM(CASE WHEN Canceled = 1 THEN 1 ELSE 0 END) AS TotalCanceledSubscriptions
FROM
[dbo].[LITA CUSTOMERDATA ];

Calculate the average subscription duration.*

SELECT 
  AVG(DATEDIFF(month ,SUBSCRIPTIONEnd, SUBSCRIPTIONStart)) AS AverageSubscriptionDuration
FROM 
  [dbo].[LITA CUSTOMERDATA ]

find customers with subscriptions longer than 12 months.
SELECT 
  CustomerID,
  CustomerName,
  SubscriptionStart,
  SubscriptionEnd
FROM 
  [dbo].[LITA CUSTOMERDATA ]
WHERE 
  SubscriptionEnd > DATEADD(month, 12, SubscriptionStart);


TOTAL REVENUE BY SUBSCRIPTION TYPE
SELECT 
  SubscriptionType,
  SUM(Revenue) AS TotalRevenue
FROM 
  [dbo].[LITA CUSTOMERDATA ]
GROUP BY 
  SubscriptionType
ORDER BY 
  TotalRevenue


