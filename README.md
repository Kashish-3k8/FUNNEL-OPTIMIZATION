# E-Commerce Funnel Optimization Analysis

## Overview
This project focuses on analyzing the customer conversion funnel of an e-commerce platform to identify major leakage points and improve overall conversion efficiency. The analysis tracks user movement across different stages of the customer journey:

Visit → Product View → Add to Cart → Purchase

The objective of the project was to identify where users were dropping off, diagnose possible causes behind low conversion rates, and suggest data-driven optimization strategies.

---

# Problem Statement

Although the platform was receiving significant user traffic, the final purchase conversion rate remained very low. The business wanted to understand:

- At which stage maximum users were dropping off
- Which traffic sources were underperforming
- Whether device type affected conversion behavior
- How funnel leakage could be reduced to improve revenue

---

# Objectives

- Perform end-to-end funnel analysis using SQL
- Calculate stage-wise conversion rates
- Identify key leakage points in the customer journey
- Analyze conversion behavior across device types and traffic sources
- Recommend business strategies to improve conversions

---

# Tools & Technologies

- SQL
- MySQL Workbench
- Data Cleaning & Aggregation
- Funnel Analysis
- KPI Analysis

---

# Dataset

The dataset contains simulated e-commerce session-level data with the following attributes:

| Column Name | Description |
|---|---|
| session_id | Unique session identifier |
| device_type | Mobile/Desktop |
| traffic_source | Google, Instagram, Facebook, Direct |
| visited | Whether user visited |
| product_view | Whether product page viewed |
| add_to_cart | Whether product added to cart |
| purchase | Whether purchase completed |

---

# Funnel Stages

1. Visit
2. Product View
3. Add to Cart
4. Purchase

---

# Key Metrics Calculated

- Visit to Product View Conversion
- Product View to Cart Conversion
- Cart to Purchase Conversion
- Overall Purchase Conversion
- Device-wise Conversion
- Traffic Source-wise Conversion

---

# SQL Queries Used
'''
## 1. Funnel Conversion Analysis

```sql
SELECT
    COUNT(*) AS total_visits,

    SUM(product_view) AS product_views,

    ROUND(
        SUM(product_view)*100.0/COUNT(*),2
    ) AS visit_to_product_pct,

    SUM(add_to_cart) AS carts,

    ROUND(
        SUM(add_to_cart)*100.0/COUNT(*),2
    ) AS cart_pct,

    SUM(purchase) AS purchases,

    ROUND(
        SUM(purchase)*100.0/COUNT(*),2
    ) AS purchase_pct

FROM user_funnel;

## 2. Device-wise Leakage Analysis

```sql
SELECT
    device_type,

    COUNT(*) AS visits,

    SUM(add_to_cart) AS carts,

    SUM(purchase) AS purchases,

    ROUND(
        SUM(purchase)*100.0/
        NULLIF(SUM(add_to_cart),0),2
    ) AS cart_to_purchase_pct

FROM user_funnel
GROUP BY device_type;

## 3. Traffic Source Analysis

```sql
SELECT
    traffic_source,

    COUNT(*) AS visits,

    SUM(purchase) AS purchases,

    ROUND(
        SUM(purchase)*100.0/COUNT(*),2
    ) AS conversion_rate

FROM user_funnel
GROUP BY traffic_source
ORDER BY conversion_rate DESC;
```

---

# Key Findings

- Significant user drop-offs were observed across the funnel stages
- Conversion rates dropped to:
  - 21.21% at Product View stage
  - 4.20% at Add to Cart stage
  - 1.34% at Purchase stage
- Mobile users showed higher checkout abandonment
- Social traffic sources had lower conversion quality compared to direct and Google traffic

---

# Business Recommendations

Based on the analysis, the following recommendations were proposed:

- Simplify mobile checkout process
- Improve landing page relevance
- Retarget abandoned users
- Optimize campaign targeting
- Improve checkout user experience and payment flow

---

# Business Impact

The analysis helped identify critical leakage points affecting customer conversion and revenue generation. The insights can support:

- Better marketing ROI
- Improved user experience
- Higher conversion efficiency
- Reduced revenue leakage

---

# Learning Outcomes

Through this project, I gained hands-on experience in:

- SQL-based funnel analysis
- Conversion rate calculation
- KPI analysis
- Business problem-solving
- Customer behavior analysis
- Analytical storytelling

---

# Future Improvements

- Build interactive Power BI dashboards
- Add cohort analysis
- Perform A/B testing analysis
- Integrate real-time customer behavior tracking
- Apply predictive analytics for conversion forecasting

---

# Author

Kashish Kumari  
B.Tech Chemical Engineering, BIT Mesra  
Aspiring Data Analyst | Consulting & Analytics Enthusiast
