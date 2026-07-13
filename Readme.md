# Retail Sales Data Cleaning & Business Intelligence Dashboard

# 📌 Project Overview

This project demonstrates a complete end-to-end Data Analytics and Business Intelligence workflow, transforming raw retail sales data into a clean, structured, and interactive business dashboard.

The project follows a real-world analytics process:

- Understanding the business problem
- Identifying data quality issues
- Cleaning and transforming raw data
- Creating a structured data model
- Developing DAX measures
- Building an interactive Power BI dashboard
- Extracting business insights
- Providing recommendations for decision-making

The objective was to convert unreliable raw sales data into meaningful information that helps stakeholders understand revenue performance, customer behavior, and sales trends.

> **Note:** The original dataset and Power BI (.pbix) file are not publicly available. Dashboard screenshots, methodology, and analytical documentation are provided for portfolio demonstration purposes.

---

# 🎯 Business Problem

The organization collects sales and customer information from different sources. However, the raw data contains several inconsistencies, formatting issues, duplicate records, and incorrect data types.

These data quality problems make it difficult to perform accurate analysis and generate reliable business insights.

The project aims to solve the following challenges:

- Improve data accuracy and consistency
- Prepare clean analytical datasets
- Build a reliable data model
- Create meaningful performance indicators
- Develop an interactive dashboard
- Support business decisions through data insights

---

# ❓ Business Questions

The dashboard was designed to answer the following key business questions:

### Sales Performance

- What is the total revenue generated?
- How many orders were completed?
- What is the average order value?
- How does revenue change over time?

### Customer Analysis

- How many unique customers purchased products?
- Who are the highest-value customers based on revenue contribution?

### Category Analysis

- Which product categories generate the highest revenue?

### Regional Analysis

- Which regions perform best in terms of revenue?

------

# 📂 Dataset Overview

i generated the dataset using AI for analytical practice and portfolio demonstration.

It contains two main tables:

---

# Sales Transactions Table

| Column Name |
|-------------|
| Transaction_ID |
| Customer_ID |
| Order_Date |
| Product_Name |
| Category |
| Unit_Price |
| Quantity |
| Discount |
| Region |

---

# Customers Table

| Column Name |
|-------------|
| Customer_ID |
| Customer_Name |
| City |
| Region |
| Gender |

---

# 🔍 Data Quality Assessment

Before analysis, the raw dataset was reviewed to identify data quality problems.

## Issues Identified

### Date Issues

- Multiple date formats
- Incorrect date types
- Inconsistent date values

### Text Issues

- Different capitalization styles
- Product name inconsistencies

Example:

```
LAPTOP
Laptop
laptop
```

Standardized into:

```
Laptop
```

---

### Numeric Issues

- Currency symbols in price columns
- Numbers stored as text
- Incorrect discount formatting

Example:

Before:

```
$1,500
```

After:

```
1500
```

---

### Data Integrity Issues

- Incorrect customer IDs
- Missing standardization

---

# 🧹 Data Cleaning & Transformation

## Tool Used:

- Microsoft Power Query

Power Query was used to transform raw data into clean, analysis-ready tables.

---

# 🧹 Data Cleaning & Transformation (Power Query)

Power Query was used to clean, standardize, and transform the raw datasets before analysis.

---

# Customer Table Cleaning

Steps performed:

✔ Standardized `Customer_ID` format by converting values to uppercase
![Customer_ID](Power_Querry/Customers/customer_id_uppercase.png)

✔ Converted `Customer_Name` into the correct data type
![Customer_Name](Power_Querry/Customers/customer_name_data_type.png)

✔ Converted `City` into the correct data type
![City](Power_Querry/Customers/City_type.png)

✔ Created a cleaned `Gender` column using add Custom Cloumn with the help of following power querry M code

```Power Querry
if [Gender] = "M" then "Male"
else if [Gender] = "F" then "Female"
else Text.Proper([Gender])
```
replaced inconsistent gender values
![Gender](Power_Querry/Customers/Gender_custom_column.png)
![Gender](Power_Querry/Customers/Gender_clean.png)

converted Gender_Clean to correct data type and then original Gender Column was replaced by Gender_Clean by removing original one.
![Gender](Power_Querry/Customers/gender_clean_type.png)

✔ Replaced incorrect values in `Age` and converted the column to the correct data type
![Age](Power_Querry/Customers/age_replace_values.png)
![Age](Power_Querry/Customers/age_repvalues_2.png)
![Age](Power_Querry/Customers/age_type.png)

✔ Standardized `Join_Date` values by replacing inconsistent date formats
![Join_Date](Power_Querry/Customers/join_date_replace.png)

✔ Converted `Join_Date` into the correct date data type using locale settings
![Join_Date](Power_Querry/Customers/join_date_type1.png)

✔ Created a cleaned `Email` column using add custom column and replaced inconsistent email values using the following power querry M code

```Power Querry
if Text.Contains([Email], "@") and not Text.Contains([Email], ".com")
then [Email] & ".com"
else [Email]
```
![Email](Power_Querry/Customers/Email_Custom.png)

---

# Sales Transactions Table Cleaning

Steps performed:

✔ Standardized `Customer_ID` format by converting values to uppercase
![Customer_ID](Power_Querry/Sales_Transaction/customer_id_uppercase.png)

✔ Standardized `Order_Date` formats using locale settings
![Order_Date](Power_Querry/Sales_Transaction/order_date_1.png)

✔ Converted `Order_Date` into the correct date data type
![Order_Date](Power_Querry/Sales_Transaction/order_date_2.png)

✔ Capitalized `Product_Name` values
![Product_Name](Power_Querry/Sales_Transaction/product_capitalize.png)

✔ Capitalized `Category` values
![Category](Power_Querry/Sales_Transaction/category_capitalize.png)

✔ Capitalized `Region` values
![Region](Power_Querry/Sales_Transaction/region_capitalize.png)

✔ Replaced incorrect text values in the `Quantity` column
![Quantity](Power_Querry/Sales_Transaction/quantity_replace_values.png)

✔ Converted `Quantity` into the correct numeric data type
![Quantity](Power_Querry/Sales_Transaction/quantity_data_type.png)

✔ Replaced incorrect text values in the `Discount` column
![Discount](Power_Querry/Sales_Transaction/discount_replace_values_1.png)
![Discount](Power_Querry/Sales_Transaction/discount_replace_values_2.png)

null value in Discount were replaced with 0
![Discount](Power_Querry/Sales_Transaction/discount_null.png)

✔ Converted `Discount` into the correct numeric data type
![Discount](Power_Querry/Sales_Transaction/discount_data_type.png)

✔ Corrected `Unit_Price` data type
![Unit_Price](Power_Querry/Sales_Transaction/unit_price_data_type.png)

✔ Capitalized `Salesperson` values
![Salesperson](Power_Querry/Sales_Transaction/salesperson_capitalize.png)
replaced e in ahmed with a i.e; ahmad
![Salesperson](Power_Querry/Sales_Transaction/salesperson_replace_values.png)

---

# 🏗 Data Modeling

A relational data model was created to improve analysis accuracy, reporting performance, and enable time-based analysis.

The data model consists of three tables:

1. **Customers Table**
2. **Sales Transactions Table**
3. **Date Table**

---

## Model Structure

```text
                 Customers
                     |
                     | 1
                     |
                     | *
            Sales Transactions
                     |
                     | *
                     |
                     | 1
                 Date Table
```

---

## Relationships

### Customers → Sales Transactions

Relationship Type:

```
One-to-Many (1:*)
```

Primary Key:

```
Customers[Customer_ID]
```

Foreign Key:

```
Sales_Transactions[Customer_ID]
```

---

### Date Table → Sales Transactions

Relationship Type:

```
One-to-Many (1:*)
```

Primary Key:

```
Date[Date]
```

Foreign Key:

```
Sales_Transactions[Order_Date]
```

---

## Date Table Creation

A dedicated Date table was created using DAX before data modeling to support time intelligence calculations and accurate date-based analysis.

The Date table was connected with the Sales Transactions table using:

```
Date[Date] → Sales_Transactions[Order_Date]
```

---

## Data Model Screenshot

![Data Model](Data_Modeling/Model_View.png)
![Data Model](Data_Modeling/1.png)
![Data Model](Data_Modeling/2.png)


---

# 📐 DAX Development

DAX was used to create a Date Table, support time-based analysis, and develop dynamic measures for dashboard KPIs.

---

# 📅 Date Table Creation

A dedicated Date Table was created using DAX to enable accurate time intelligence analysis and establish a proper relationship with the Sales Transactions table.

## Date Table

```DAX
Date_Table =
CALENDAR(
    MIN(Sales_Transactions[Order_Date]),
    MAX(Sales_Transactions[Order_Date])
)
```
![Date_Table](DAX_development/Date_Table/Date_table.png)

---

## Month Column

A Month column was created for displaying monthly trends in the dashboard.

```DAX
Month =
FORMAT(
    Date_Table[Date],
    "MMM YYYY"
)
```
![Month](DAX_development/Date_Table/Month_date_table.png)

---

## Month Number Column

A Month Number column was created to sort months chronologically.

```DAX
Month_number =
YEAR(Date_Table[Date]) * 100 +
MONTH(Date_Table[Date])
```
![Month_no](DAX_development/Date_Table/month_number.png)

---

# 📊 DAX Measures Development

DAX measures were created to calculate key performance indicators (KPIs) and support business analysis.

---

## Revenue

Calculates total revenue based on quantity, unit price, and discount.

```DAX
Revenue =
SUMX(
    Sales_Transactions,
    Sales_Transactions[Quantity] *
    Sales_Transactions[Unit_Price] *
    (1 - Sales_Transactions[Discount])
)
```
![Revenue](DAX_development/Dax_Measures/Revenue.png)

---

## Total Orders

Calculates the total number of completed transactions.

```DAX
Total Orders =
COUNT(
    Sales_Transactions[Transaction_ID]
)
```
![Total_Orders](DAX_development/Dax_Measures/orders.png)

---

## Total Customers

Calculates the number of unique customers.

```DAX
Total Customers =
DISTINCTCOUNT(
    Customers[Customer_ID]
)
```
![Total_Customers](DAX_development/Dax_Measures/Total_Customers.png)

---

## Average Order Value

Calculates the average revenue generated per order.

```DAX
Average Order Value =
DIVIDE(
    [Revenue],
    [Total Orders]
)
```
![AOV](DAX_development/Dax_Measures/Average_order_value.png)

---

# 📊 Dashboard Development

An interactive Power BI dashboard was developed to monitor sales performance, analyze customer behavior, and identify business trends.

The dashboard includes KPI cards, analytical visuals, a customer detail table, and interactive slicers for filtering insights.

---

# Dashboard Features

## 📌 KPI Cards

The dashboard contains four key performance indicators:

- **Total Revenue**  
  Displays the overall revenue generated from sales transactions.

- **Total Orders**  
  Shows the total number of completed sales transactions.

- **Total Customers**  
  Displays the number of unique customers who purchased products.

- **Average Order Value**  
  Shows the average revenue generated per order.

---

# 📈 Visual Analysis

## Revenue by Product

Analyzes revenue contribution of individual products and identifies products generating the highest sales.

---

## Revenue by Category

Compares revenue performance across different product categories to identify high-performing categories.

---

## Revenue by Region

Analyzes regional sales performance and highlights regions contributing the most revenue.

---

## Revenue by Month

Displays monthly revenue trends to identify changes in sales performance over time.

---

## Orders by Region

Compares the number of orders across regions to understand sales activity distribution.

---

# 👥 Customer Analysis Table

A detailed customer table was created containing:

| Column | Description |
|--------|-------------|
| Customer_ID | Unique customer identifier |
| Customer_Name | Customer name |
| Revenue | Total revenue generated by customer |
| Orders | Total number of orders placed by customer |

This table helps identify valuable customers and analyze customer-level performance.

---

# 🎛️ Dashboard Filters (Slicers)

Three interactive slicers were added to allow users to filter dashboard insights:

- Region
- Category
- Month

These slicers enable dynamic exploration of sales performance across different business dimensions.

---

# 📸 Dashboard Preview

![Power BI Dashboard](dashboard/dashboard.png)

---

# 🔎 Analysis & Key Insights

## Revenue Performance

- Revenue trends show monthly changes in overall sales performance.
- Product and category analysis identifies major contributors to revenue.
- Regional analysis highlights differences in sales performance.

---

## Customer Insights

- Customer-level analysis helps identify high-value customers.
- Revenue and order information provides visibility into customer contribution.

---

## Product & Category Insights

- Product-level revenue analysis identifies top-performing products.
- Category comparison helps understand which categories drive sales.

---

## Regional Insights

- Revenue and order analysis highlights strong and weak performing regions.
- Regional comparisons help identify potential improvement opportunities.

---

# 💡 Business Recommendations

Based on dashboard analysis:

### 1. Focus on High-Performing Products and Categories

Increase marketing and inventory focus on products and categories generating higher revenue.

---

### 2. Improve Customer Retention

Develop retention strategies for customers contributing significant revenue.

---

### 3. Optimize Regional Performance

Investigate low-performing regions and develop targeted strategies for improvement.

---

### 4. Monitor Sales Trends

Use monthly revenue trends to plan promotions and business strategies during changing demand periods.

---

### 5. Use Data-Driven Decisions

Continue monitoring KPIs and dashboard insights to support strategic business decisions.
---

# 🛠 Tools & Technologies

| Tool | Purpose |
|---|---|
| Excel | Data Storage and Initial Review |
| Power Query | Data Cleaning and Transformation |
| Power BI | Dashboard Development |
| DAX | KPI Calculations |
| Data Modeling | Relationship Management |

---

# 📁 Project Structure

```
Retail-Sales-Business-Intelligence-Analytics

│
├── 01_Project_Documentation
│
├── 02_Data_Quality_Assessment
│
├── 03_Power_Query
│   └── Screenshots
│
├── 04_Data_Modeling
│
├── 05_DAX_Measures
│
├── 06_Power_BI_Dashboard
│   └── Dashboard_Screenshots
│
├── 07_Insights_Report
│
└── README.md
```

---

# 🔄 Complete Analytics Workflow

```
Business Problem
        ↓
Business Questions
        ↓
Dataset Understanding
        ↓
Data Quality Assessment
        ↓
Data Cleaning & Transformation
        ↓
Data Modeling
        ↓
DAX Development
        ↓
Dashboard Creation
        ↓
Data Analysis
        ↓
Insights Generation
        ↓
Business Recommendations
```

---

# ✅ Conclusion

This project demonstrates a complete Business Intelligence workflow, starting from raw data challenges and ending with actionable business insights.

The project showcases practical skills in:

✔ Data Cleaning  
✔ Power Query  
✔ Data Transformation  
✔ Data Modeling  
✔ DAX Calculations  
✔ Power BI Dashboard Development  
✔ Business Analysis  
✔ Data Storytelling  

The final dashboard provides stakeholders with a clear understanding of sales performance and supports better decision-making through data-driven insights.

---

# 📌 Author

**Yasir Shah**

Data Analyst | Power BI | SQL | Excel
