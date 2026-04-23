# 🔋 Battery Degradation Modeling & Simulation Pipeline

## 📁 WORKFLOW SCRIPTS
This folder contains scripts used to test a complete workflow from **battery degradation modeling** to **economic analysis**.

---

## 🎯 Objective
This repository provides a simplified and structured pipeline for:
- Extracting battery degradation characteristics  
- Fitting a **State of Health (SOH)** model  
- Running simulations in Simscape  
- Performing downstream economic evaluation  

The goal is to create a **clear, reproducible framework** for onboarding new users.  
If anything is unclear, please reach out.

---

## 🔄 Workflow Overview

**Battery Data
→ Degradation Extraction
→ SOH Model Fitting
→ Simscape Simulation
→ SOH Estimation
→ Data Logging
→ Data Export
→ Economic Analysis**
---

## 🧩 Pipeline Steps

### 1. Battery Data Input
Input battery cycling data including:
- Voltage  
- Current  
- Capacity (Ah)  
- Cycle count or time  

---

### 2. Degradation Feature Extraction
Compute degradation indicators as a function of **Full Equivalent Cycles (FEC)**:

- **Capacity Fade**  
  - Capacity vs FEC  

- **Internal Resistance**  
  ```math
  R = \frac{V_{open} - V_{load}}{I}
  
 -**Open Circuit Voltage Drift**
  - Vopen vs FEC
    
### 3. SOH Model Fitting
Define: $SOH = \frac{C}{C_{initial}}$

Fit a degradation model using optimization techniques
Use the parameter_fitting script provided in the repository

Notes:
-Single dataset → no weighting needed
-Multiple datasets → define appropriate weighting ratios

## 4. Parameter Export
Save fitted parameters:
.mat, .txt, or manual copy

⚠️ Important:
Ensure parameters are updated inside the Simscape subsystem before running simulations.

## 5. Simscape Model Execution
Run the Simscape battery model using repeated flight profiles
Mission profile (power input) is stored in the Data Store block

##6. SOH Estimation Module

Estimate:
-State of Charge (SOC)
-State of Health (SOH)
-Remaining Useful Life (RUL)

Each metric is implemented as an independent subsystem.

## 7. Data Logging
Use "To Workspace" blocks in Simulink to log:
-Cycles
-SOC
-SOH
-RUL
Save outputs as:
.mat file

##8. Data Export
Convert simulation outputs to CSV using MATLAB scripts
A sample export script is included in the repository

⚠️ Note:
Data is exported as timeseries, which may become deprecated in future MATLAB versions.

## 9. Run Economic analysis
Input flights till degradation and charging time to the excel solver including supporting details like flight time revenue per weight. 
