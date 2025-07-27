# Customer Churn Analysis

This README file provides a detailed analysis of customer churn based on the provided dataset. The goal of this analysis is to identify the key drivers of churn and recommend actionable solutions to improve customer retention.

---

## Data Overview

1.The analysis is based on the `Customer_Data.csv` file, which contains various attributes of customers. 
2.The dataset includes information on customer demographics, account details, and the services they use. 
3.The `SQL Queries.docx` file [cite: 2] contains queries used for initial data exploration.

The dataset contains **31 columns** and a substantial number of customer records, providing a rich source of information for churn analysis.

---

## In-depth Analysis & Key Insights

### 1. Customer Demographics and Churn

- **Age:** Younger customers, particularly those in the **18-25 age group**, have a higher churn rate. This could be due to factors like lower brand loyalty or more price sensitivity.
- **Marital Status:** Customers who are **not married** are more likely to churn compared to those who are married. This suggests that married customers might have more stable life situations, leading to longer-term commitments with service providers.

### 2. Contract and Tenure

-**Contract Type:** Customers on a **Month-to-Month contract** have a significantly higher churn rate compared to those on One-Year or Two-Year contracts. This is a critical insight, as it highlights the vulnerability of short-term contracts.
- **Tenure:** Customers with a **shorter tenure** are more likely to churn. This is a common trend in subscription-based services, where new customers are still evaluating the service and have not yet developed strong loyalty.

### 3. Service Usage and Churn

-**Internet Service:** Customers with **Fiber Optic** internet service have a higher churn rate compared to those with DSL. This might be counterintuitive, as Fiber Optic is a premium service. However, it could be related to higher prices or service reliability issues in certain areas.
- **Value Deals:** Customers on **Value Deals** have a lower churn rate, indicating that promotions and special offers are effective in retaining customers.

### 4. Churn Reasons

The top reasons for churn, as indicated in the `Churn_Category` and `Churn_Reason` columns, are:

- **Competitor Offers:** A large number of customers churned due to better offers from competitors, such as "competitor had better devices" or "competitor offered higher download speeds." 
- **Dissatisfaction:** "Product dissatisfaction" and "service dissatisfaction" are also significant drivers of churn. This points to issues with the quality of the service provided.
- **Price:** "Price too high" and "long-distance charges" are frequently cited as reasons for leaving. This highlights the importance of competitive pricing.

---

## Recommended Solutions

Based on the analysis, we recommend the following solutions to reduce customer churn:

### 1. Enhance Customer Retention Strategies

- **Targeted Offers for High-Risk Segments:** Develop targeted retention campaigns for high-risk customer segments, such as young, unmarried customers on month-to-month contracts.
- **Promote Long-Term Contracts:** Encourage customers to switch from Month-to-Month contracts to One-Year or Two-Year contracts by offering incentives like discounts or additional services.

### 2. Improve Service Quality and Pricing

- **Investigate Fiber Optic Issues:** Conduct a thorough investigation into the high churn rate among Fiber Optic customers to identify and address any service quality or pricing issues.
- **Competitive Pricing:** Regularly benchmark prices against competitors and adjust pricing strategies to remain competitive. Consider offering more flexible pricing plans to cater to different customer needs.

### 3. Proactive Customer Engagement

- **Customer Feedback Mechanism:** Implement a robust customer feedback mechanism to identify and address customer dissatisfaction before it leads to churn.
- **Loyalty Programs:** Introduce a loyalty program to reward long-term customers and provide them with exclusive benefits.

---

## SQL Queries

The following SQL queries were used for the initial data exploration:

```sql
-- Check Distinct Values for Gender
SELECT Gender, Count(Gender) as TotalCount,
Count(Gender) * 1.0 / (Select Count(*) from stg_Churn)  as Percentage
from stg_Churn
Group by Gender

-- Check Distinct Values for Contract
SELECT Contract, Count(Contract) as TotalCount,
Count(Contract) * 1.0 / (Select Count(*) from stg_Churn)  as Percentage
from stg_Churn
Group by Contract

-- Check Customer Status and Total Revenue
SELECT Customer_Status, Count(Customer_Status) as TotalCount, Sum(Total_Revenue) as TotalRev,
Sum(Total_Revenue) / (Select sum(Total_Revenue) from stg_Churn) * 100  as RevPercentage
from stg_Churn
Group by Customer_Status

-- Check Distinct Values for State
SELECT State, Count(State) as TotalCount,
Count(State) * 1.0 / (Select Count(*) from stg_Churn)  as Percentage
from stg_Churn
Group by State
Order by Percentage desc
