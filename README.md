Securitisation Risk Analytics Platform
Auto Loan Asset-Backed Securities (ABS) — Pool: ZAAUTO2024-1

Overview
This project delivers an end-to-end securitisation risk intelligence platform for the ZAAUTO2024-1 Auto Loan ABS pool — 500 auto loans with an aggregate outstanding balance of ₹31.78 Crore, originated across five regions of India. The analysis applies industry-standard methodologies used by rating agencies (S&P, Moody's, CRISIL, ICRA) and regulators (RBI, SEBI) for ongoing surveillance of structured finance pools.
FieldDetailAnalystDivyanshu SinghRoleData Analyst InternOrganizationZetheta Algorithms Pvt. Ltd.PoolZAAUTO2024-1 — Auto Loan ABSCutoff DateOctober 2024Pool Size₹31.78 Crore (500 active loans)Project Duration15 Days — June 2026

Key Metrics at a Glance
MetricValueStatusTotal Pool Outstanding₹31.78 Crore—Pool Factor0.5819NormalWeighted Average Coupon (WAC)10.95%Normal30+ DPD Rate14.11%⚠️ Breach (threshold: 5%)Total ECL Provision₹1.17 Crore (3.67% of pool)🔴 ElevatedMonthly Default Rate (CDR)0.233%MonitoredCollection Efficiency110.20%✅ NormalExcess Spread (Oct 2024)₹10.3 Lakhs✅ PositiveAvg CIBIL Score (pool)752Weighted by balance

Repository Structure
zetheta-project-1a-securitisation/
│
├── BI.pbix                          # Power BI dashboard (5-part analytics)
├── BI.pdf                           # Exported Power BI report
├── Securitisation_Analytics_Report.pdf   # Full 9-page analyst report
├── Securitisation_ECL_Model.xlsx    # IFRS 9 ECL model workbook
├── securitisation_risk_arena_game.html   # Gamified Risk Arena simulation
└── README.md

Project Structure — 7 Parts
Part 1 — Pool Architecture & Data Model

Star schema with 4 source datasets: auto_loan_securitisation_data (500 loans, 55 fields), dpd_snapshot_history (6,000 monthly snapshots), static_pool_vintage_data (376 rows, 15 vintages), dynamic_loss_monthly (11 months)
Pool Summary Dashboard: KPI cards, delinquency bucket distribution, regional breakdown, IFRS 9 stage classification

Part 2 — DPD Trend & Roll Rate Analysis

Monthly DPD trend tracking from Dec 2023 to Oct 2024 across buckets (Current → 90+ DPD)
Roll rate transition matrix showing migration probabilities between delinquency buckets
Key finding: 30+ DPD rate at 14.11% — breaches the standard 5% early-warning trigger
Stage 2 → Stage 3 migration confirmed as primary driver of ECL provision increase

Part 3 — Vintage & Static Pool Analysis

15 origination cohorts tracked from Q1 2021 to Q3 2024 using fixed-denominator methodology
2022 vintage cohorts show accelerated cumulative net loss curves (~1.75% by Month 30) vs 2021/2023 (~0.6%)
Monthly default rate (MDR) and Single Monthly Mortality (SMM) prepayment tracking
Net loss vs excess spread coverage analysis across 11 months

Part 4 — IFRS 9 ECL Model & Cash Flow Waterfall

Full ECL computation: ECL = PD × LGD × EAD under Ind AS 109 / IFRS 9
Three-stage classification: Stage 1 (12-month ECL), Stage 2 (lifetime ECL), Stage 3 (credit-impaired, lifetime ECL)
Total ECL: ₹1.17 Crore — 40.81% concentrated in Stage 3 (only 6.6% of pool by count)
Cash flow waterfall modelling: Senior AAA → Mezzanine BBB → Equity/Originator priority allocation
Trigger/covenant status table: 1 breach (30+ DPD), 4 passing

Part 5 — Stress Testing & Scenario Analysis
ScenarioDefault MultiplierAnnual LossECLCE CoverageRating ImpactBase Case1.0x₹0.40 Cr₹1.17 Cr25.90xAAA MaintainedModerate Stress1.5x₹0.47 Cr₹1.85 Cr9.54xAA MaintainedSevere Stress2.5x₹1.27 Cr₹3.30 Cr5.02x⚠️ Downgrade RiskCrisis (4x)4.0x₹2.33 Cr₹9.19 Cr2.71x🔴 Below AAAsf Min
Part 6 — Real-World Case Studies

2008 Global Financial Crisis — how the absence of vintage tracking, roll rate monitoring, and severe stress testing caused systemic collapse of US subprime MBS
IL&FS Crisis (2018) — obligor concentration risk and cash flow disruption in Indian structured finance; post-crisis RBI reforms (MHP/MRR — RBI/2021-22/85)

Part 7 — Conclusion & Recommendations

4 actionable risk findings with priority levels and recommended interventions
Enhanced surveillance protocol for DPD breach
Underwriting tightening guidance for 2022-style origination profiles
Reserve account top-up recommendation for Crisis scenario CE gap


Gamified Risk Arena
An interactive browser-based simulation (securitisation_risk_arena_game.html) where the user plays the role of a lead risk analyst managing the ZAAUTO2024-1 pool in real time.
Features:

5 live event rounds based on actual pool data (DPD breach, vintage divergence, Stage 3 concentration, stress CE gap, IL&FS-style servicer risk)
4 choices per event with expert feedback grounded in IFRS 9, RBI, and S&P criteria
Interactive Stress Lab — live waterfall, ECL, and CE coverage ratio updates across all 4 scenarios
Scoring system with final analyst rating (Senior Analyst AAA → Pool in Distress)


Methodology & Standards
FrameworkApplicationIFRS 9 / Ind AS 109ECL staging and provisioningRBI IRAC NormsNPA classification (90+ DPD)RBI/2021-22/85MHP, MRR, skin-in-the-game requirementsS&P AAAsf Criteria3.0x–4.0x base case CE coverage requirementStatic Pool AnalysisFixed-denominator vintage loss curve methodologyDPD Roll Rate MatrixMarkov-chain delinquency migration modelling

Tools & Technologies

Python 3.12 — pandas, numpy, matplotlib, openpyxl (data processing & analytics)
Microsoft Power BI — DAX measures, interactive dashboards, 5-module visual reporting
Excel — IFRS 9 ECL model, waterfall calculations, scenario tables
HTML / JavaScript — Gamified Risk Arena simulation platform
Git / GitHub — Private repository, branch protection, version control


Data Sources
DatasetRecordsDescriptionauto_loan_securitisation_data500 loansLoan-level data, 55 fields — borrower, vehicle, performancedpd_snapshot_history6,000 rowsMonthly DPD snapshots, Dec 2023 – Oct 2024static_pool_vintage_data376 rowsCumulative loss data, 15 origination vintagesdynamic_loss_monthly11 monthsPool-level collections, defaults, prepayments

Risk Findings Summary
#FindingRisk LevelRecommended Action130+ DPD at 14.11% — breaches 5% trigger🔴 HighActivate enhanced surveillance; review collection strategy22022 vintage loss curves accelerated vs peers🟡 MediumTighten underwriting; increase CE for future deals3Stage 3 ECL at 40.81% of total despite 6.6% of pool🟡 MediumAccelerate SARFAESI recovery; review LGD assumptions4Crisis scenario CE coverage at 2.71x (min: 3.0x)🟡 Low-MedTop up reserve account; monitor monthly

Submitted by: Divyanshu Singh | Data Analyst Intern | Zetheta Algorithms Pvt. Ltd. | June 2026
This repository is private and confidential per project NDA requirements.
