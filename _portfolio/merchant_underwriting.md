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


- **Decision Funnel:** Designing sequential SQL logic that filters the applications and strictly prioritizes regulatory compliance before evaluating financial metrics.
  - The SQL query used to construct the funnel can be found [here](https://github.com/tomnguyentran/merchant-underwriting-decision-engine/blob/main/queries/decision_engine.sql).
  - The SQL query used to aggregate the decision metrics for the report can be found [here](https://github.com/tomnguyentran/merchant-underwriting-decision-engine/blob/main/queries/summary_output.sql)


- **Automation & Business Impact**: Analyzing the engine's final output to validate the automation rate and quantify the financial exposure.
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

