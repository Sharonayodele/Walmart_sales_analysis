# Walmart Sales Analysis

## About
"In this recruiting competition, job-seekers are provided with historical sales data for 45 Walmart stores located in different regions. Each store contains many departments, and participants must project the sales for each department in each store." [source](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting)

## Aim Of The Project
This project aims to explore Walmart Sales data to understand some metrics including:
- Top-performing branches and products
- Sales trends of different products, and
- Customer behavior.

## Objective
The objectives are to answer questions using the data to extract insight into sales performance and provide recommendations on how to improve and optimize it. 
The dataset was obtained from the [Kaggle Walmart Sales Forecasting Competition](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting).

## About the Data

The dataset was obtained from the [Kaggle Walmart Sales Forecasting Competition](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting). This dataset contains sales transactions from three different branches of Walmart, respectively located in Mandalay, Yangon, and Naypyitaw. The data contains 17 columns and 1000 rows:

| Column                  | Description                             | Data Type      |
| :---------------------- | :-------------------------------------- | :------------- |
| invoice_id              | Invoice of the sales made               | VARCHAR(30)    |
| branch                  | Branch at which sales were made         | VARCHAR(5)     |
| city                    | The location of the branch              | VARCHAR(30)    |
| customer_type           | The type of the customer                | VARCHAR(30)    |
| gender                  | Gender of the customer making purchase  | VARCHAR(10)    |
| product_line            | Product line of the product sold        | VARCHAR(100)   |
| unit_price              | The price of each product               | DECIMAL(10, 2) |
| quantity                | The amount of the product sold          | INT            |
| VAT                     | The amount of tax on the purchase       | FLOAT(6, 4)    |
| total                   | The total cost of the purchase          | DECIMAL(10, 2) |
| date                    | The date on which the purchase was made | DATE           |
| time                    | The time at which the purchase was made | TIMESTAMP      |
| payment_method          | The total amount paid                   | DECIMAL(10, 2) |
| cogs                    | Cost Of Goods sold                      | DECIMAL(10, 2) |
| gross_margin_percentage | Gross margin percentage                 | FLOAT(11, 9)   |
| gross_income            | Gross Income                            | DECIMAL(10, 2) |
| rating                  | Rating                                  | FLOAT(2, 1)    |


## Business Questions To Answer

### Generic Question

1. How many unique cities does the data have?
2. In which city is each branch?

### Product

1. How many unique product lines does the data have?
2. What is the most common payment method?
3. What is the most selling product line?
4. What is the total revenue by month?
5. What month had the largest COGS?
6. What product line had the largest revenue?
5. What is the city with the largest revenue?
6. What product line had the largest VAT?
7. Fetch each product line and add a column to those product lines showing "Good", "Bad". Good if its greater than average sales
8. Which branch sold more products than the average product sold?
9. What is the most common product line by gender?
12. What is the average rating of each product line?

### Sales

1. What is the number of sales made at each time of the day per weekday? 
2. Which of the customer types brings the most revenue?
3. Which city has the largest tax percentage/ VAT (**Value Added Tax**)?
4. Which customer type pays the most in VAT?

### Customer

1. How many unique customer types does the data have?
2. How many unique payment methods does the data have?
3. Which customer type buys the most?
4. What is the gender of most of the customers?
5. What is the gender distribution per branch?
6. Which time of the day do customers give the most ratings?
7. Which time of the day do customers give the most ratings per branch?
8. Which day of the week has the best average ratings?

## Workflow

1. **Data Cleaning:** This is the first step where the data is inspected to ensure **NULL** values and missing values are detected and data replacement methods are applied. Fortunately, there are no NULL values.

2. **SQL Database creation**
> 1. Build the database "walmartsalesdata"
> 2. Create a table and insert the data.
> 3. Select columns with null values in them. There are no null values in our database.

3. **Feature Engineering:** This will help us generate new columns from existing ones.
> A. Add a new column named `time_of_day` converting the time to Morning, Afternoon, and Evening. This will help answer the question of which part of the day most sales are made.

![Added a new column 'time of day'](media/pics/walmartsalessql_featureeng1.PNG)

> B. Add a new column named `day_name` that contains the extracted days of the week on which the given transaction took place (Mon, Tue, Wed, Thur, Fri). This will help answer the question of which week of the day each branch is busiest.

![Added a new column 'day_name'](media/pics/walmartsalessql_featureeng_dayname.PNG)

> C. Add a new column named `month_name` that contains the extracted months of the year on which the given transaction took place (Jan, Feb, Mar). To determine which month of the year has the most sales and profit.

![Added a new column 'month_name'](media/pics/walmartsalessql_featureeng_monthname.PNG)


4. ### Data analysis
The data analysis is divided into 3 parts:
#### 1. Product Analysis
> Analyze the data to understand the different product lines, the product lines performing best, and the product lines that need to be improved.

1. How many unique product lines does the data have?
   
   ![Answer](media/pics/walmartsales_sql_prdctq1.PNG)
   > There are 6 unique product lines.
   
2. What is the most common payment method?
   
   ![Answer](media/pics/walmartsales_sql_prdctq2.PNG)
   > The most common payment method is Ewallet.
   
3. What is the highest-selling product line?
   
   ![Answer](media/pics/walmartsales_sql_prdctq3.PNG)
  > The highest-selling product line is Fashion accessories.

4. What is the total revenue by month?
   
   ![Answer](media/pics/walmartsales_sql_prdctq4.PNG)
   
5. What month had the largest COGS?
   
   ![Answer](media/pics/walmartsales_sql_prdctq5.PNG)
   
6. What product line had the largest revenue?
   
  ![Answer](media/pics/walmartsales_sql_prdctq6.PNG)

7. What is the city with the largest revenue?
   
   ![Answer](media/pics/walmartsales_sql_prdctq7.PNG)
   
8. What product line had the largest VAT?
   
   ![Answer](media/pics/walmartsales_sql_prdctq8.PNG)
   
9. Which branch sold more products than the average product sold?
    
    ![Answer](media/pics/walmartsales_sql_prdctq10.PNG)
  
10. What is the most common product line by gender?
    
    ![Answer](media/pics/walmartsales_sql_prdctq11.PNG)
    
11. What is the average rating of each product line?
    
    ![Answer](media/pics/walmartsales_sql_prdctq12.PNG)


#### 2. Sales Analysis
> This analysis aims to answer the question of product sales trends. The result of this can help us measure the effectiveness of the sales strategies the business applied.

1. What is the number of sales made at each time of the day per weekday?
   
   ![Answer](media/pics/walmartsales_sql_salesq1.PNG)

   ![Answer](media/pics/walmartsales_sql_salesq1.5.PNG)
   
2. Which of the customer types brings the most revenue?
   
   ![Answer](media/pics/walmartsales_sql_salesq2.PNG)
   
3. Which city has the largest tax percentage/ VAT (**Value Added Tax**)?

   ![Answer](media/pics/walmartsales_sql_salesq3.PNG)
   
5. Which customer type pays the most in VAT?

   ![Answer](media/pics/walmartsales_sql_salesq4.PNG)

#### 3. Customer Analysis
> This analysis aims to uncover the different customer segments, purchase trends, and the profitability of each customer segment.

1. How many unique customer types does the data have?

   ![Answer](media/pics/walmartsales_sql_cstmr1.PNG)
   
2. How many unique payment methods does the data have?

   ![Answer](media/pics/walmartsales_sql_cstmr2.PNG)

3. Which customer type buys the most?

   ![Answer](media/pics/walmartsales_sql_cstmr3.PNG)
   
4. What is the gender of most of the customers?

   ![Answer](media/pics/walmartsales_sql_cstmr4.PNG)
   
5. What is the gender distribution per branch?

    ![Answer](media/pics/walmartsales_sql_cstmr5.PNG)
    
6. Which time of the day do customers give the most ratings?

    ![Answer](media/pics/walmartsales_sql_cstmr6.PNG)
    
7. Which time of the day do customers give the most ratings per branch?

    ![Answer](media/pics/walmartsales_sql_cstmr7.PNG)
    
8. Which day of the week has the best average ratings?

    ![Answer](media/pics/walmartsales_sql_cstmr7.PNG)


## Data Analysis

## Revenue And Profit Calculations


|$COGS = unitsPrice * quantity$                                                                | 
|VAT = 5\% * COGS$                                                                             |

$VAT$ is added to the $COGS$ and this is what is billed to the customer.

$ total(gross_sales) = VAT + COGS $

$ grossProfit(grossIncome) = total(gross_sales) - COGS $

**Gross Margin** is gross profit expressed in percentage of the total(gross profit/revenue)

$ \text{Gross Margin} = \frac{\text{gross income}}{\text{total revenue}} $

<u>**Example with the first row in our DB:**</u>

**Data given:**

- $ \text{Unite Price} = 45.79 $
- $ \text{Quantity} = 7 $

$ COGS = 45.79 * 7 = 320.53 $

$ \text{VAT} = 5\% * COGS\\= 5\%  320.53 = 16.0265 $

$ total = VAT + COGS\\= 16.0265 + 320.53 = $336.5565$

$ \text{Gross Margin Percentage} = \frac{\text{gross income}}{\text{total revenue}}\\=\frac{16.0265}{336.5565} = 0.047619\\\approx 4.7619\% $
