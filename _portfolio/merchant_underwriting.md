---
title: "Merchant Underwriting Decision Engine"
excerpt: "Automated underwriting engine blocking $38M in exposure and streamlining 96% of decisions using SQL and Python. <br/><img src='/images/merchant_underwriting_summary/summary_output.png'>"
collection: portfolio
weight: 2
---

# Project Background
A merchant acquirer faced a surge of 2,000 merchant applications, representing over $108 million in potential processing volume.

However, the company's manual underwriting team has become a critical bottleneck. Relying on manual human review for every application delayed
revenue for legitimate businesses while increasing the risk of human error on high-stakes decisions.

This project builds an automated underwriting decision engine using SQL and Python. By implementing a logical decision funnel,
the system is designed to instantly approve safe merchants while automatically blocking $38 million in exposure from high-risk and prohibited applicants.


The architecture and insights of the decision engine are broken down into the following key areas:

- **Synthetic Data Generation:** Using Python to simulate a dataset of 2,000 merchant applications, specifically engineering realistic distributions to test the system.
  - The Python code used to generate the merchant datasets can be found [here](https://github.com/tomnguyentran/merchant-underwriting-decision-engine/blob/main/scripts/underwriting_datasets.ipynb).


- **Decision Funnel:** Designing SQL logic that filters the applications and strictly prioritizes regulatory compliance before evaluating financial risk.
  - The SQL query used to construct the funnel can be found [here](https://github.com/tomnguyentran/merchant-underwriting-decision-engine/blob/main/queries/decision_engine.sql).


- **Automation & Business Impact**: Analyzing the engine's final output to validate the automation rate and quantify the financial exposure.
  - The SQL query used to aggregate the decision metrics for the report can be found [here](https://github.com/tomnguyentran/merchant-underwriting-decision-engine/blob/main/queries/summary_output.sql)
  - The executive summary report used to visualize the portfolio exposure can be found [here](https://github.com/tomnguyentran/merchant-underwriting-decision-engine/blob/main/summary_output/summary_output.png).

---

# Data Structure

The database structure of the merchant applications consists of three tables: `applications`, `merchants`, and `mcc_codes`.

![data_structure](/images/merchant_underwriting_summary/underwriting_er_diagram.png)

---

# Executive Summary

### Overview of Findings

The automated underwriting engine processed **$108 million** in requested volume across 2,000 applications.
The logic safely onboarded **$64 million** in revenue while blocking **$38 million** in exposure from prohibited and high-risk merchants.
Furthermore, the system achieved a 96% automation rate, routing **$6 million** in complex cases to human underwriters for due diligence.

![executive_summary](/images/merchant_underwriting_summary/summary_output.png)

---

# Technical Deep Dive

### Synthetic Data Generation:

- Utilized the `faker` library and `random.seed(42)` to generate a dataset of 2,000 merchant applications and ensured consistent testing results.


- Applied specific probability weights using `random.choices([...], weights=[...])` to mirror realistic acceptance rates. For example, a 5% KYC failure rate and 2% TMF (blacklisted) hit rate to test the engine's ability to catch rare cases.


- Engineered a relational schema by passing the `merchant_id` from the **merchants** table to the **applications** table as a foreign key for SQL joins.

![python code](/images/merchant_underwriting_summary/underwriting_script.png)

### Decision Funnel:

- Implemented a hierarchical `CASE WHEN` logic that prioritizes regulatory compliance before evaluating financial risk, ensuring that high-risk applicants are rejected instantly to save processing resources.


- Designed a "Manual Review" tier to catch anomalies, such as **new businesses requesting >$50K**, automatically routing them to human underwriters for review.


- Wrapped the complex decision logic within a Common Table Expression (CTE) and created the final output as a **Database View** (`decision_results`), allowing the logic to be reused across multiple reports without rewriting the core code.

![sql query](/images/merchant_underwriting_summary/underwriting_logic.png)

### Automation & Business Impact:

- Aggregated the final output to group the 2,000 applications by their specific decision reasons and quantify the financial liability.


- Exported the aggregated SQL results to Excel and applied conditional formatting to create a high-level executive report. This final view communicates the **96% automation rate** and the **$38M in blocked exposure** to non-technical stakeholders.


- Revealed that new businesses were requesting significantly higher limits **($91K avg)** versus safe applicants ($53k avg), validating the business need for a manual review tier to catch these cases.

![sql summary report](/images/merchant_underwriting_summary/underwriting_summary_output.png)

![excel anomaly](/images/merchant_underwriting_summary/underwriting_anomaly.png)

---

# Future Improvements:

### To scale this prototype to a production-grade system, the following enhancements are recommended:

- **Transition to Machine Learning:** While the current SQL logic is an effective rule-based solution, implementing a machine learning model in Python would improve detection of complex patterns that static rules might miss.


- **Real-Time Data Streaming:** Currently, the engine processes applications in batch. The next step would be to wrap the logic in a streaming pipeline to process applications instantly as they arrive.
