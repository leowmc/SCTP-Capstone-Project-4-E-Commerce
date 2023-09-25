# Sales Revenue Analysis Using Power BI

<img width="1000" alt="image" src="https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/ca62c228-6046-4a44-be0a-4b5372763ac3">



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
- Are the products sales performance affected by discount, lead time, age group, income or other factors?

## Data Preparation

##### Overview of the dataset
* The original data source is from Canvas in this LINK: https://ntuc.instructure.com/courses/20951/files/645709?module_item_id=285701

* There are 2 datasets provided:
  - Customer.csv file where the order came from, which shows the customer demographics such as age, country, name, gender and income, and 
  - Purchase.csv file showing purchase price of different product names, with information on discount, tax, quantity and shipping cost for each order.
* Both datasets are imported from .csv files using Power BI where some data cleaning is done.  
* From the column profile in the View tab, Customer dataset contains 1000 rows and 7 columns, while Purchase dataset contains 50000 rows and 11 columns. No nulls/errors/duplicates are detected.
  
<img width="800" alt="image" src="https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/687f471b-7436-4445-9510-c80ccac01bba">

<img width="800" alt="image" src="https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/e2650046-349f-4cd7-b981-8cea51bdcbdd">

* In the customer table,
  - Merge columns first_name and last name under transform tab, and rename as ‘Full Name’ before removing columns for first_name and last_name.

     ![image](https://github.com/leowmc/leowmc/assets/144865130/a3921bf1-096b-4fc8-b930-9b5db8731313)

  - For deep dive analysis, 2 new columns are added by merging queries, one is the Age Group to bin the different age groups, and the other is the Income Group binned according to the different income group.

    <img width="800" alt="image" src="https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/93885680-23d3-442d-9c7a-2a46d590d013">


* In the purchase table,
  - The purchase table is renamed as Sales.
  - Change the Data Type of price and shipping cost to fixed decimal number.
  - Order_date spanning from 15 Aug 2019 to 1 Jan 2023. 
    - Sales dataset after 31/12/2022 will be omitted in the analysis as there are incomplete dataset in 2023 (only 44 filtered rows from 1 Jan 2023)
  
    ![image](https://github.com/leowmc/leowmc/assets/144865130/1bbc7386-22f0-4ca5-86d1-74cc748d9585)
  
    - Sales dataset in Aug 2019 will be removed as data is incomplete, as order date only from 15/8/2019 to 31/8/2019, total 694 rows.
    - Final number of rows become 49262.
  
    ![image](https://github.com/leowmc/leowmc/assets/144865130/6912fc22-c4d5-457c-aa6c-c1b34d285918)
    
  - For deep dive analysis, following new columns and measures are added :
    - Added column ‘Sales’ using formula: sales = Sales[price] * Sales[quantity]
    - Added column ‘Lead Time’ using formula: Lead Time = DATEDIFF(Sales[order_date], Sales[shipping_date], DAY)
  
    ![image](https://github.com/leowmc/leowmc/assets/144865130/314dbe89-f25e-4aa6-88cc-ab59f9dc448d)
  
    ![image](https://github.com/leowmc/leowmc/assets/144865130/6e5c34d1-159b-4e4e-be25-bde94934f585)
 
   - Add a new measure for Purchase Frequency to determine the number of appearances of the customers within the period
      - Purchase Frequency = COUNTROWS('Sales')
    - Add a new measure for Customer Purchase Quantity (Cus_PurchaseQty) to determine the total number of quantity of products each of the customers purchased within the period
      - Cus_PurchaseQty = SUMX('Sales', Sales[quantity])

  
* Create 2 new tables:
  - Add Table ‘Category’ to identify any sales pattern from the drilldown of the 30 product_names.
  - Add a table for ‘Date’ using Date = CALENDAR(DATE(2019,9,1),DATE(2022,12,31))



## Data Analysis & Findings









