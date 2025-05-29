# Marketing Campaign Analytics & Customer Segmentation

## Overview

This project analyses customer data for a grocery retailer to drive actionable marketing insights. The pipeline covers data cleaning, RFM segmentation, deep profiling, campaign ROI, and predictive modelling for campaign response.

---

## Business Objectives

- Identify and segment customers to maximize revenue and retention
- Optimise campaign targeting for highest ROI
- Predict future responders to improve campaign efficiency

---

## Data

- **Source:** [Kaggle Marketing Campaign Data](https://www.kaggle.com/datasets/imakash3011/customer-personality-analysis)
- **Rows:** ~2,200 customers, 29 features
- **Contents:** Demographics, product spend, channel usage, campaign response

---

## Analysis Pipeline

### 1. Data Cleaning & EDA
- Missing values handled, outliers checked, new features (Age, Tenure) engineered, converted to datetime
- Cleaned Date:

|   ID |   Year_Birth | Education   | Marital_Status   |   Income |   Kidhome |   Teenhome | Dt_Customer         |   Recency |   MntWines |   MntFruits |   MntMeatProducts |   MntFishProducts |   MntSweetProducts |   MntGoldProds |   NumDealsPurchases |   NumWebPurchases |   NumCatalogPurchases |   NumStorePurchases |   NumWebVisitsMonth |   AcceptedCmp3 |   AcceptedCmp4 |   AcceptedCmp5 |   AcceptedCmp1 |   AcceptedCmp2 |   Complain |   Z_CostContact |   Z_Revenue |   Response |   Age |
|-----:|-------------:|:------------|:-----------------|---------:|----------:|-----------:|:--------------------|----------:|-----------:|------------:|------------------:|------------------:|-------------------:|---------------:|--------------------:|------------------:|----------------------:|--------------------:|--------------------:|---------------:|---------------:|---------------:|---------------:|---------------:|-----------:|----------------:|------------:|-----------:|------:|
| 5524 |         1957 | Graduation  | Single           |    58138 |         0 |          0 | 2012-09-04 00:00:00 |        58 |        635 |          88 |               546 |               172 |                 88 |             88 |                   3 |                 8 |                    10 |                   4 |                   7 |              0 |              0 |              0 |              0 |              0 |          0 |               3 |          11 |          1 |    68 |
| 2174 |         1954 | Graduation  | Single           |    46344 |         1 |          1 | 2014-03-08 00:00:00 |        38 |         11 |           1 |                 6 |                 2 |                  1 |              6 |                   2 |                 1 |                     1 |                   2 |                   5 |              0 |              0 |              0 |              0 |              0 |          0 |               3 |          11 |          0 |    71 |
| 4141 |         1965 | Graduation  | Together         |    71613 |         0 |          0 | 2013-08-21 00:00:00 |        26 |        426 |          49 |               127 |               111 |                 21 |             42 |                   1 |                 8 |                     2 |                  10 |                   4 |              0 |              0 |              0 |              0 |              0 |          0 |               3 |          11 |          0 |    60 |
| 6182 |         1984 | Graduation  | Together         |    26646 |         1 |          0 | 2014-02-10 00:00:00 |        26 |         11 |           4 |                20 |                10 |                  3 |              5 |                   2 |                 2 |                     0 |                   4 |                   6 |              0 |              0 |              0 |              0 |              0 |          0 |               3 |          11 |          0 |    41 |
| 5324 |         1981 | PhD         | Married          |    58293 |         1 |          0 | 2014-01-19 00:00:00 |        94 |        173 |          43 |               118 |                46 |                 27 |             15 |                   5 |                 5 |                     3 |                   6 |                   5 |              0 |              0 |              0 |              0 |              0 |          0 |               3 |          11 |          0 |    44 |

![Distribution of Customer Age](/age_histogram.png)


### 2. RFM Segmentation
- Calculated Recency, Frequency, and Monetary value
- Assigned quintile-based scores (1–5), created segment codes (e.g., Champions, Loyal, At Risk)

![Customer Segments by Size](rfm_segment_counts.png)

| Count               |   count |
|:--------------------|--------:|
| Hibernating         |     534 |
| Loyal Customers     |     471 |
| Potential Loyalists |     463 |
| Champions           |     334 |
| Promising           |     199 |
| At Risk             |     161 |
| New Customers       |      75 |

### 3. Deep Segment Profiling
- Demographics, product spend, and channel usage analysed by segment
![Average Product Spend by Segment](product_spend_by_segment.png)

![Channel Usage by Segment](channel_usage_by_segment.png)


### 4. Campaign Response & ROI Analysis
- Campaign acceptance rates and expected ROI calculated per segment and campaign
Visualise each product by segment

![Expected Campaign Revenue by Segment](expected_revenue_by_segment.png)

|                     |   AcceptedCmp1_ExpRevenue |   AcceptedCmp2_ExpRevenue |   AcceptedCmp3_ExpRevenue |   AcceptedCmp4_ExpRevenue |   AcceptedCmp5_ExpRevenue |
|:--------------------|--------------------------:|--------------------------:|--------------------------:|--------------------------:|--------------------------:|
| Champions           |                  83954.3  |                  13326.1  |                  41310.8  |                  59967.3  |                  95947.8  |
| Loyal Customers     |                  58927.4  |                  13928.3  |                  37499.3  |                  70712.9  |                  68570.1  |
| Potential Loyalists |                  12952.3  |                   2467.1  |                  19120    |                  22203.9  |                  15419.4  |
| At Risk             |                   2103.88 |                    420.78 |                   4628.54 |                   5470.09 |                    420.78 |
| Promising           |                      0    |                      0    |                   1455.15 |                    291.03 |                      0    |
| Hibernating         |                      0    |                    114.17 |                   1997.95 |                    228.34 |                      0    |
| New Customers       |                      0    |                      0    |                    148.27 |                      0    |                      0    |

### 5. Predictive Modeling
- Logistic regression to predict campaign response
- Features scaled and evaluated (precision, recall, F1, ROC-AUC)
'|              |   precision |   recall |   f1-score |   support |\n|:-------------|------------:|---------:|-----------:|----------:|\n| 0            |        0.87 |     0.98 |       0.93 |    572    |\n| 1            |        0.66 |     0.19 |       0.29 |    100    |\n| accuracy     |        0.86 |     0.86 |       0.86 |      0.86 |\n| macro avg    |        0.76 |     0.59 |       0.61 |    672    |\n| weighted avg |        0.84 |     0.86 |       0.83 |    672    |'

![ROC Curve for Campaign Response Model](roc_curve.png)

| Feature             |   Coefficient |
|:--------------------|--------------:|
| R_Score             |    0.691086   |
| MntWines            |    0.56884    |
| M_Score             |    0.552016   |
| NumWebPurchases     |    0.243979   |
| Kidhome             |    0.23732    |
| MntMeatProducts     |    0.223744   |
| NumCatalogPurchases |    0.14146    |
| MntFruits           |    0.0953911  |
| MntGoldProds        |    0.0639338  |
| F_Score             |    0.0246599  |
| Age                 |    0.00269325 |
| MntSweetProducts    |   -0.0437972  |
| MntFishProducts     |   -0.0759331  |
| Income              |   -0.296351   |
| Teenhome            |   -0.375085   |
| NumStorePurchases   |   -0.806589   |

---

## Key Insights

- **Champions** and **Loyal Customers** yield the highest campaign ROI; target with premium offers and loyalty programs.
- **Potential Loyalists** respond best to Campaigns 3 & 4; nurture for higher value.
- **Lower-value segments** (At Risk, Hibernating, New) require low-cost, automated re-engagement.
- Predictive model achieves ROC-AUC of 0.80; top predictors include recent activity, wine spend, and web/catalog engagement.

---

## Business Recommendations

- Prioritise premium campaigns for Champions and Loyal Customers (especially Campaigns 4 & 5)
- Use targeted, nurture offers for Potential Loyalists
- Employ cost-effective re-engagement for lower-value segments
- Apply model predictions to maximise ROI in future campaigns

---

## How to Reproduce

1. Clone this repo and download the data
2. Run notebooks in order:
    - `01_data_cleaning_and_eda.ipynb`
    - `02_rfm_feature_engineering.ipynb`
    - `03_campaign_roi_and_recommendations.ipynb`
    - `04_predictive_modeling.ipynb`
3. See outputs and visualisations as you proceed

---

## Data Dictionary

| Column                | Description                                                                          |
|-----------------------|--------------------------------------------------------------------------------------|
| AcceptedCmp1          | 1 if customer accepted the offer in the 1st campaign, 0 otherwise                    |
| AcceptedCmp2          | 1 if customer accepted the offer in the 2nd campaign, 0 otherwise                    |
| AcceptedCmp3          | 1 if customer accepted the offer in the 3rd campaign, 0 otherwise                    |
| AcceptedCmp4          | 1 if customer accepted the offer in the 4th campaign, 0 otherwise                    |
| AcceptedCmp5          | 1 if customer accepted the offer in the 5th campaign, 0 otherwise                    |
| Response (target)     | 1 if customer accepted the offer in the last campaign, 0 otherwise                   |
| Complain              | 1 if customer complained in the last 2 years                                         |
| DtCustomer            | Date of customer’s enrolment with the company                                        |
| Education             | Customer’s level of education                                                        |
| Marital               | Customer’s marital status                                                            |
| Kidhome               | Number of small children in customer’s household                                     |
| Teenhome              | Number of teenagers in customer’s household                                          |
| Income                | Customer’s yearly household income                                                   |
| MntFishProducts       | Amount spent on fish products in the last 2 years                                    |
| MntMeatProducts       | Amount spent on meat products in the last 2 years                                    |
| MntFruits             | Amount spent on fruits products in the last 2 years                                  |
| MntSweetProducts      | Amount spent on sweet products in the last 2 years                                   |
| MntWines              | Amount spent on wine products in the last 2 years                                    |
| MntGoldProds          | Amount spent on gold products in the last 2 years                                    |
| NumDealsPurchases     | Number of purchases made with discount                                               |
| NumCatalogPurchases   | Number of purchases made using catalogue                                             |
| NumStorePurchases     | Number of purchases made directly in stores                                          |
| NumWebPurchases       | Number of purchases made through company’s web site                                  |
| NumWebVisitsMonth     | Number of visits to company’s web site in the last month                             |
| Recency               | Number of days since the last purchase                                               |

---

## Assumptions & Limitations

- RFM and response at customer level (not transaction)
- No timestamped transactions, limiting some churn analysis
- Model performance can be improved with more data or other algorithms

---

## About

Created by Sina Sangsari (me!), digital marketer.  
