# Customer Shopping Behavior Analysis

An end-to-end data analytics project that explores customer shopping behavior using **Python, SQL, and Power BI**. The project cleans and transforms customer-level purchase data, answers business questions with SQL, and presents insights in an interactive Power BI dashboard.

## Project Overview

Retail teams need to understand what customers buy, how much they spend, how discounts relate to purchases, and how shopping patterns differ across customer groups. This project analyzes a customer shopping dataset to help investigate these questions.

The supplied CSV contains **3,900 records and 18 columns**, including customer demographics, products and categories, purchase amounts, review ratings, subscription status, shipping type, discounts, previous purchases, payment method, and purchase frequency.

## Tools and Technologies

- **Python:** data cleaning, transformation, and exploratory data analysis
- **Pandas:** data manipulation and feature creation
- **Jupyter Notebook:** analysis workflow and documentation
- **SQL:** business-oriented aggregations and customer/product analysis
- **MySQL / SQLAlchemy:** loading the transformed data into a relational database
- **Power BI:** dashboarding and visual exploration

## Project Files

| File | Purpose |
|---|---|
| `Customer_Shopping_Behavior_Analysis.ipynb` | Python-based data inspection, cleaning, feature engineering, and database-loading workflow |
| `customer_shopping_behavior.csv` | Source customer shopping dataset |
| `customer_behavior_sql_queries.sql` | SQL queries for customer, product, revenue, discount, and shipping analysis |
| `customer_behavior_dashboard.pbix` | Power BI dashboard file |

## Workflow

1. **Load and inspect the data**  
   Read the CSV with Pandas and inspect sample records, data types, summary statistics, and missing values.

2. **Clean missing values**  
   Fill missing review ratings using the median rating within the corresponding product category.

3. **Standardize column names**  
   Convert column names to lowercase snake_case and rename the purchase amount field to `purchase_amount`.

4. **Create analytical features**  
   - Create age groups using quartile-based binning.
   - Map purchase-frequency labels to approximate day intervals.
   - Remove `promo_code_used` after checking its relationship with `discount_applied` in the notebook.

5. **Load the transformed data into a database**  
   Use SQLAlchemy to connect to MySQL and write the DataFrame to a `customer` table in the `customer_behavior` database.

6. **Query business questions with SQL**  
   Analyze customer spending, product ratings, discount rates, repeat purchases, subscription status, shipping types, and revenue by age group.

7. **Explore results in Power BI**  
   Open the `.pbix` file in Power BI Desktop to inspect the dashboard and its visualizations.

## Business Questions

The SQL analysis includes questions such as:

- How does purchase revenue compare by gender?
- Which customers used a discount and still spent at least the average purchase amount?
- Which products have the highest average review ratings?
- How do average purchase amounts compare for Standard and Express shipping?
- How do average spend and total revenue differ between subscribers and non-subscribers?
- Which products have the highest percentage of purchases with discounts?
- How can customers be grouped into New, Returning, and Loyal segments based on previous purchases?
- What are the top three purchased products within each category?
- How many repeat buyers are subscribers versus non-subscribers?
- How is revenue distributed across age groups?

These are analytical questions, not proof of causation. For example, differences between subscribers and non-subscribers do not by themselves show that subscriptions cause higher spending.

## Getting Started

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd <your-repository-folder>
```

### 2. Create a Python environment

```bash
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Install the core Python packages:

```bash
pip install pandas jupyter sqlalchemy pymysql
```

### 3. Run the notebook

Keep `Customer_Shopping_Behavior_Analysis.ipynb` and `customer_shopping_behavior.csv` in the same directory, then run:

```bash
jupyter notebook
```

Open the notebook and execute the cells in order.

### 4. Configure MySQL

Install and start MySQL Server, then create a database user with permission to create/use the project database and write tables. Configure connection details through environment variables or a local configuration file that is **not committed to Git**.

Example PowerShell environment variables for the current terminal session:

```powershell
$env:DB_USER = "your_mysql_username"
$env:DB_PASSWORD = "your_mysql_password"
$env:DB_HOST = "localhost"
$env:DB_PORT = "3306"
$env:DB_NAME = "customer_behavior"
```

Before running the database-loading section, update the notebook to read these variables (for example, with Python's `os.environ`) instead of hardcoding credentials. The notebook currently contains a hardcoded database password; remove it before publishing and rotate that password if it is real.

### 5. Run the SQL analysis

Load the transformed data into the `customer` table first, then execute the queries in `customer_behavior_sql_queries.sql` using a SQL client compatible with the query syntax. Check the SQL dialect before execution: the provided file includes PostgreSQL-style casting (`::numeric`), while the notebook's database-loading section uses MySQL. Adapt the cast and any other dialect-specific syntax if running the queries in MySQL.

### 6. Open the dashboard

Open `customer_behavior_dashboard.pbix` with **Power BI Desktop**. If the dashboard uses a local database connection, update its data-source credentials and refresh the data as needed.

## Notes and Limitations

- The purchase-frequency-to-days field is an approximate mapping of categories, not an observed transaction interval.
- Quartile-based age groups depend on the dataset's age distribution.
- The notebook checks whether `discount_applied` and `promo_code_used` match before dropping the latter. Review this assumption before using the transformed data for further analysis.
- Confirm the SQL dialect and database connection settings in your own environment.
- No performance metrics or business outcomes are claimed in this README; results should be reported only after reproducing the analysis.

## Future Improvements

- Add a data dictionary and explicit definitions for each business metric.
- Add automated data-quality checks and validation tests.
- Parameterize database configuration using environment variables.
- Make SQL queries compatible with a single documented database dialect.
- Add dashboard screenshots and a concise findings section after verifying the dashboard's actual visuals and results.
- Add reproducible exports of key analysis tables.

## Author

**Vagisha Bhavsar**

GitHub: [Vagishaa11](https://github.com/Vagishaa11)

---

If you use or extend this project, verify the data transformations and SQL dialect against your own environment before relying on the results.
