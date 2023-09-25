# Sales Revenue Analysis Using Power BI

* An interactive dashboard was created showing the sales and sum of quantity by product category and product names. Additionally there are filters to filter the dashboard by country, dates, customer age, income group for further analysis. The dashboard can be accessed from this link and downloading Revenue Report.pbix.

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


--

## Data Analysis & Findings

#### 1. Total Sales by country
* At $97M, Colombia had the highest Sum of Sales among the region, followed by Chile, Mexico and Brazil which had the lowest Sum of Sales at $80M.
* At 28% of Sum of Sales, Colombia has highest Sum of Quantity at 74K, followed by Chile, Brazil and Mexico.

#### 2. Total Sales by Year, Quarter and Month and Country
* Though Colombia has the highest Sales, there is sign of downtrend (8.3%) between Sep 2019 and Dec 2022.
* Chile, the 2nd highest in Sales, is trending up gradually from Sep 2019 to Dec 2022 with Q4 2022 revenue exceeds that of Colombia.
* Mexico also shows slightly downtrend in Sales between Sep 2019 to Dec2022.
* Brazil Sales is flat between September 2019 and December 2022.

#### 3. Total Sales and Quantity of Category and Products
* The top 4 total Sales of the 4 countries are similar, mainly from the product category Home Décor, Home Furniture, Kitchen Appliances, and Electronic Devices.
* At $140M, Home Decor had the highest Sales and 2nd highest in sales quantity at 54K.
•	Although Apparel has the highest sales quantity at 90K, the total Sales is 2nd lowest at about 14M. This can be explained by fast fashion driving consumer demand to buy new clothing items in excess with low prices.

#### 4. Total Sales Revenue by Category & Product_Names
* The bulk of Shopee sales from the 4 countries are generated from home related products. About 67% of the total Sales are from Home Décor, Home Furniture and Kitchen Appliances.
* The top 10 products are home related products with Sales ranging $22M - $24M. The total Sales of other products like Electronic Devices, Apparel etc are around $10M and below.
•	The top 10 products of the 4 countries are similar with respect to total Sales.

#### 5. Sum of Quantity by Product_Names
* Apparel has highest sales quantity at 90K, followed by Home Décor at 54K and the rest are under 30K.
* By Country, the top 3 product category is similar with respect to total Sales.
* By Product Name, the difference between the highest and lowest Quantity products are 0.6K, which is statistically not significant. However, the ranking of the products varies among the 4 countries.

#### 6. Sales by Income Group and country
* From 2019-2022, Colombia and Chile show top sales coming from lower medium income group $30000 - $60000 range, while Mexico top sales come from these 2 income groups ranging $30000-$90000. Only Brazil top sales come from the highest income group $120000-$150000.
* Both Colombia and Chile top sales come from age group 45-54 yrs old, while that of Brazil from age group 35-44 and Mexico from age group 55-64.
* Further drilldown on Colombia and Chile on why top sales are coming from lower medium income group $30001-$60000:
    - For Chile, the top sales from income group $30001-$60000 are dominated by younger adult age group 25-34 with increasing sales over the years. Youth group and younger senior age group 55-64 also seeing higher sales.
    - For Colombia, the top sales from income group $30001-$60000 are dominated by adult age group 45-54, followed by age group 35-44 and 25-34. These 3 age-group showed declining sales from 2020-2022.
* The bulk of the product items purchased by all age groups in the 4 countries come from the top 3 product category (Home Décor, Home Furniture and Kitchen Appliances) which contributed to the higher sales.
  
#### 7. Customer Purchase Pattern
* The purchase frequency and customer purchase quantity follow the downtrend in the total Sales over time for Colombia and Mexico and uptrend in total Sales over time for Chile.
* For all 4 regions, it was also observed that the total Sales is consistently higher from Sep-Dec compared to other months, and this is probably due to seasonal consumer pattern related to holiday season, year-end discount, seasonal products etc which may drive up sales.

--
## Key Insights
* Colombia has highest sales and quantity ($97M, 74K), followed by Chile, Mexico and Brazil
* Sales from Colombia and Mexico shows decreasing trend over time, which follows decreasing trend of purchase frequency and quantity.
* Sales from Chile shows increasing trend over time, which follows increasing trend of purchase frequency and quantity. Sales in Q4 2022 exceed that of Colombia.
* Top 3 Product Category from the 4 countries come from ‘Home Related Products’ (Home Décor, Home Furniture, Kitchen Appliances), contributing ~67% of total sales.
* The Sum of Quantity of these ‘Home Related Products’ is equivalent to that of Apparel which has highest Sum of Quantity at 90K.
* Adults Age Group across all income groups from the 4 countries contribute the highest sales. However, sales can be driven by different age groups and income groups for the 4 countries.
  - Colombia and Chile top sales from 2nd lowest income group. 
  - Mexico top sales from medium income group.
  - Brazil top sales from highest income group.
![image](https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/5cad8462-8ba8-41b5-a5e0-342fc8ccedfb)





