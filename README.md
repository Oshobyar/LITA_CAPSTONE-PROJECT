n# LITA_CAPSTONE-PROJECT
This is a documentation of my final project while learning Data Analysis at Incubator Hub.

## PROJECT 1:  Sales Performance Analysis for a Retail Store

### PROJECT OVERVIEW
This project aims to analyze the sales performance of a retail store over the past two years. By analyzing various parameters in the data set, we seek to uncover key insights such as top-selling products, regional performance, and monthly sales trends.

### DATA SOURCES
The data used was downloaded from Canvas LMS of the LITA Data Analysis class organized by the Incubator Hub

### TOOLS USED
- Microsoft Excel: Data Cleaning, Analysis and Visualization [Download Here](https://www.microsoft.com)
- SQL- Structured Query Language: Querying of Data [Download Here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- PowerBI: Data Modelling and Visualization [Download Here](https://www.microsoft./power-bi/downloads)
- GitHub: Portfolio Building [Sign up](https://github.com/)

### Data Cleaning and Preparations
To clean and prepare the data for analysis, the following actions were performed;
1. Data loading and inspection
2. Duplicate removing

### Exploratory Data Analysis
The data was explored to answer some questions such as;
1. What are the top-selling products
2. How do the regions perform
3. What is the monthly sales trend

### Data Analysis
- ### Microsoft Excel
![Screenshot 2024-11-05 222415](https://github.com/user-attachments/assets/09e0da2f-16a9-48e6-801b-f566c043d472)

![image](https://github.com/user-attachments/assets/83b9944d-9982-4281-b27b-5110661e4b20)
 
![image](https://github.com/user-attachments/assets/9a35f3d9-54fa-4f73-bb44-e054f1895980)

``` EXCEL FORMULA
AVERAGE SALES PER PRODUCT
Gloves = AVERAGEIF(C2:D9922, "Gloves", H2:H9922)
Hat    = AVERAGEIF(C2:D9922, "Hat", H2:H9922)
Jacket = AVERAGEIF(C2:D9922, "Jacket", H2:H9922)
Shirt  = AVERAGEIF(C2:D9922, "Shirt", H2:H9922)
Shoes  = AVERAGEIF(C2:D9922, "Shoes", H2:H9922)
Socks  = AVERAGEIF(C2:D9922, "Socks", H2:H9922)

TOTAL REVENUE BY REGION
NORTH = SUMIF(D2:D9922,"North",H2:H9922)
SOUTH = SUMIF(D2:D9922,"South",H2:H9922)
EAST  = SUMIF(D2:D9922,"East",H2:H9922)
WEST  = SUMIF(D2:D9922,"West",H2:H9922)
```
- ### SQL QUERIES
``` SQL
SELECT * FROM [dbo].[Sales_Data]

-----Retrieve the total sales for each product category--------
SELECT PRODUCT, SUM(Total_Sales) as TotalSales
   FROM Sales_Data
     GROUP BY PRODUCT

--------find the number of sales transactions in each region-------
SELECT REGION, COUNT(OrderID) as Num_of_SaleTransaction
   FROM Sales_Data
     GROUP BY REGION

-----find the highest-selling product by total sales value------
SELECT top (1) PRODUCT, SUM(Total_Sales) as TotalSales
   FROM Sales_Data
     GROUP BY PRODUCT
	 
--------calculate total revenue per product----------
SELECT PRODUCT, SUM(Total_Sales) as TotalRevenue
   FROM Sales_Data
	GROUP BY PRODUCT

--------calculate monthly sales totals for the current year-----------
SELECT Month(OrderDate) AS Month,
    SUM(Total_Sales) AS MonthlySalesTotal
      FROM Sales_Data WHERE YEAR(OrderDate) = 2024
       GROUP BY Month(OrderDate)
         ORDER BY Month

---------find the top 5 customers by total purchase amount--------
SELECT TOP (5) Customer_Id, SUM (Total_Sales) as TotalPurchaseAmount
  FROM Sales_Data
    GROUP BY Customer_Id
	 ORDER BY SUM(Total_Sales) desc

-------calculate the percentage of total sales contributed by each region-------
SELECT Region, SUM(Total_Sales) AS RegionTotalSales,
FORMAT(ROUND((SUM(Total_Sales) / CAST((SELECT SUM(Total_Sales) FROM Sales_Data) AS DECIMAL(10,2)) * 100), 1), '0.#') 
AS PercentageOfTotalSales
FROM sales_data
GROUP BY Region
---------identify products with no sales in the last quarter------
SELECT PRODUCT FROM Sales_Data
GROUP BY Product
HAVING SUM(CASE 
WHEN OrderDate BETWEEN '2024-06-01' AND '2024-08-31' 
THEN 1 ELSE 0 END) = 0
```
