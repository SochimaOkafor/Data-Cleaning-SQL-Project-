# Data-Cleaning-SQL-Project-
# Introduction

Data cleaning is one of the most critical steps in any data analysis or data science project. Inconsistent, incomplete, or duplicate data can lead to misleading insights and poor decision-making.

This project focuses on using SQL to clean and prepare a dataset for analysis — addressing data quality issues such as missing values, duplicates, inconsistent formats, and incorrect entries. The goal is to ensure that the dataset is accurate, consistent, and ready for further analysis or visualization.

By applying SQL-based cleaning techniques, I demonstrate how relational database tools can be effectively used to manage and preprocess large datasets before analysis.

# Data Sources

The dataset used in this project is included in the /data folder in this repository.

It contains several columns such as:
- Customer_ID
- Customer_Name
- Email
- Date_of_Purchase
- Country
- Amount_Spent

# Data Preprocessing

The raw dataset contained various inconsistencies that needed cleaning before it could be analyzed. Below are the detailed steps performed using SQL:

1. **Handling Missing Data**
- Identified missing values using conditional queries (WHERE column_name IS NULL).
- Replaced or removed missing entries depending on their importance to the dataset.

2. **Removing Duplicates**
- Used ROW_NUMBER() and Common Table Expressions (CTEs) to identify and remove duplicate records:
```sql
WITH duplicate_cte AS (
  SELECT *,
         ROW_NUMBER() OVER (PARTITION BY Customer_ID ORDER BY Customer_ID) AS row_num
  FROM customers
)
DELETE FROM duplicate_cte WHERE row_num > 1;
```

3. **Standardizing Formats**
- Converted inconsistent date formats into a uniform YYYY-MM-DD format using CONVERT() or CAST().
- Standardized country names and text cases using string functions like UPPER() or LOWER().
<img width="1093" height="395" alt="image" src="https://github.com/user-attachments/assets/2049a2e2-07ad-4f0d-b56a-04fb81725a17" />



# Analysis Methods
While the primary goal of this project was data cleaning, several exploratory SQL queries were used to assess the dataset’s quality and patterns:

**Data Profiling:**
- Counting unique customers, transactions, and records per country.
- Checking minimum, maximum, and average spending values.

**Consistency Checks:**
- Ensuring referential integrity (e.g., no orphaned records).
- Validating data relationships between tables, if applicable.

**Key SQL Functions Used:**
- ROW_NUMBER(), GROUP BY, HAVING, CASE WHEN, CONVERT(), TRIM(), LOWER(), COUNT(), SUM(), AVG(), DISTINCT.

# Results

**After performing all cleaning steps, the final dataset:**
- Contained no duplicates or missing key records.
- Had consistent formats for dates, names, and categorical variables.
- Was ready for analysis and visualization in tools such as Power BI or Python.

**Sample validation queries:**
```sql
SELECT COUNT(*) FROM cleaned_data;  
SELECT COUNT(DISTINCT Customer_ID) FROM cleaned_data;
```

# Conclusions
**Key Takeaways**
- SQL is a powerful and efficient tool for cleaning and transforming data before analysis.
- Structured queries can handle missing values, duplicates, and inconsistencies even in large datasets.
- Clean data ensures reliability and accuracy in downstream analytics and reporting.

**Limitations & Future Work**
- The current project focuses on cleaning static data; future work can involve automating data cleaning pipelines using stored procedures or ETL tools.
- Integration with Python or Power BI could enhance analysis and visualization after cleaning.

# Technologies Used
- Language: SQL
- Database Tool: SQL Server 
