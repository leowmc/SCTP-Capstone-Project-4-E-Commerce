# Shopee Sales Analysis Using Power BI

<img width="800" alt="image" src="https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/289b00d5-79b9-4416-bc48-ec72be7570e4"> <br />



An interactive dashboard was created showing the sales and sum of quantity by product category and product names. Additionally there are filters to filter the dashboard by country, dates, customer age, income group for further analysis. The dashboard can be accessed from downloading _**Shopee Sales Report 2019-2022.pbix**_.

<img width="1000" alt="image" src="https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/3ed8eb6a-272b-4281-a8b8-83bb74832ea3"> <br />


## Project Overview

- Analysing past sales over time period of 4 years for Shopee selling multiple products focusing on LAC region (Colombia, Chile, Mexico, Chile)
- Analysing the sales performance of different product categories to identify which categories will increase company's revenue
- Data is analysed using Power BI

<br />

## Business Objectives
- As a data analyst from Shopee, my task is to analyse which categories of products have the best sales performance and how they are affected by country, customer gender, age and income
- Identify which customer base to enhance customer experience and recommend relevant products to customers and increase revenue

<br />

## Questions to guide the analysis
- Which country brings in the highest revenue?
- Which product category has highest revenue?
- Which product category has the highest quantity of sales?
- Which periods bring in the most sales in terms of quantity and profit?
- Are the products sales performance affected by discount, lead time, age group, income or other factors?

<br />

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
    
    <img width="200" alt="image" src="https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/b16ebb0a-f84e-4894-95d3-2b4ae0dbbf8d">
    
    <img width="200" alt="image" src="https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/5c315ffa-4a6c-40af-ad13-98f083b1b8cc">



* In the purchase table,
  - The purchase table is renamed as Sales.
  - Change the Data Type of price and shipping cost to fixed decimal number.
  - Order_date spanning from 15 Aug 2019 to 1 Jan 2023. 
    - Sales dataset after 31/12/2022 will be omitted in the analysis as there are incomplete dataset in 2023 (only 44 filtered rows from 1 Jan 2023)
  
    ![image](https://github.com/leowmc/leowmc/assets/144865130/1bbc7386-22f0-4ca5-86d1-74cc748d9585)
  
    - Sales dataset in Aug 2019 will be removed as data is incomplete, as order date only from 15/8/2019 to 31/8/2019, total 694 rows.
    - Final number of rows in Sales table become 49262.
  
    ![image](https://github.com/leowmc/leowmc/assets/144865130/6912fc22-c4d5-457c-aa6c-c1b34d285918)
    
  - For deep dive analysis, following 2 new columns and 2 new measures are added :
    - Added new column ‘Sales’ using formula: sales = Sales[price] * Sales[quantity]
    - Added new column ‘Lead Time’ using formula: Lead Time = DATEDIFF(Sales[order_date], Sales[shipping_date], DAY)
  
    ![image](https://github.com/leowmc/leowmc/assets/144865130/314dbe89-f25e-4aa6-88cc-ab59f9dc448d)
  
    ![image](https://github.com/leowmc/leowmc/assets/144865130/6e5c34d1-159b-4e4e-be25-bde94934f585)
 
    - Added new measure for Purchase Frequency to determine the number of appearances of the customers within the period
      - Purchase Frequency = COUNTROWS('Sales')
    - Added new measure for Customer Purchase Quantity (Cus_PurchaseQty) to determine the total number of quantity of products each of the customers purchased within the period
      - Cus_PurchaseQty = SUMX('Sales', Sales[quantity])

  
* Create 2 new tables:
  - Added a table for ‘Category’ to group the 30 product_names into their respective product categories to identify any sales pattern
  - Added a table for ‘Date’ using Date = CALENDAR(DATE(2019,9,1),DATE(2022,12,31))

<br />

## Data Analysis & Findings

#### 1. Total Sales by country
* Colombia had the highest sales among the region, amounting to $97 million, followed by Chile, Mexico, and Brazil with sales at $80 million.
* In terms of sales quantity, Colombia accounted for 28% of the total sales, with 74K units sold. Chile, Brazil, and Mexico followed in terms of sales quantity

<img width="500" alt="image" src="https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/7c5803a0-bcb3-43c1-a5a6-1b190ba3d83f">


#### 2. Total Sales by Year, Quarter and Month and Country
* Brazil’s sales trend closely aligns with the average line between September 2019 and December 2022.
* Although Colombia has the highest sales, there is a sign of an 8.3% downtrend between September 2019 and December 2022, which is a concern.
* Chile, the second-highest in sales, shows positive signs with sales trending up gradually from September 2019 to December 2022. In Q4 2022, revenue exceeds that of Colombia.
* Mexico also shows a slight downtrend in sales over time between September 2019 to December 2022

<img width="800" alt="image" src="https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/d0382631-7c9b-497d-8f11-469d508ba3dd">

<img width="800" alt="image" src="https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/b87aec1b-267b-4d10-ad15-6d0e246a8564">


#### 3. Total Sales and Quantity of Category and Products
* The top four product categories contributing to total sales across the four countries are Home Décor, Home Furniture, Kitchen Appliances, and Electronic Devices.
* Home Decor had the highest sales at $140 million and was the second-highest in sales quantity at 54K units.
* Apparel had the highest sales quantity at 90K units but had the second-lowest total sales at approximately $14 million. This can be attributed to fast fashion driving consumer demand to buy new clothing items excessively at low prices.

<img width="800" alt="image" src="https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/463bf280-d199-46a5-8f9b-ce253548066b">


#### 4. Total Sales Revenue by Category & Product_Names
* The bulk of Shopee sales from the 4 countries are generated from home related products. Approximately 67% of the total Sales are from Home Décor, Home Furniture and Kitchen Appliances.
* When drilling down by product name, the top 10 products are home-related products with total sales in the range of $22 million to $24 million. On the other hand, total sales from other products like Electronic Devices and Apparel are around $10 million and below.
* When filter by country, the top 10 products across the four countries are similar in terms of total sales.

<img width="800" alt="image" src="https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/ee43dba4-11f8-4bc5-9beb-76b32b1371d8">


#### 5. Sum of Quantity by Product_Names
* Apparel has highest sales quantity at 90K, followed by Home Décor at 54K.  The rest of the products have quantities under 30K.
* By filtering by Country, the top three product categories show similarities in terms of total Sales.
* Combining all home-related products from Home Décor, Home Furniture, and Kitchen Appliances, the sales quantity is equivalent to that of Apparel at 90K.
* The difference between the highest and lowest quantity products is 0.6K, which is statistically not significant. However, the ranking of the products varies among the four countries.

#### 6. Sales by Income Group and country
* Colombia and Chile show top sales coming from the lower medium income group ($30,000 - $60,000), while Mexico’s top sales come from these two income groups ranging from $30,000 to $90,000. Only Brazil’s top sales come from the highest income group ($120,000 - $150,000).
* In general, both Colombia and Chile have their top sales coming from the age group of 45-54 years old, while Brazil’s top sales come from the age group of 35-44 and Mexico’s from the age group of 55-64.
* For Chile, the top sales from the income group of $30,001-$60,000 are dominated by younger adult age group of 25-34 years old. The youth group and younger senior age group (55-64) also see higher sales.
* For Colombia, the top sales from the income group of $30,001-$60,000 are dominated by adult age group of 45-54 years old, followed by age groups of 35-44 and 25-34. These three age groups showed declining sales from 2020 to 2022.
* It was observed that except Brazil, the higher income groups from Colombia, Chile and Mexico seem to spend less than the lower medium income group $30000 - $60000.
* The bulk of the product items purchased by all age groups in these four countries come from the top three product categories: Home Décor, Home Furniture, and Kitchen Appliances.

<img width="1000" alt="image" src="https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/86c14bee-b9cb-46c9-8a25-b3e114b32770">


#### 7. Customer Purchase frequency and quantity behaviour over time
* Colombia and Mexico are experiencing a sales downtrend over time, which aligns with the decreasing trend of customer purchase frequency and quantity.
  - When drilling down by age group for Colombia, the purchase frequency and quantity from all age groups show a declining trend over time, except for the age group of 35-44.
* Similarly, for Chile, the sales uptrend over time follows the increasing trend of purchase frequency and quantity.
  - When drilling down by age group, the purchase frequency and quantity from all age groups show an increasing trend over time, except for the Youth age group showing a slight decline.
* Mexico’s slight decline in sales over the years is mainly driven by less purchase frequency and quantity from the adult age group of 35-44, as well as the Youth and Seniors age groups.
* Brazil shows a positive increase in sales from Youths over time, offset the decline in sales from some adult age groups.

<img width="800" alt="image" src="https://github.com/leowmc/SCTP-Capstone-Project-4-E-Commerce/assets/144865130/73924b6b-229a-4d15-8b74-f5b2463b25fc">


<br />

## Key Insights
**1. Optimize Product Offerings**
  - The bulk of the product items purchased by all age groups in these four countries come from the top three product categories: Home Décor, Home Furniture, and Kitchen Appliances.
  - Businesses operating in these sectors can focus on optimizing their offerings within these categories to capitalize on this demand.

<br />

**2. Identify Opportunities for Improvement**
  - Colombia and Mexico are experiencing a downtrend in sales over time, which aligns with the decreasing trend of customer purchase frequency and quantity. 
  - Further analysis is required to understand the underlying factors contributing to the decline in sales and customer behaviour over time. 

<br />

**3. Targeting Specific Age Group and Income Group**
  - Understanding the income-specific or age-specific trends in customer behaviour can help businesses tailor their marketing strategies accordingly. For examples :
    - Businesses can attract more higher income groups to spend more by creating a premium brand as higher-income groups are more likely to purchase products from brands that they perceive as premium. 
    - Chile shows an increasing trend of purchase frequency and quantity across all adult age groups. This suggests that businesses operating in Chile may benefit from targeting specific age groups using targeted advertising        to capitalize on this increasing trend. 








