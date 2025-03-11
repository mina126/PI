# PI
# Data Analysis Report from Power BI

## **1. Objective**
**What is the main goal?**
The goal of this analysis is to evaluate the sales, quantity, and profitability performance of Plant Co. for 2023, comparing it with the previous year (PYTD). The objective is to understand performance impacts across different countries and products to optimize future strategies.

## **2. Data Source**
The data was extracted from a Power BI report based on company sales sources. It includes:
- **YTD (Year-To-Date) and PYTD (Previous Year-To-Date) metrics**
- **Total gross profit and profit percentage**
- **Country-wise performance analysis**
- **Sales trends across months**
- **Product classification (Indoor, Landscape, Outdoor)**
- **Profitability and market share analysis**

## **3. Data Cleaning Process**
Before conducting the analysis, the data was cleaned following these steps:

### **A. Removing Duplicates**
Data was scanned for duplicates using **SQL**, based on (Country, Product Name, Quantity Sold, Date). Duplicates were removed to ensure data accuracy.

### **B. Fixing Errors**
- **Trimmed extra spaces** in product names using `TRIM()`.
- **Standardized product names** to unify similar categories.
- **Converted date fields** from text format to actual date format using `STR_TO_DATE()`.

### **C. Handling Missing Values**
- Empty values in `total_laid_off` and `percentage_laid_off` were kept as they are essential for analysis.
- Records with completely missing essential values were removed to maintain data reliability.

### **D. Removing Unnecessary Data**
Irrelevant columns like `row_num`, which was only used for data processing, were dropped as they were not required for final analysis.

## **4. Data Exploration & Analysis**
### **A. Sales & Overall Performance**
- **Total YTD Sales:** 555.66K
- **PYTD Sales:** 538.61K
- **Year-over-Year Growth:** +17.05K
- **Average Gross Profit Margin:** 39.62%

### **B. Country-wise Performance**
#### **Bottom 10 Countries by YTD vs PYTD Performance:**
1. China: -9.76K
2. France: -9.36K
3. Sweden: -6.71K
4. Greece: -4.73K
5. Japan: -3.74K
6. Netherlands: -3.26K
7. Vietnam: -1.2K
8. United States: -1.1K

### **C. Trend Analysis**
#### **Sales Volume Across Months:**
- **Highest Sales:** February (52.26K)
- **Lowest Sales:** June (37.23K)
- **Sales showed a fluctuating trend with a dip in summer and a rise in winter.**

## **5. Development & Code Implementation**

### **A. Data Cleaning Code**
**Trimming extra spaces in product names:**
```sql
UPDATE sales_data 
SET product_name = TRIM(product_name);
```

**Converting date fields to proper format:**
```sql
UPDATE sales_data 
SET sale_date = STR_TO_DATE(sale_date, '%Y-%m-%d');
```

**Ensuring no duplicate data exists:**
```sql
DELETE FROM sales_data 
WHERE id NOT IN (
    SELECT MIN(id)
    FROM sales_data
    GROUP BY country, product_name, sale_date, quantity
);
```

## **6. Conclusions & Recommendations**
- **Focus on underperforming countries** like **China, France, and Sweden** to identify the reasons for declining sales.
- **Enhance sales during summer months** to counteract seasonal declines.
- **Improve data accuracy** by standardizing product names and ensuring proper industry classification.

This analysis enables data-driven decision-making to enhance overall company performance and profitability.

