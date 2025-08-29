# Loan Data Analysis – Documentation

## Introduction
The purpose of this assignment is to explore, clean, and analyze a loan dataset to understand borrower characteristics, loan funding details, repayment performance, and risk-related factors.

The analysis involves:
- Data Cleaning  
- Feature Reduction  
- Feature Engineering  
- Exploratory Data Analysis (EDA)  
- Insights from Loan Funding, Borrower Profiles, Loan Status, and Time-based Trends  

---

## Libraries Used
The following Python libraries were used:
- **pandas** : Data manipulation and analysis  
- **numpy** : Numerical computations  
- **matplotlib / seaborn** : Data visualization  
- **datetime** : Handling date/time values  
- **sklearn** : Data preprocessing and feature engineering  

---

## Data Exploration

### 3.1 Dataset Overview
- Dataset loaded into a pandas DataFrame.  
- Initial inspection done: shape, column names, data types.  
- Dataset initially had **111 columns**.  

---

## Data Cleaning – 001

### Handling Missing Values
- Dropped all columns with **100% missing values** (54 columns).  
- Removed columns with **more than 30% missing values**.  
- Replaced NaN in categorical columns:  
  - `emp_title`, `title` → `"Unknown"`.  
- Removed rows with missing values in `last_pymnt_d`, `last_credit_pull_d` (converted to datetime).  
- Replaced missing values in numerical columns using **mean imputation**:  
  - `collections_12_mths_ex_med`  
  - `chargeoff_within_12_mths`  
  - `pub_rec_bankruptcies`  
  - `tax_liens`  
- Filled missing values in `emp_length` with `"0 years"`.  

### Duplicate Check
- Verified no duplicate rows remained.  

---

## Feature Reduction
Classified dataset columns into categories:

- **Discrete (intCols):**  
  `delinq_2yrs`, `inq_last_6mths`, `open_acc`, `pub_rec`, `revol_bal`, `total_acc`, `total_rec_prncp`, `total_rec_int`, `pub_rec_bankruptcies`  

- **Continuous (floatCols):**  
  `loan_amnt`, `funded_amnt`, `funded_amnt_inv`, `annual_inc`, `installment`, `dti`, `last_pymnt_amnt`, `total_pymnt`, `total_pymnt_inv`, `revol_util`  

- **Categorical (catCols):**  
  `grade`, `home_ownership`, `verification_status`, `loan_status`, `purpose`, `term`  

- **Categorical to Numeric (catColstoNum):**  
  `int_rate`, `emp_length`  

- **Date (dateCols):**  
  `issue_d`, `earliest_cr_line`  

➡️ Dropped irrelevant or redundant columns after evaluation.  

---

## Data Cleaning – 002
- Converted date columns (`issue_d`, `earliest_cr_line`, `last_pymnt_d`) to **datetime format**.  
- Converted string-based numerical columns (e.g., `int_rate`, `emp_length`) into numeric values.  
- Finalized column data types for consistency.  

---

## Feature Engineering

### Categorical Encoding
- Applied **one-hot encoding** and **label encoding** where required.  

### Derived Features
- `principal_paid_ratio = total_rec_prncp / loan_amnt`  
- `interest_paid_ratio = total_rec_int / loan_amnt`  
- `debt_ratio = installment / annual_inc`  
- `credit_history_years = issue_d.year - earliest_cr_line.year`  
- `delinq_flag` = Categorized delinquency status (**No, Maybe, Yes**)  

### Final Feature Set
- **Loan and Funding Information:**  
  `loan_amnt`, `funded_amnt`, `funded_amnt_inv`, `term`, `int_rate`, `installment`  

- **Borrower Characteristics:**  
  `grade`, `emp_length`, `home_ownership`, `annual_inc`, `verification_status`  

- **Loan Performance and Status:**  
  `issue_d`, `loan_status`, `purpose`, `dti`, `delinq_2yrs`, `earliest_cr_line`, `inq_last_6mths`,  
  `open_acc`, `pub_rec`, `revol_bal`, `revol_util`, `total_acc`,  
  `total_pymnt`, `total_pymnt_inv`, `total_rec_prncp`, `total_rec_int`,  
  `last_pymnt_amnt`, `pub_rec_bankruptcies`  

- **Engineered Features:**  
  `principal_paid_ratio`, `interest_paid_ratio`, `debt_ratio`, `credit_history_years`, `delinq_flag`  

---

## Data Analysis and Insights

### 8.1 Loan and Funding Information
- Distribution of loan amounts requested by borrowers  
- Most common loan terms  
- Average funded vs requested loan amount  
- Difference between funded amount (lenders vs investors)  
- Percentage of loans issued per term  
- Average interest rate by loan grade  
- Average installment amount across loan categories  

### 8.2 Borrower Characteristics
- Borrower distribution by credit grade  
- Home ownership vs loan approval / interest rate  
- Income verification vs funding and interest  
- Borrower delinquency distribution  
- Borrowers by employment length  

### 8.3 Loan Performance and Status
- Loan status distribution  
- Loan purpose vs repayment outcome  
- Debt-to-Income Ratio (DTI) vs default risk  
- Delinquencies in last 2 years vs repayment  
- Credit inquiries (last 6 months) vs default  
- Open accounts and total accounts vs performance  
- Average repayment by loan grade  
- Bankruptcies vs loan status  

### 8.4 Engineered Features
- Principal and interest ratios vs loan status  
- Debt ratio vs repayment behavior  
- Credit history length vs default probability  
- Delinquency flag vs loan performance  
- Grade levels vs delinquency  

### 8.5 Time-based Analysis
- Loan issue date vs default trends  
- Loans issued per year  
- Average loan amount over time  
- Loan purpose distribution over time  
- Monthly trend of total funded amount  

### 8.6 Correlation Analysis
- Average loan amount by grade and year  
- Loan amount vs funded amount  
- Correlation heatmap with interest rate  
- Loan amount vs installment values  
- Multicollinearity check: `total_rec_prncp`, `principal_paid_ratio`, `loan_amnt`  

---

## Conclusion
- Dataset was successfully cleaned, reduced, and transformed.  
- Derived features such as **debt ratio**, **principal/interest paid ratio**, and **credit history years** gave additional insights.  
- Analysis highlighted patterns in **loan issuance**, **borrower demographics**, **repayment behaviors**, and **financial risk**.  
- Findings can assist in **predictive modeling** for loan default classification and **credit risk management**.  
