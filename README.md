# DEGO Project – Team 7

*Repository: [github.com/maxhaus31/dego-project-team7](https://github.com/maxhaus31/dego-project-team7) · Group 7 · DEGO 2606 · Nova SBE*
*YouTube Link: https://youtu.be/8CE5gpT0XNA*


## Abstract

This project analyses NovaCred's credit scoring dataset for data quality issues, algorithmic bias, and privacy/governance gaps. We identified significant disparate impact against women (DI = 0.77) and young applicants aged 18–25 (DI = 0.53), multiple PII fields lacking protection, and five critical governance gaps. All issues were quantified, remediated in code, and mapped to GDPR articles and EU AI Act obligations. Our findings demonstrate that NovaCred's current system constitutes a high-risk AI application under Annex III of the EU AI Act and requires immediate corrective action.

---

## Team Members

- Benjamin Iby – Product Lead
- Filippo Deluchi – Governance Officer
- Maximilian Haussmann – Data Engineer
- Tim Schmitz – Data Scientist

---

## Project Description

Credit scoring bias analysis for DEGO 2606 (Data Ecosystems and Governance in Organizations), MSc Business Analytics, Nova SBE.

---

## Structure

```
dego-project-team7/
|-- README.md                    # Project overview & findings summary
|-- data/                        # Data files
|-- notebooks/
|   |-- 01_DataQualityCheck.ipynb    # Part 1 – Data Engineer
|   |-- 02_BiasAnalysis.ipynb   # Part 2 – Data Scientist
|   +-- 03_PrivacyDemo.ipynb    # Part 3 – Governance Officer
```

The video is posted on YouTube because it is larger than 100MB.

---

## Executive Summary

### Dataset Overview

The NovaCred dataset contains 502 applicant records across 27 fields, covering applicant identity, financial profile, spending behaviour, and loan decisions. The data is stored in nested JSON format and is used to power an automated credit approval model. It contains embedded data quality issues, bias patterns, and multiple sensitive PII fields.

---

### 1. Data Quality Analysis

We identified and remediated issues across six data quality dimensions:

- **Duplicates** (Completeness): 4 duplicate records (0.8%) found. Duplicate SSNs with inconsistent personal information were flagged for further review.
- **Missing Values** (Completeness): 32 missing values across 26 columns, concentrated in `applicant_info` fields. Missing SSNs and emails flagged as incomplete applications.
- **Type Inconsistencies** (Validity): Several fields stored with incorrect data types (e.g., income as string); resolved to appropriate integers.
- **Gender Coding** (Consistency): Six distinct encodings found (`'Male'`, `'Female'`, `'M'`, `'F'`, `' '`, `None`). Normalized to `'Male'`, `'Female'`, and `'Unknown'`.
- **Date Formats** (Consistency): Three different formats detected (`YYYY-MM-DD`, `DD/MM/YYYY`, `YYYY/MM/DD`). Normalized to `YYYY-MM-DD`.
- **Invalid Values** (Accuracy): Invalid entries in `credit_history_months`, `debt_to_income`, and `savings_balance` — flagged for review.

---

### 2. Bias Detection & Fairness

**Gender Bias:**
The disparate impact ratio for gender is **DI = 0.7698**, below the four-fifths rule threshold of 0.80. Women are approved at only 77% the rate of men (Female: 66.0% vs. Male: 50.8%). This constitutes explicit evidence of adverse impact under fair lending law.

**Age Bias:**
The DI ratio comparing applicants aged 18–25 to those aged 36–50 is **DI = 0.5338** — well below threshold. Young applicants are approved at only 53% the rate of middle-aged applicants (18–25: 36.2% vs. 36–50: 67.8%).

**Proxy Discrimination:**
ZIP code showed no statistically significant correlation with gender (p = 0.361), ruling out geographic redlining as the primary driver. However, spending behaviour categories heavily associated with female applicants (e.g., Rent) are negatively correlated with loan approval (r = −0.094), indicating structural indirect discrimination.

**Interaction Effects:**
Bias is intersectional. Young women aged 18–25 face the lowest approval rate in the entire dataset at just **34.6%**, compared to over **72%** for middle-aged men.

**Algorithmic Transparency:**
A Random Forest feature importance analysis confirms that `Age` and `Is_Female` are among the top model features alongside financial variables (`Annual Income`, `Savings Balance`). This constitutes disparate treatment — a severe fair lending compliance violation.

---

### 3. Privacy & Governance

**PII Mapping & Remediations:**

| Field | PII Type | GDPR Article | Remediation |
|---|---|---|---|
| Full Name | Direct identifier | Art. 5(1)(c) – minimization | Pseudonymized (SHA-256 + salt) |
| Email Address | Direct identifier | Art. 5(1)(e) – storage limit | Pseudonymized (SHA-256 + salt) |
| Social Security No. | Sensitive identifier | Art. 9 – special category | Pseudonymized (SHA-256 + salt) |
| Date of Birth | Quasi-identifier | Art. 5(1)(c) – minimization | Generalized to age range |
| IP Address | Quasi-identifier | Art. 5(1)(b) – purpose limitation | Eliminated |
| ZIP Code | Quasi-identifier | Art. 5(1)(c) – minimization | Last two digits anonymized |
| Spending Behaviour (Alcohol, Gambling, Adult Ent., Healthcare) | Art. 9 sensitive | Art. 9 – special category | Records deleted; explicit consent required |

**EU AI Act Classification:** Credit scoring is classified as **HIGH RISK** under Annex III, requiring human oversight, transparency, and audit trails.

**Governance Gaps & Fixes (5 identified):**

1. **No Audit Trail** *(AI Act Art. 12 violation)*: Implemented automated JSON audit log capturing timestamp, app_id, AI decision, human intervention flag, and officer email. 500 events logged.
2. **No Consent Mechanism** *(GDPR Art. 9 violation)*: Sensitive spending records deleted. New `tracking_customer_consent` column added. Formal explicit consent procedure required.
3. **No Human Oversight** *(AI Act Art. 14 violation)*: `decision_loan_approved` renamed to `decision_loan_approved_AI`. New `decision_loan_approved_human` column created, awaiting human-in-the-loop implementation.
4. **Fairness Principle Violation** *(GDPR Art. 7 / AI Act Art. 10)*: Recommendations include data re-integration with bias-free sources, algorithmic re-weighting, and enforcement of DI ≥ 0.80 as a fairness constraint.
5. **No Retention Policy** *(GDPR Art. 5 violation)*: Retention schedule implemented — denied loans deleted 365 days after rejection; approved loans deleted 365 days after final installment.

---

## Status

| Component | Status |
|---|---|
| Data Quality Analysis (01_DataQualityCheck) | ✅ Complete |
| Bias Analysis (02_BiasAnalysis) | ✅ Complete |
| Privacy & Governance (03_Privacy) | ✅ Complete |
| Video Presentation (6 min, MP4) | ✅ Complete — all 4 members appear and speak; key visualizations and specific metrics cited |
| Q&A Preparation | 🔄 In progress — Session 6 on Monday |
| Final Submission | 🔄 On track |

---

## Individual Contributions

- **Maximilian Haussmann** (Data Engineer): Led data ingestion, cleaning pipeline, and all data quality remediation (notebook 01).
- **Tim Schmitz** (Data Scientist): Led bias detection, fairness metric calculations, proxy analysis, interaction effects, and Random Forest feature importance (notebook 02).
- **Filippo Deluchi** (Governance Officer): Led PII mapping, GDPR/AI Act analysis, pseudonymization demo, governance gap identification and fixes (notebook 03).
- **Benjamin Iby** (Product Lead): Project coordination, repository structure, presentation narrative, and README.
