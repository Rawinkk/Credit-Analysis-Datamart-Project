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

## Create Tables:

  ```
  CREATE TABLE borrower_dim
(
    borrower_id integer NOT NULL DEFAULT nextval('borrower_dim_borrower_id_seq'::regclass),
    address text COLLATE pg_catalog."default",
    employment_status text COLLATE pg_catalog."default",
    income real,
    yoj numeric,
    gender text COLLATE pg_catalog."default",
    education_level text COLLATE pg_catalog."default",
    home_ownership_status text COLLATE pg_catalog."default",
    derog integer,
    debt_to_income_ratio numeric(5,2),
    delinq integer,
    CONSTRAINT borrower_dim_pkey PRIMARY KEY (borrower_id)
);

CREATE TABLE date_dim
(
    date_key integer NOT NULL,
    date date NOT NULL,
    weekday character varying(9) COLLATE pg_catalog."default" NOT NULL,
    weekday_num integer NOT NULL,
    day_month integer NOT NULL,
    day_of_year integer NOT NULL,
    week_of_year integer NOT NULL,
    iso_week character(10) COLLATE pg_catalog."default" NOT NULL,
    month_num integer NOT NULL,
    month_name character varying(9) COLLATE pg_catalog."default" NOT NULL,
    month_name_short character(3) COLLATE pg_catalog."default" NOT NULL,
    quarter integer NOT NULL,
    year integer NOT NULL,
    first_day_of_month date NOT NULL,
    last_day_of_month date NOT NULL,
    yyyymm character(7) COLLATE pg_catalog."default" NOT NULL,
    weekend_indr character(10) COLLATE pg_catalog."default" NOT NULL,
    CONSTRAINT date_dim_pk PRIMARY KEY (date_key),
    CONSTRAINT date_dim_economic_indicator_dim_fkey FOREIGN KEY (date_key)
);

CREATE TABLE economic_indicator_dim
(
    economic_indicator_id integer NOT NULL DEFAULT nextval('economic_indicator_dim_economic_indicator_id_seq'::regclass),
    gdp_time numeric,
    uer_time numeric,
    hpi_time numeric,
    date_key integer,
    CONSTRAINT economic_indicator_dim_pkey PRIMARY KEY (economic_indicator_id)
);

CREATE TABLE loan_purpose_dim
(
    loan_purpose_id integer NOT NULL DEFAULT nextval('loan_purpose_dim_loan_purpose_id_seq'::regclass),
    loan_purpose_name text COLLATE pg_catalog."default",
    loan_purpose_category text COLLATE pg_catalog."default",
    value_h numeric,
    is_home_collateral boolean,
    CONSTRAINT loan_purpose_dim_pkey PRIMARY KEY (loan_purpose_id)
);

CREATE TABLE loan_fact
(
    loan_id integer NOT NULL DEFAULT nextval('loan_fact_loan_id_seq'::regclass),
    borrower_id integer,
    loan_amount numeric(10,2),
    interest_rate numeric(5,2),
    balance_orig_time numeric(10,2),
    mat_time date,
    origination_date date,
    loan_purpose_id integer,
    loan_risk_score numeric(5,2),
    economic_indicator_id integer,
    date_dim integer,
    delinquency_status integer,
    status_time integer,
    loan_type integer,
    CONSTRAINT loan_fact_pkey PRIMARY KEY (loan_id),
    CONSTRAINT loan_fact_borrower_id_fkey FOREIGN KEY (borrower_id)
    CONSTRAINT loan_fact_date_dim_fkey FOREIGN KEY (date_dim)
    CONSTRAINT loan_fact_economic_indicator_id_fkey FOREIGN KEY (economic_indicator_id)
    CONSTRAINT loan_fact_economic_indicator_id_fkey1 FOREIGN KEY (economic_indicator_id)
    CONSTRAINT loan_fact_loan_purpose_id_fkey FOREIGN KEY (loan_purpose_id)
    CONSTRAINT loan_fact_loan_purpose_id_fkey1 FOREIGN KEY (loan_purpose_id)
);
```




