# Sales Revenue Analysis Using Power BI





## Project Overview

- Analysing past sales over time period of 4 years for Shopee selling multiple products focusing on LAC region (Colombia, Chile, Mexico, Chile)
- Analysing the sales performance of different product categories to identify which categories will increase company's revenue
- Data is analysed using Power BI

## Business Objectives
- To analyse which categories of products have the best sales performance and how they are affected by country, customer gender, age and income
- Identify which customer base to enhance customer experience and recommend relevant products to customers and increase revenue

## Questions to guide the analysis
- Which country brings in the highest revenue?
- Which product category has highest revenue?
- Which product category has the highest quantity of sales?
- Which periods bring in the most sales in terms of quantity and profit?
- Are the products sales performance affected by discount, lead time or other factors?

## Data Preparation

##### Overview of the dataset
* The original data source is from Canvas in this LINK: https://ntuc.instructure.com/courses/20951/files/645709?module_item_id=285701

* There are 2 datasets provided:
  - Customer.csv file where the order came from, which shows the customer demographics such as age, country, name, gender and income, and 
  - Purchase.csv file showing purchase price of different product names, with information on discount, tax, quantity and shipping cost for each order.
* Both datasets are extracted from .csv files using Power BI where some data cleaning was done.  
* As part of the data cleaning, Pandas was also used as it was deemed quicker to determine the number of rows and columns, and to check for null values in each dataset.
* In the customer.csv file, there are 1000 rows and 7 columns, no nulls are detected. 

![image](https://github.com/leowmc/leowmc/assets/144865130/b113f88b-e963-48ed-8523-7a7520e0f58c)

![image](https://github.com/leowmc/leowmc/assets/144865130/2d83d255-f010-4084-b8dd-348a3ce5c634)

* In the purchase.csv file, there are 50000 rows with 11 columns, and no nulls are detected. 

![image](https://github.com/leowmc/leowmc/assets/144865130/88d440b1-e74b-46b6-b732-bf1a56f8d666)

![image](https://github.com/leowmc/leowmc/assets/144865130/4cda714f-f8cb-44f3-b2e2-6d33be6c50ba)

* Continue data preparation and cleaning in Power BI.

* In the customer table, merge columns first and last name under transform tab, and rename as ‘Full Name’ in customer table. Remove columns for first_name and last_name.
  
  ![image](https://github.com/leowmc/leowmc/assets/144865130/a3921bf1-096b-4fc8-b930-9b5db8731313)
  
* In the purchase table,
  - Rename table as ‘Sales’
  - Change the Data Type of price and shipping cost to fixed decimal number.
  
  ![image](https://github.com/leowmc/leowmc/assets/144865130/2b4027b2-4eea-40e8-a747-3596df6b57e4)

  - Added column ‘Sales’ using formula: sales = Sales[price] * Sales[quantity]
  - Added column ‘Lead Time’ using formula: Lead Time = DATEDIFF(Sales[order_date], Sales[shipping_date], DAY)
  
  ![image](https://github.com/leowmc/leowmc/assets/144865130/314dbe89-f25e-4aa6-88cc-ab59f9dc448d)
  
  ![image](https://github.com/leowmc/leowmc/assets/144865130/6e5c34d1-159b-4e4e-be25-bde94934f585)
  
  
* Following dataset will be omitted and removed in the analysis:
  - Sales dataset after 31/12/2022 will be omitted in the analysis as there are incomplete dataset in 2023 (only 44 filtered rows from 1 Jan 2023)
  
  ![image](https://github.com/leowmc/leowmc/assets/144865130/1bbc7386-22f0-4ca5-86d1-74cc748d9585)
  
  - Sales dataset in Aug 2019 will be removed as data is incomplete, as order date only spanning from 15/8/2019 to 31/8/2019, total 694 rows. 
  
  ![image](https://github.com/leowmc/leowmc/assets/144865130/6912fc22-c4d5-457c-aa6c-c1b34d285918)
  
      
* Create 3 new tables:
  - Add Table ‘Category’ to identify any sales pattern from the drilldown of the 30 product_names.
  - Add a table for ‘Date’ using Date = CALENDAR(DATE(2019,9,1),DATE(2022,12,31))
  - Add a table for ‘Income Group’
  - Manage relationships in the Data Model for the new tables.
 
    <img width="328" alt="image" src="https://github.com/leowmc/Capstone-Project/assets/144865130/70179954-25db-44f2-84d8-76384b14b44c">
    <img width="171" alt="image" src="https://github.com/leowmc/Capstone-Project/assets/144865130/cc955b21-0580-464f-a154-53a8d52b7fce">

* In the Sales table, create 2 new measures :
  - Add a new measure for Purchase Frequency to determine the number of appearances of the customers within the period
    - Purchase Frequency = COUNTROWS('Sales')
  - Add a new measure for Customer Purchase Quantity (Cus_PurchaseQty) to determine the total number of quantity of products each of the customers purchased within the period
    - Cus_PurchaseQty = SUMX('Sales', Sales[quantity])
   
--

## Data Analysis & Findings









