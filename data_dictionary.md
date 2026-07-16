\# Data Dictionary — UAE FinPay

\## Project 2: BNPL Default Risk Predictor \& Expected Loss Model



\---



\## Core Customer \& Credit Fields



| Field | Type | Description |

|-------|------|-------------|

| customer\_id | VARCHAR | Unique customer ID — format: UAE\_CUST\_\[ID] |

| transaction\_date | TIMESTAMP | Date of BNPL transaction (UTC+4, UAE local time) |

| amount\_aed | DECIMAL | BNPL purchase amount in UAE Dirhams (AED) |

| emirate | VARCHAR | UAE emirate — Dubai, Abu Dhabi, Sharjah, Ajman |

| kyc\_status | VARCHAR | KYC verification status — verified, pending, rejected |

| credit\_score | INTEGER | Customer credit score on 300-850 scale |

| annual\_income\_aed | DECIMAL | Customer annual income converted to AED (USD x 3.67) |

| purchase\_amount\_aed | DECIMAL | BNPL purchase amount converted to AED (USD x 3.67) |

| purchase\_category | VARCHAR | Product category — Beauty, Groceries, Travel, Electronics etc |

| bnpl\_provider | VARCHAR | BNPL provider — Sezzle, Affirm etc |

| gender | VARCHAR | Customer gender — Male, Female, Non-Binary |



\---



\## BNPL Credit Risk Fields



| Field | Type | Description |

|-------|------|-------------|

| default\_flag | INTEGER | Default label — 1 = defaulted, 0 = paid on time |

| repayment\_status | VARCHAR | Raw repayment status — Defaulted or Paid On Time |

| credit\_risk\_tier | VARCHAR | Credit tier from credit score — HIGH\_RISK (below 580), MEDIUM\_RISK (580-670), LOW\_RISK (670-740), VERY\_LOW\_RISK (above 740) |



\---



\## Expected Loss Fields



| Field | Type | Description |

|-------|------|-------------|

| pd\_score | DECIMAL | Probability of Default — model output between 0 and 1 |

| ead | DECIMAL | Exposure at Default — purchase amount in AED |

| lgd | DECIMAL | Loss Given Default — fixed at 0.65 (65%) for unsecured BNPL |

| expected\_loss\_aed | DECIMAL | Expected Loss = PD x LGD x EAD calculated in AED |

| pd\_risk\_tier | VARCHAR | Risk tier from PD score — LOW\_RISK (0-20%), MEDIUM\_RISK (20-40%), HIGH\_RISK (40-60%), VERY\_HIGH\_RISK (above 60%) |

| ltv\_aed | DECIMAL | Customer Lifetime Value proxy in AED |

| net\_customer\_value\_aed | DECIMAL | LTV minus Expected Loss — profitability metric |



\---



\## Model Performance Fields



| Field | Type | Description |

|-------|------|-------------|

| auc\_roc | DECIMAL | Area Under ROC Curve — model discrimination ability |

| precision | DECIMAL | True positives divided by total predicted positives |

| recall | DECIMAL | True positives divided by total actual positives |

| f1\_score | DECIMAL | Harmonic mean of precision and recall |

| feature\_importance | DECIMAL | Random Forest feature importance score 0-1 |



\---



\## Expected Loss Calculation



Expected Loss (EL) = PD x LGD x EAD

Where:

PD  = Probability of Default (model output, 0-1 scale)

LGD = Loss Given Default (65% for unsecured BNPL)

EAD = Exposure at Default (purchase\_amount\_aed)

Example:

Customer A: PD = 0.08, LGD = 0.65, EAD = AED 2,000

Expected Loss = 0.08 x 0.65 x 2,000 = AED 104



\---



\## CBUAE Compliance Notes



\- Maximum BNPL tenure: 36 months per Cabinet Resolution No.134/2025

\- Affordability assessment applied using credit score and income fields

\- AECB reporting triggered for customers with 30+ days past due

\- PDPL data minimisation applied — no sensitive personal identifiers stored



For full regulatory context see COMPLIANCE\_CREDIT\_RISK.md



\---



\## Data Lineage Reference



\- README.md — Project overview and methodology

\- COMPLIANCE\_CREDIT\_RISK.md — CBUAE, PDPL, AECB regulatory framework



\---



Last Updated: July 2026

Maintained By: Kunal Sharma — Financial Data Analyst

