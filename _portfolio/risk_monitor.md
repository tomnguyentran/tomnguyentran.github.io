---
title: "Merchant Transaction Risk Monitor"
excerpt: "Risk analysis dashboard identifying $2.9M in fraud and visualizing chargeback trends using SQL and Tableau. <br/><img src='/images/risk_dashboard/chargeback_dashboard_small.png'>"
collection: portfolio
---

# Project Background
This project analyzes a dataset from a Fintech company that provides payment processing solutions for merchants.
The company's business model generates revenue though transaction fees, but profitability is threatened by fraudulent activities and chargebacks.

Note: This project uses a simulated dataset for educational purposes. The data was downloaded from this [website](https://www.kaggle.com/datasets/kartik2112/fraud-detection?select=fraudTrain.csv)

in 2019, the company processed about **$65 million** in total transaction volume. The main challenge identified was the significant amount of chargebacks
where customers dispute their transactions and demand refunds due to fraud or service issues. These disputes resulted in **$2.9 million** in losses and put the company
at risk with card networks (Visa/Mastercard), which typically penalize processors that exceed the 1% chargeback ratio.

The goal of this analysis was to evaluate the financial impact of fraud, identify high risk merchants, and recommend strategies to minimize losses using SQL and Tableau.

Insights and recommendations are provided on the following key areas:

- **Executive KPI Assessment:** An evaluation of the company's overall health, comparing total sales
against total loss to determine the chargeback ratio.

- **High Risk Merchant Identification:** A comprehensive visualization of all active merchants, using a diverging color palette to highlight merchants exceeding the safety threshold. 

- **Fraud Trends:** A timeline analysis tracking the company's risk performance throughout 2019.

- **Root Cause Analysis:** A breakdown of chargebacks by merchant category and Visa reason code to pinpoint the causes of financial loss.

The Python code used to simulate chargeback scenarios and assign Visa reason codes (10.4 and 13.1) can be found [here](https://github.com/tomnguyentran/chargeback/blob/ab9ab6bdf089db8786a845a388b4543e4587049d/python_scripts/chargeback.ipynb).

The SQL queries used to aggregate transaction metrics for the dashboard can be found [here](https://github.com/tomnguyentran/chargeback/blob/d1153e6c9ad380ec4fecce84fd2b324edd962c6b/queries/merchant_chargeback_ratios.sql).

A Tableau dashboard used to report and explore fraud trends can be found [here](https://public.tableau.com/app/profile/tom.tran3530/viz/chargeback_dashboard/Dashboard).



# Data Dictionary

The analysis began with a raw dataset containing about 1.3 million transaction records. This data was preprocessed in Python to engineer specific risk features, 
then aggregated using SQL to generate the final summary table used for the dashboard.

The summary table contains the following columns:

| Column Name        | Description                                             | Data Type |
|--------------------|---------------------------------------------------------|-----------|
| merchant           | Name of the merchant                                    | string    |
| category           | Category of the merchant                                | string    |
| date               | Transaction date (YYYY-MM format)                       | string    |
| total_transactions | Total number of transactions                            | int       |
| total_sales_usd    | Total sales amount in USD                               | float     |
| total_lost_usd     | Total amount lost to chargebacks in USD                 | float     |
| total_chargebacks  | Total number of chargebacks                             | int       |
| card_absent_10_4   | Number of chargebacks with Visa reason code 10.4        | int       |
| card_absent_13_1   | Number of chargebacks with Visa reason code 13.1        | int       |
| chargeback_ratio   | Percentage of transactions that resulted in chargebacks | float     |


# Executive Summary

### Overview of Findings

The analysis revealed a total financial loss of **$2.9 million** in 2019, primarily due to **"Card Absent"** fraud from **online merchants**.
The year began with a critical chargeback ratio of **1.15%**, but saw significant improvements throughout the year, dropping to **0.65%** by December.
This downward trend stabilized the company's overall annual ratio of **0.79%**.

Below is the overview page from the Tableau dashboard. The entire dashboard can be downloaded [here](https://public.tableau.com/app/profile/tom.tran3530/viz/chargeback_dashboard/Dashboard).

![Overview Page](/images/risk_dashboard/chargeback_dashboard.png)

# Insights Deep Dive

### Executive KPI Assessment:

* The company processed a total of **$65 million** in sales volume while losing **$2.9 million** from chargebacks. 
  

* The overall chargeback ratio is **0.79%**, which is under the critical 1% threshold. However, this is within the **0.8% danger zone**, requiring constant monitoring and improvement.

### High Risk Merchant Identification:

* The chart reveals that specific accounts (highlighted in red) have experienced chargebacks ratios exceeding **3.0%**, which is significantly higher than the company average.


* As the list descends towards the **0.8%**, the bars shift to gray (Warning Zone) and finally to green (Safe Zone) to instantly distinguish between risky and safe merchants.

![high risk merchants](/images/risk_dashboard/risky_merchants.png)

![safe merchants](/images/risk_dashboard/safe_merchants.png)



### Fraud Trends:

* The company began 2019 in a critical state, with a chargeback ratio of **1.15%** in January.
  

* Throughout the year, the performance steadily improved, hitting a low of **0.59%** in June and ending the year at a healthy **0.65%** in December.

![fraud trends](/images/risk_dashboard/fraud_trends.png)


### Root Cause Analysis:

* The primary cause of loss is **"Card Absent"** fraud (Reason code 10.4), which accounted for **5,220 incidents**. 
  This volume is more than double the second-highest reason code, "Items Not Received" (2,043 incidents)


* Online Merchants collectively drove the vast majority of disputes, accounting for nearly 4,000 incidents (led by the "Online Shopping" category with 2,190). 
This indicates that risk is heavily concentrated in digital transactions rather than physical retail or logistics issues


![root cause analysis](/images/risk_dashboard/root_cause.png)



# Recommendations:

Based on the insights and findings above, we would recommend the stakeholders to consider the following: 

* "Card Absent" fraud is the primary loss driver (5,220 incidents), concentrated within online merchants.
  * Recommendation: Implement 3D-Secure technology for all online transactions to verify cardholder identity at checkout and shift liability away from the merchant.


* Specific high risk merchants are exceeding a chargeback ratio of 3.0%, far above the 0.8% safety threshold.
  * Recommendation: Conduct an immediate audit of the top 20 merchants identified in the dashboard to determine if account termination is required.
