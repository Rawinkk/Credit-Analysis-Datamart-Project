# Credit Risk Analysis Datamart Project
This project has been devoloped for practice myskils to create and design DataWareHouse purpose consist of Master DataWareHouse,Dimensional Modeling and ETL process.
## Contents:
- Dimensional Modeling
    - Dimension Tables
    - Fact Table
- ETL Process
    - Extract/Transform/Load
- Basic queries
## Dimensinal Modeling:
for this implementation I'm going to implement simple Dimentional Model. after I collected data source from lendingclub website and portfolios underlying U.S. residential mortgage-backed securities (RMBS) securitization portfolios and provided by International Financial Research that encourage me to create tables and factors as belows
### Dimension Tables
  1. borrwer_dim : This dimension table contains descriptive data about borrowers, such as their address, employment status, income, and other demographic information. Each row in the table represents a specific borrower.
  
  2. loan_purpose_dim : This dimension table contains descriptive data about the purpose of each loan, such as whether the loan is for a car, a house, or other types of purchases and the value of the asset.
  
  3. economic_indicator_dim: This dimension table contains descriptive data about the important economic indicator that effect to the model such as gdg_time, house price index at the time, unemployment rate at the time
  
  4. date_dim: This dimension table should be separate from the other dimention. Date columns that created base on purpose of business. you can reduce or add some columns in this table depending on the purpose the important columns.
### Fact Table
  I retrieve all measurable attributes and transactions factors into this table and populate surrogate keys to Fact table

