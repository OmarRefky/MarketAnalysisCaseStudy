# **Market Data Analysis Case Study**
- Inspected the data Data Shape, Summary Statistics, Missing values, Datatypes and the details of 4 Categorical Variables.
- Cleaned the data from 3 problems: negative prices, duplicated rows and wrong datatypes.
- Engineered 2 new features.
- Analyzed the data answering 8 questions and extracting insights using techniques such as: Pivot tables, Time series analysis and more.

------------

## Goals of the Analysis

**Given the raw data attached (dataset1) that has data from the 1st of April till the 15th of June:**

1. Calculate the total monthly retention rate for May (customers retained from April) and retention rate for every channel and state recommendations on how to enhance this KPI.


2. Calculate the percentage growth of May over April for every district in terms of number of orders, distinct retailers, average order price, total revenues (sum of order price) and highlight the top 5 and least 5 districts in terms of revenue growth. Based on the analysis, list the districts that should be capitalized on and the districts that should be shutted down and why?


3. Calculate the total monthly burn for April and May and state what techniques can to use in order to decrease the burn on discounts.


4. Calculate the weekly percentage contribution of every channel from the total weekly orders for April and May.


5. For May, based on the following criteria:

    - App users are:
      * Retailers who have at least 2 monthly delivered app orders (channel application)
      * Retailers who 75%+ of their total delivered monthly orders on the App (channel application)
    - Telesales users are:
      * Retailers who have at least 2 monthly delivered telesales orders (channel telesales)
      * Retailers who have their last delivered order channel telesales

    Based on the criteria mentioned above, calculate the total monthly percentage of App users and telesales users from the total retailers of May and mention techniques by which the app users percentage could be increased.

 

6. Calculate the projection of total sales orders and total revenues (sum of order price) for the rest of June for every retailer and hence, total June.

 

**For the raw data attached (dataset2):**

7.  Considering the Stock snapshot and the sales data per SKU, Calculate days on hand for all SKUs (time remaining till SKUs run out of stock).

 

8.  Calculate the stocks to be purchased from suppliers per SKU to reach 7 days on hand for all SKUs.

-----------

### Files
* 'dataset1.xlsx': Sales data from '2020-04-01' to '2020-06-15'.
* 'dataset2.xlsx': SKU sales counts from '2020-06-06' to '2020-06-15' in sheet 1 and stocks in sheet 2.
* 'forecast_orders.xlsx': The entire forecasted numbers of orders.
* 'forecast_revenues.xlsx': The entire forecasted Revenues.
* 'stock_days_on_hand.xlsx': Days on hand per SKU.
* 'stocks_to_purchase.xlsx': Stocks to purchase.

### Meta Data

**Orders Dataframe** ('dataset1.xlsx')

| Feature | Description | DType |  Comments |
| ----------- | ----------- | ----------- | ----------- |
| `week` | Number of the week | int64 | Starts at week 14 to week 25 |
| `month` | Number of the month | int64 | Starts at month 4 (April) |
| `creation_date` | Order date | object | Converted to date type |
| `sales_order_id` | Order ID | int64 | - |
| `retailer_id` | Retailer ID | int64 | - |
| `sales_order_status` | Order Status | object | Delivered, Canceled, Failed |
| `channel` | Channel used to order | object | Application, salesagent, telesales |
| `district_ar` | Name of the district in Arabic | object | 82 districts |
| `order_price_before_discount` | Order price before discount | float64 | - |
| `discount` | Amount of discount | float64 | - |


**Sales Dataframe** ('dataset2.xlsx', sheet 0)

| Feature | Description | DType | Comments |
| ----------- | ----------- | ----------- | ----------- |
| `Date` | Date of the record | datetime64 | - |
| `Weeek` | Number of the week | int64 | - |
| `sku` | Name of the sku in arabic | object | - |
| `Sales_Count` | Number of sold products | int64 | - |


**Stocks Dataframe** ('dataset2.xlsx', sheet 1)

| Feature | Description | DType | Comments |
| ----------- | ----------- | ----------- | ----------- |
| `sku` | Name of the sku in arabic | object | - |
| `Stock` | Number of stocked products | int64 | - |


---------------

## Conclusion

- Inspecting the data shape, summary statistics, datatypes and null values.
- Cleaned the data from negative values, Checked for outliers and fixed datatypes.
- Aggregated 2 new columns to help with the Analysis later.
- Analyzed the data to answer the goals.
1. **Retention Rate**
   + May Retention Rate = **47.477%**
   + Retention Rate per channel:
     - May Retention Rate for Application = **48.424%**
     - May Retention Rate for salesagent = **7.0%**
     - May Retention Rate for telesales = **37.197%**
     
   + **My recommendations on how retention rate could be enhanced according to what the data suggests:**
     - Monitor why the orders fail and try to maintain it regularly.
     - Monitor the sales agents performance and potentially host a training workshop for them on how to provide follow up services.
     - Try and provide more discounts whenever possible as the data shows even a small amount could have a big impact on the retention rate.
     - Facilitate and advertise bulk/big purchases.


2. **District Growth Percentage**
   + After comparing the districts across all 4 metrics, these are results:
   <table>
        <tr>
            <td> <b>Top Performing districts</b> </td><td> <b>Bottom Performing districts</b> </td><td> <b>Zero Impact districts</b> </td>
        </tr>
        <tr>
            <td> قها </td><td> أبو رواش </td><td> دار السلام </td>
        </tr>
        <tr>
            <td> بولاق </td><td> حدائق الأهرام </td><td> مدينة 15 مايو </td>
        </tr>
        <tr>
            <td> المعتمدية </td><td> المقط </td><td> الزمالك </td>
        </tr>
        <tr>
            <td> منشية ناصر </td><td> الدويقة </td><td> سريقاوس </td>
        </tr>
        <tr>
            <td> الجمالية </td><td> مدينة النهضة </td><td>  </td>
        </tr>
        <tr>
            <td> أوسيم </td><td> عمرانيه 3 </td><td>  </td>
        </tr>
        <tr>
            <td> التجمع التالت </td><td> مساكن شيراتون </td><td>  </td>
        </tr>
        <tr>
            <td>  </td><td> الوايلي </td><td>  </td>
        </tr>
        <tr>
            <td>  </td><td> ميت حلفا </td><td>  </td>
        </tr>
    </table>
    
   + My recommendations are:
     1. More investing into the Top performing districts.
        * According to the evaluation metrics these districts are growing at very decent base in many aspects which indicates a potential good investment.
     2. Shutdown the Zero impact districts.
        * These districts aren't contributing at all. Hence, its better to save resources spent there and spend them else where.
     3. Re evaluate the bottom performing districts.
        * While these districts seems like a bad investment I wouldn't recommend shutting them down purly based on these results as the data from just 1 month might be heavily skewed by outliers but it might be a good idea to keep those districts tracked.
     
     
3. **Monthly Burn**
   + Total Monthly Burn:
     * Burn Rate in April: **176390.66 EGP**
     * Burn Rate in May: **177447.55 EGP**
   + While decreasing the burn on discounts I definitely won't recommend decreasing the number of discounts as they affect retention rate as discussed earlier.
   + My recommendations to decrease monthly burn without decreasing the number of discounts:
     1. Cap the discount at a certain limit.
     2. Activate discounts only above a certain order price, hence either the order prices will increase or the burn on lower prices orders will decrease.


4. **Weekly Contribution Percentage by Channel**
   <table>
        <tr>
            <td> <b>Weekly Contribution Percentages by Channel in April</b> </td>
            <td> <b>Weekly Contribution Percentages by Channel in May</b> </td>
        </tr>
        <tr>
            <td> <img src='https://i.imgur.com/TkOFZ8C.png'> </td>
            <td> <img src='https://i.imgur.com/EMdMDYq.png'> </td>
        </tr>
    </table>


5. **Percentage of App and Telesales users**
   + According to the criteria:
     - Percentage of App users in May: **21.899**%
     - Percentage of Telesales users in May: **2.169**%
   + Techniques to increase app users:
     - Discounts for new users, this could attract new customers.
     - Referal System, where current customers can invite new customers and when the new customers make their first order through the app it gives the referal a discount.
     - Discount every X orders or after making an order worth more than X EGP.
     
     
6. **Sales orders and revenues Forcasting**
   + **Average projecting for number of orders and revenue per retailer**
    <table>
        <tr>
            <td><b><center>Projected Sales orders per retailer in June</center></b></td>
            <td><b><center>Project Revenue per retailer in June</center></b></td>
        </tr>
        <tr>
            <td><center>Total Sales Orders (Average Estimation) = <b>7183</b> Orders</center></td>
            <td><center>Total Sales Revenues (Average Estimation) = <b>21903983.43</b>EGP</center></td>
        </tr>
        <tr>
            <td> <img src='https://i.imgur.com/Saxj93x.png'> </td>
            <td> <img src='https://i.imgur.com/p2LvpwF.png'> </td>
        </tr>
    </table>
    
    + **Time Series Forecasting for number of orders and revenue**
    <img src='https://i.imgur.com/SFiyhW6.png'>
    <img src='https://i.imgur.com/KPe66x7.png'>


7. **Days on hand by stock**

![image](https://user-images.githubusercontent.com/88734429/200434761-675cee1c-6656-4497-ad27-2dd57deb179d.png)


8. **Stocks to reach 7 days on hand**

![image](https://user-images.githubusercontent.com/88734429/200434833-84c9c8c2-e39a-48c2-9faf-6dd9484c3485.png)

