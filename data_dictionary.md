# Data Dictionary — UAE FinPay
## Project 2: BNPL Default Risk Predictor & Expected Loss Model

---

## Core Customer & Credit Fields

| Field | Type | Description |
|-------|------|-------------|
| customer_id | VARCHAR | Unique customer ID — format: UAE_CUST_[ID] |
| transaction_date | TIMESTAMP | Date of BNPL transaction (UTC+4, UAE local time) |
| amount_aed | DECIMAL | BNPL purchase amount in UAE Dirhams (AED) |
| emirate | VARCHAR | UAE emirate — Dubai, Abu Dhabi, Sharjah, Ajman |
| kyc_status | VARCHAR | KYC verification status — verified, pending, rejected |
| credit_score | INTEGER | Customer credit score on 300-850 scale |
| annual_income_aed | DECIMAL | Customer annual income converted to AED (USD x 3.67) |
| purchase_amount_aed | DECIMAL | BNPL purchase amount converted to AED (USD x 3.67) |
| purchase_category | VARCHAR | Product category — Beauty, Groceries, Travel, Electronics etc |
| bnpl_provider | VARCHAR | BNPL provider — Sezzle, Affirm etc |
| gender | VARCHAR | Customer gender — Male, Female, Non-Binary |

---

## BNPL Credit Risk Fields

| Field | Type | Description |
|-------|------|-------------|
| default_flag | INTEGER | Default label — 1 = defaulted, 0 = paid on time |
| repayment_status | VARCHAR | Raw repayment status — Defaulted or Paid On Time |
| credit_risk_tier | VARCHAR | Credit tier from credit score — HIGH_RISK (below 580), MEDIUM_RISK (580-670), LOW_RISK (670-740), VERY_LOW_RISK (above 740) |

---

## Expected Loss Fields

| Field | Type | Description |
|-------|------|-------------|
| pd_score | DECIMAL | Probability of Default — model output between 0 and 1 |
| ead | DECIMAL | Exposure at Default — purchase amount in AED |
| lgd | DECIMAL | Loss Given Default — fixed at 0.65 (65%) for unsecured BNPL |
| expected_loss_aed | DECIMAL | Expected Loss = PD x LGD x EAD calculated in AED |
| pd_risk_tier | VARCHAR | Risk tier from PD score — LOW_RISK (0-20%), MEDIUM_RISK (20-40%), HIGH_RISK (40-60%), VERY_HIGH_RISK (above 60%) |
| ltv_aed | DECIMAL | Customer Lifetime Value proxy in AED |
| net_customer_value_aed | DECIMAL | LTV minus Expected Loss — profitability metric |

---

## Model Performance Fields

| Field | Type | Description |
|-------|------|-------------|
| auc_roc | DECIMAL | Area Under ROC Curve — model discrimination ability |
| precision | DECIMAL | True positives divided by total predicted positives |
| recall | DECIMAL | True positives divided by total actual positives |
| f1_score | DECIMAL | Harmonic mean of precision and recall |
| feature_importance | DECIMAL | Random Forest feature importance score 0-1 |

---

## Expected Loss Calculation

Expected Loss (EL) = PD x LGD x EAD
Where:
PD  = Probability of Default (model output, 0-1 scale)
LGD = Loss Given Default (65% for unsecured BNPL)
EAD = Exposure at Default (purchase_amount_aed)
Example:
Customer A: PD = 0.08, LGD = 0.65, EAD = AED 2,000
Expected Loss = 0.08 x 0.65 x 2,000 = AED 104

---

## CBUAE Compliance Notes

- Maximum BNPL tenure: 36 months per Cabinet Resolution No.134/2025
- Affordability assessment applied using credit score and income fields
- AECB reporting triggered for customers with 30+ days past due
- PDPL data minimisation applied — no sensitive personal identifiers stored

For full regulatory context see COMPLIANCE_CREDIT_RISK.md

---

## Data Lineage Reference

- README.md — Project overview and methodology
- COMPLIANCE_CREDIT_RISK.md — CBUAE, PDPL, AECB regulatory framework

---

Last Updated: July 2026
Maintained By: Kunal Sharma — Financial Data Analyst
