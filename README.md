# Credit Analysis Datamart Project
This project has been devoloped for practice myskils to create and design DataWareHouse consist of Master DataWareHouse,Dimensional Modeling and ETL process.
## Contents:
- Dimensional Modeling
    - Dimension Tables
    - Fact Table
    - ERD
- ETL Process
    - Extract/Transform/Load
## Dimensinal Modeling:
for this implementation I'm going to implement simple Dimentional Model. after I collected data source from lendingclub website and portfolios underlying U.S. residential mortgage-backed securities (RMBS) securitization portfolios and provided by International Financial Research that encourage me to create tables and factors as belows
### Dimension Tables
  1. borrower_dim : This dimension table contains descriptive data about borrowers, such as their address, employment status, income, and other demographic information. Each row in the table represents a specific borrower.
  
  2. loan_purpose_dim : This dimension table contains descriptive data about the purpose of each loan, such as whether the loan is for a car, a house, or other types of purchases and the value of the asset.
  
  3. economic_indicator_dim: This dimension table contains descriptive data about the important economic indicator that effect to the model such as gdg_time, house price index at the time, unemployment rate at the time
  
  4. date_dim: This dimension table should be separate from the other dimention. Date columns that created base on purpose of business. you can reduce or add some columns in this table depending on the purpose the important columns.
### Fact Table
  I retrieve all measurable attributes and transactions factors into this table and populate surrogate keys to Fact table

## ERD

![](https://github.com/Rawinkk/Credit-Analysis-Datamart-Project/blob/main/images/Screenshot_20230221_033743.png)

## ETL Process
I use Pentaho and PostgreSQL to extract, transform, and load data from an external data source to create a data mart. I will show you an example process by which I treat data below.
1. Create staging schemas for extracting and transforming data, then create core schemas to be a datamart after passing the process in staging.
2. Scan and prepare data sources in columns (datatype, special characters, missing value, etc.) from the fact table and dimensional table gradually.

![](https://github.com/Rawinkk/Credit-Analysis-Datamart-Project/blob/main/images/missing_value_long_str.png)

3. Adding a node from PostgreSQL connected to Petaho

![](https://github.com/Rawinkk/Credit-Analysis-Datamart-Project/blob/main/images/node.png)

4. Replacing, transforming, filtering data, and connecting to staging schemas

![](https://github.com/Rawinkk/Credit-Analysis-Datamart-Project/blob/main/images/pantaho_edit1.png)

5. Set up new data sorce from public schemas , insert into staging schemas and run job process in Pentaho program to load clean datamart to core schemas

![](https://github.com/Rawinkk/Credit-Analysis-Datamart-Project/blob/main/images/pentaho_edit2.png)
 
