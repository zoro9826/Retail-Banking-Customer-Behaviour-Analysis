# Bank Customer EDA

Exploratory data analysis of a retail banking customer dataset — profiling customer demographics, account balances, and product holdings to surface behavioral patterns and correlations across income, savings, credit, and lending metrics.

## Repository Contents

| File | Description |
|---|---|
| `Banking.csv` | Raw dataset — 3,000 customers × 25 fields |
| `BankEDA (Version 1).ipynb` | First-pass EDA: univariate, bivariate, and correlation analysis |
| `BankEDA (Version 2).ipynb` | Refined EDA: adds data cleaning, missing-value checks, date parsing, and expanded written insights |

## Dataset Overview

`Banking.csv` contains 3,000 rows, each representing a bank customer, with 25 columns spanning demographics, account relationships, and financial holdings:

**Customer profile**
- `Client ID`, `Name`, `Age`, `Location ID`, `Joined Bank`, `Banking Contact`, `Nationality`, `Occupation`, `GenderId`

**Banking relationship**
- `Fee Structure`, `Loyalty Classification`, `Risk Weighting`, `BRId`, `IAId`

**Financial holdings**
- `Estimated Income`, `Superannuation Savings`, `Amount of Credit Cards`, `Credit Card Balance`, `Bank Loans`, `Bank Deposits`, `Checking Accounts`, `Saving Accounts`, `Foreign Currency Account`, `Business Lending`, `Properties Owned`

## Analysis Workflow

Both notebooks load the CSV with pandas and follow a standard EDA structure; Version 2 extends Version 1 with additional data-quality steps.

**1. Data Inspection**
- Shape, dtypes, `.info()`, and `.describe()` summaries
- Missing-value check per column (Version 2)
- Parsing `Joined Bank` into a proper datetime column (Version 2)

**2. Feature Engineering**
- Bucketing `Estimated Income` into an `Income Band` category (`Low` / `Med(Mid)` / `High`) using `pd.cut`

**3. Univariate Analysis**
- Value counts and count plots across categorical fields: `BRId`, `GenderId`, `IAId`, `Amount of Credit Cards`, `Nationality`, `Occupation`, `Fee Structure`, `Loyalty Classification`, `Properties Owned`, `Risk Weighting`, `Income Band`
- Histograms of value distributions per category

**4. Bivariate Analysis**
- Categorical fields plotted against `Nationality` to compare distributions across groups

**5. Numerical Analysis**
- Distribution plots for `Estimated Income`, `Superannuation Savings`, `Credit Card Balance`, `Bank Loans`, `Bank Deposits`, `Checking Accounts`, `Saving Accounts`, `Foreign Currency Account`, `Business Lending` (and `Age` in Version 2)
- Scatter plots for selected variable pairs, e.g. Bank Deposits vs. Saving Accounts, Checking Accounts vs. Foreign Currency Account, Age vs. Superannuation Savings

**6. Correlation / Heatmap Analysis**
- Correlation matrix and heatmap across all numerical financial fields

## Key Insights

- **Deposits and savings move together.** The strongest positive correlation is between `Bank Deposits` and `Checking Accounts` / `Saving Accounts` / `Foreign Currency Account`, indicating customers with high balances in one account type tend to hold substantial funds across other account types too.
- **Income, age, and accumulation.** Moderate correlations between `Age` / `Estimated Income` and balances like `Superannuation Savings`, `Saving Accounts`, and `Checking Accounts` reflect a typical financial lifecycle — older, higher-income customers tend to accumulate more savings and retirement funds, and may also carry higher credit balances or loans.
- **Property ownership is weakly correlated with banking metrics.** `Properties Owned` shows low correlation with the financial fields, suggesting it's driven by external factors (location, real estate market, inheritance) not captured in this dataset.
- **Business vs. personal banking are distinct.** `Business Lending` has a moderate link to `Bank Loans` (some customers carry both personal and business debt) but is largely uncorrelated with deposit or property metrics — suggesting it serves a distinct customer segment or need.

## Tools Used

- Python, pandas, NumPy
- matplotlib, seaborn (visualization)
