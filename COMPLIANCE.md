# Regulatory Compliance Framework

## UAE FinPay — Project 2: BNPL Default Risk & Expected Loss Model

---

## Executive Summary

This project implements a credit risk framework for UAE FinPay's BNPL product, aligned with CBUAE's 2026 consumer protection and credit risk management regulations. The methodology focuses on Expected Loss calculation (PD × LGD × EAD), risk tier segmentation, and fair lending practices per Cabinet Resolution No.134/2025.

**Key Compliance Areas:**
- Consumer Protection (BNPL tenure limits, affordability assessment)
- Credit Risk Management (Expected Loss methodology, IFRS 9 alignment)
- Data Protection (PDPL compliance for customer financial data)
- Credit Information Sharing (AECB reporting requirements)

---

## CBUAE Consumer Protection Framework (BNPL-Specific)

### Legal Basis

- **Cabinet Resolution No. (134) of 2025** — Executive Regulations for Consumer Protection in Financial Services
- **Federal Decree-Law No. (10) of 2025** — AML/CFT/CPF (data protection provisions)
- **CBUAE Consumer Protection Guidance for Payment Service Providers** — March 2026

### BNPL Product Requirements

| Requirement | CBUAE Mandate | Applied in This Project |
|-------------|---------------|------------------------|
| Maximum Tenure | 36 months (3 years) | BNPL transactions filtered to max 36-month tenure |
| Affordability Assessment | Mandatory before credit approval | Customer income and existing debt considered in risk scoring |
| Transparent Disclosure | Fees, penalties, repayment schedules | Clear risk tier communication (Low/Medium/High/Very High) |
| Fair Treatment | No discriminatory pricing | Risk-based pricing justified by Expected Loss (PD × LGD × EAD) |
| Complaint Handling | Dedicated channel, 15-day resolution | Modeled compliance framework for customer grievance escalation |

### Critical Clarification — BNPL vs Personal Loan

BNPL products under CBUAE 2026 guidance are classified as **short-term credit facilities** with:
- Maximum tenure: 36 months (vs 60+ months for personal loans)
- Lower regulatory capital requirements (if Sharia-compliant structure)
- Simplified affordability assessment (vs full income verification for personal loans)

This project models BNPL-specific risk characteristics, not traditional personal loan underwriting.

---

## CBUAE Credit Risk Management Framework

### Expected Loss Methodology

This project implements the **standard Expected Loss (EL) formula** per CBUAE Credit Risk Management Regulation:

Expected Loss (EL) = PD × LGD × EAD


Where:
- **PD (Probability of Default):** Likelihood customer defaults within 12 months
- **LGD (Loss Given Default):** Percentage of exposure lost after recovery (estimated at 40% for unsecured BNPL)
- **EAD (Exposure at Default):** Total outstanding amount at time of default (in AED)

### IFRS 9 Alignment (Expected Credit Loss)

For provisioning purposes, this model aligns with **IFRS 9 Stage 1 ECL** (12-month expected credit loss):

| IFRS 9 Stage | Description | Applied in This Project |
|--------------|-------------|------------------------|
| Stage 1 | Performing loans, no significant increase in credit risk | All BNPL customers at origination |
| Stage 2 | Significant increase in credit risk (SICR) | Modeled via 30+ days past due flag |
| Stage 3 | Credit-impaired (default) | Target variable: `default` = 1 |

**Note:** This project focuses on Stage 1 (12-month PD) for simplicity. Production models would implement lifetime ECL for Stage 2/3.

### Risk Tier Segmentation

Customer segmentation aligns with CBUAE guidance on retail credit portfolios:

| Risk Tier | PD Range | Business Action |
|-----------|----------|-----------------|
| Low | 0-5% | Standard approval, competitive pricing |
| Medium | 5-15% | Enhanced review, moderate pricing |
| High | 15-30% | Senior underwriter approval, higher pricing |
| Very High | 30%+ | Decline or secured product alternative |

---

## Al Etihad Credit Bureau (AECB) Reporting

### Credit Information Sharing Requirements

Per CBUAE 2026 guidance, BNPL providers must report to AECB:

- **Customer identification:** Emirates ID, passport number
- **Credit facility details:** Approved limit, outstanding balance, payment history
- **Delinquency status:** 30+, 60+, 90+ days past due
- **Default events:** Accounts written off or charged off

### Applied in This Project

This project simulates AECB reporting by:
- Calculating `days_past_due` for each customer
- Flagging accounts with 30+ DPD for potential AECB reporting
- Modeling probability of default (PD) as input to AECB risk scoring

**Note:** Actual AECB reporting requires secure API integration and customer consent — not implemented in this analytical prototype.

---

## UAE Data Protection Law (PDPL)

### Legal Basis

- **Federal Decree-Law No. (45) of 2021** — Protection of Personal Data (PDPL)
- **CBUAE Guidance on Data Protection for Financial Institutions** — January 2026

### Compliance Applied

| PDPL Principle | Implementation in This Project |
|----------------|-------------------------------|
| **Data Minimisation** | Only necessary fields collected (customer_id, income, tenure, amount, credit_score, default) |
| **Purpose Limitation** | Data used solely for credit risk modeling — documented in model descriptions |
| **Storage Limitation** | 5-year retention for payment/credit data (per CBUAE record-keeping requirements) |
| **Cross-Border Transfer** | Azure cloud resources configured in UAE region (UAE North, Dubai) |
| **Customer Consent** | Modeled via `consent_flag` field — customers must opt-in for credit risk modeling |
| **Data Subject Rights** | Framework for customer data access, correction, deletion requests (not implemented in prototype) |

---

## VARA (Virtual Assets Regulatory Authority)

### Virtual Asset Transaction Monitoring

While this project focuses on traditional BNPL (fiat currency), the framework includes capability notes for:

- **Virtual asset transaction reporting** — if BNPL is extended to crypto-asset purchases
- **Stablecoin payment integration** — compliance with VARA Rulebook for Virtual Asset Activities
- **Crypto-adjacent monitoring** — flagging BNPL transactions linked to virtual asset exchanges

**Note:** VARA licensing required if BNPL product is used to purchase virtual assets (e.g., Bitcoin, Ethereum).

---

## Key 2026 Regulatory Updates Impacting BNPL

| Update | Impact on This Project |
|--------|----------------------|
| **CBUAE Expansion of Payment Service Provider Oversight** (Federal Decree-Law No. 6 of 2025) | BNPL providers now classified as credit facilities — requires licensing by September 2026 |
| **Mandatory AECB Reporting** | All BNPL providers must report customer credit data to AECB |
| **Consumer Protection Enhancement** (Cabinet Resolution No.134/2025) | Stricter affordability assessment, 36-month tenure cap, transparent pricing disclosure |
| **IFRS 9 ECL Provisioning** | BNPL portfolios must calculate expected credit loss for financial reporting |
| **FATF 5th Round Mutual Evaluation** (2026) | Enhanced AML/CFT controls for BNPL (customer due diligence, transaction monitoring) |

---

## Compliance Limitations (Prototype Scope)

This project is an **analytical prototype** for portfolio analytics. Production deployment would require:

- **Integration with core banking system** for real-time PD/EAD calculation
- **AECB API integration** for credit bureau data and reporting
- **Model validation and audit** by independent risk team (per CBUAE Model Risk Management guidance)
- **Customer consent management system** for PDPL compliance
- **VARA licensing** if BNPL is extended to virtual asset purchases

---

## Sources

- Cabinet Resolution No. (134) of 2025 — Consumer Protection in Financial Services
- Federal Decree-Law No. (10) of 2025 — AML/CFT/CPF
- Federal Decree-Law No. (45) of 2021 — Protection of Personal Data (PDPL)
- Federal Decree-Law No. 6 of 2025 — Central Bank and Financial Institutions Law
- CBUAE Credit Risk Management Regulation (Regulation No. 178/2016, updated 2025)
- CBUAE Consumer Protection Guidance for Payment Service Providers — March 2026
- Al Etihad Credit Bureau (AECB) — Credit Information Sharing Framework
- IFRS 9 — Financial Instruments (Expected Credit Loss)
- VARA Rulebook for Virtual Asset Activities — 2025 Edition

---