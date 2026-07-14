# \# UAE FinPay BNPL Default Risk Predictor \& Expected Loss Model

# 

# \## Business Problem

# UAE FinPay's BNPL product faces rising default risk across

# customer segments in Dubai, Abu Dhabi, and Sharjah. This

# project builds a predictive default model, calculates

# Expected Loss in AED by risk tier, and simulates an A/B

# test on feature engineering to guide underwriting decisions.

# 

\## Data Lineage
Raw Layer (BNPL Dataset — Kaggle, Bhanage, 50,000 rows)
===

# ↓

# UAE Staging Layer (AED conversion, emirate, credit risk tier)

# ↓

# Feature Engineering (encoding, risk scoring)

# ↓

# Model Training (Logistic Regression vs Random Forest)

# ↓

# Expected Loss (PD × LGD × EAD in AED by risk tier)

# ↓

# A/B Test (credit score feature impact on AUC-ROC)

# ↓

# Net Customer Value (LTV minus Expected Loss)

# ↓

# GitHub (notebook, charts, compliance docs)



\## Tech Stack

Python 3.12 | pandas | scikit-learn | seaborn | scipy | Jupyter



\## Business Outcomes

\- Logistic Regression AUC-ROC 0.7154 — best performing model

&#x20; on this synthetic dataset (Random Forest: 0.7020)

\- Both models below 0.77 benchmark — expected for synthetic

&#x20; data without behavioral transaction history

\- Expected Loss calculated in AED across 4 risk tiers

\- Net Customer Value shows medium-risk segment profitable

&#x20; when LTV exceeds Expected Loss

\- A/B test quantifies credit score feature value with

&#x20; statistical significance test

\- CBUAE Consumer Protection compliance per Cabinet

&#x20; Resolution No.134/2025 applied

\- Default rate: 8.8% across 50,000 BNPL transactions



\## Key Analyses

| Analysis | Business Question |

|----------|------------------|

| Default Prediction | Which customers will default? |

| Expected Loss (PD×LGD×EAD) | How much AED is at risk per tier? |

| Risk Tier Segmentation | Low/Medium/High/Very High split |

| Feature Importance | What drives default — MLRO audit trail |

| A/B Test Simulation | Does credit score improve AUC-ROC? |

| Net Customer Value | Which tiers are profitable after loss? |

| CBUAE Compliance | Consumer Protection compliance check |



\## Model Performance

| Model | AUC-ROC | vs Benchmark (0.77) |

|-------|---------|---------------------|

| Logistic Regression | 0.7154 | -5.46% |

| Random Forest | 0.7020 | -6.80% |

| Industry Benchmark | 0.7700 | baseline |



> Note: Both models score below the 0.77 industry benchmark

> because this synthetic dataset lacks behavioral signals

> such as payment history and transaction velocity that

> production BNPL models use. The methodology — PD x LGD x EAD

> Expected Loss framework, A/B testing, and risk tier

> segmentation — reflects real-world BNPL credit risk practice.



\## Project Structure

uae-finpay-bnpl-risk-python/

├── README.md

├── COMPLIANCE.md

├── data\_dictionary.md

├── .gitignore

├── notebooks/

│   └── uae\_finpay\_bnpl\_risk\_analysis.ipynb

└── charts/

├── 01\_eda\_overview.png

├── 02\_model\_comparison.png

├── 03\_expected\_loss.png

└── 04\_feature\_importance.png



\## Data Quality

Dataset: 50,000 synthetic BNPL transactions

No missing values — dataset is analysis-ready

UAE staging layer adds emirate, AED conversion,

and CBUAE compliance flags



\## Regulatory Framework

See COMPLIANCE.md for CBUAE 2026 references including

Federal Decree-Law No.10/2025 and Cabinet Resolution No.134/2025.



\## GitHub

https://github.com/KunalFinData/uae-finpay-bnpl-risk-python



\## LinkedIn

https://www.linkedin.com/in/kunalsharma0425

