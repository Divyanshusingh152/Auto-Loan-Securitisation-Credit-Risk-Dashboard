# Auto Loan Securitisation & Credit Risk Dashboard

## 📌 Project Overview
This repository contains a comprehensive, 5-page **Securitisation Risk Assessment Dashboard** built using Microsoft Power BI. The project simulates an institutional-grade banking risk analysis tracking a portfolio of **500 unique auto loans** with a total outstanding balance of **₹31.78 Crore ($317.79M)**. 

The analytical core utilizes advanced **DAX expressions** to evaluate portfolio health, payment performance, cash flow dynamics, cohort vintage degradation, and **IFRS 9 Expected Credit Loss (ECL)** risk reserves.

---

## 📊 Dashboard Architecture & Core Metrics

### 1. Pool Summary & Demographics
* **Total Active Loans:** 500 Unique IDs
* **Total Outstanding Pool Balance:** ₹317.79M (~₹31.78 Crore)
* **Weighted Average Coupon (WAC):** 10.95% *(Calculated using weight-proportional interest returns)*
* **Weighted Average Maturity (WAM):** 45.14 Months remaining
* **Insights:** The portfolio is incredibly well-balanced across employment types (Salaried: 24%, Self-Employed: 24%, Professionals: 28.4%). Geographically, the **East Region** represents the highest concentration with ₹7.69 Crore outstanding.

### 2. Delinquency Tracking
* **30+ DPD Rate:** 15.60% (78 Loans in the serious late-payment zone)
* **Trend Analysis:** Tracks the month-over-month increase in `AmountOverdue`, signaling key focal points for the bank's collections team.

### 3. Monthly Performance & Cash Flow
* **Average Collection Efficiency:** 129.12%
* **Insights:** Collection efficiency regularly crosses 100% due to a high volume of early loan prepayments and borrowers successfully clearing out older accumulated debts. Cash flow trends reveal standard cyclical "mountain range" spikes.

### 4. Vintage Analysis (Cohort Performance)
* Developed line charts mapping `MonthsOnBook` against `CumulativeNetLossRate` grouped by `VintageID`.
* Successfully measures long-term batch decay rates to pinpoint which past credit origination quarters carry higher systemic defaults.

### 5. IFRS 9 ECL Risk Reserve
* **Total Safety Cushion Money Set Aside:** ₹11.66M (~₹1.16 Crore)
* **Risk Breakdown:** Modeled across standard banking stages (Stage 1: Low Risk, Stage 2: Medium Risk, Stage 3: High Risk/Default). 
* **Insights:** Stage 3 is the tallest column by far, validating that the credit risk framework correctly allocates safety funds to high-emergency asset buckets.

---

## 🛠️ Advanced DAX Formulas Implemented

To build this institutional-grade risk dashboard, advanced DAX measures were implemented across the data model to handle financial calculations, conditional routing, and percentage rate breakdowns.

### 1. Total Active Loan Portfolio Count
Tracks the absolute volume of unique auto loan contracts active within the securitized pool.
```dax
Total_Loans = COUNT(auto_loan_securitisation_data[LoanID])
WAC = 
DIVIDE(
    SUMX(
        auto_loan_securitisation_data, 
        auto_loan_securitisation_data[InterestRate] * auto_loan_securitisation_data[CurrentBalance]
    ),
    SUM(auto_loan_securitisation_data[CurrentBalance])
) / 100

2. Weighted Average Coupon (WAC)
Calculates the true interest yield of the pool by weighting each individual loan's interest rate against its current outstanding balance, preventing skewness from smaller accounts.

Code snippet
WAC = 
DIVIDE(
    SUMX(
        auto_loan_securitisation_data, 
        auto_loan_securitisation_data[InterestRate] * auto_loan_securitisation_data[CurrentBalance]
    ),
    SUM(auto_loan_securitisation_data[CurrentBalance])
) / 100
3. Weighted Average Maturity (WAM)
Measures the asset pool's remaining lifespan in months, heavily weighting loans with massive capital exposure to provide accurate cash flow runway estimates.

Code snippet
WAM = 
DIVIDE(
    SUMX(
        auto_loan_securitisation_data, 
        auto_loan_securitisation_data[RemainingTerm] * auto_loan_securitisation_data[CurrentBalance]
    ),
    SUM(auto_loan_securitisation_data[CurrentBalance])
)
4. Serious Delinquency Count (30+ DPD Counter)
An advanced filtering measure that scans the entire portfolio array to isolate and count only borrowers who are 30 days or more late on their vehicle EMIs.

Code snippet
Loans_30_Plus = 
CALCULATE(
    [Total_Loans],
    auto_loan_securitisation_data[DelinquencyDays] >= 30
) + 0
5. Portfolio Late Payment Rate (30+ DPD Rate)
Establishes the fundamental Credit Risk Metric by dividing active late-stage loans against total pool issuance. This serves as the core trigger flag for risk managers.

Code snippet
30Plus_DPD_Rate = DIVIDE([Loans_30_Plus], [Total_Loans])
6. Dynamic Collection Efficiency Index
Measures monthly cash application logic against billing expectations. Evaluates operational cash collection performance over consecutive reporting schedules.

Code snippet
Collection_Efficiency = 
AVERAGE(dynamic_loss_monthly[CollectionEfficiency])
7. Total Safety Risk Reserve Allocation
Aggregates the macro-level expected loss parameters to evaluate the stability of the bank's safety cushion under regulatory compliance frameworks.

Code snippet
Total_Safety_Reserve = SUM(auto_loan_securitisation_data[ECL_Provision])
