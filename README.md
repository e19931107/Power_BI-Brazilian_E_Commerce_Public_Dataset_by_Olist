# Power_BI-Brazilian_E_Commerce_Public_Dataset_by_Olist

## Source 
https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

## About Dataset
This is a Brazilian ecommerce public dataset of orders made at Olist Store. The dataset has information of 100k orders from 2016 to 2018 made at multiple marketplaces in Brazil. Its features allow viewing an order from multiple dimensions: from order status, price, payment, and freight performance to customer location, product attributes, and finally reviews written by customers. We also released a geolocation dataset that relates Brazilian zip codes to lat/lng coordinates.

This is real commercial data, it has been anonymized, and references to the companies and partners in the review text have been replaced with the names of Game of Thrones great houses.

I chose 2017 as bais because 2016 and 2018 data are not complete.
There are 4 pages,

## Result
I divided the dashboard into 4 parts: Overview, Order, Product and Map.

### Overview
This page can help sales or manager to check the whole sales status in 2017.

Therefore, this page contains key KPI.
![image](https://github.com/e19931107/Power_BI-Brazilian_E_Commerce_Public_Dataset_by_Olist/assets/50692450/a10ce187-6148-4eee-b52a-e312273df55c)

### Order
This page can provide order status, lead time and scatter chart of lead time and review score.
![image](https://github.com/e19931107/Power_BI-Brazilian_E_Commerce_Public_Dataset_by_Olist/assets/50692450/91a6aab9-3717-4483-ac46-5b58862caad5)

### Product
Product view to check the performance, including Pareto Chart.
![image](https://github.com/e19931107/Power_BI-Brazilian_E_Commerce_Public_Dataset_by_Olist/assets/50692450/5dfc23bf-1095-4f24-b9fc-38d450a4a8fb)

### Map
Since the data provide some information about latitude and longitude, so I built a page to show performance by status and city view.
![image](https://github.com/e19931107/Power_BI-Brazilian_E_Commerce_Public_Dataset_by_Olist/assets/50692450/3acf5d47-e93a-4076-9e1d-eb695daed4f9)

## Table
I built two tables, Pareto Chart in paroduct page and State and code for map page.

### Pareto Chart
![image](https://github.com/e19931107/Power_BI-Brazilian_E_Commerce_Public_Dataset_by_Olist/assets/50692450/4cb38083-a1cf-481a-b7f6-bf3e0846ccb7)

Here are the DAX I used in Pareto Chart:
Avg Price = AVERAGE([Price])

Avg Transaction = AVERAGE([Count])

Avg Value = AVERAGE([Value])

Count = CALCULATE(
    COUNTROWS('olist_order_items_dataset'),
    FILTER('olist_products_dataset',
    'olist_products_dataset'[product_category_name] = 'Pareto Chart'[product_category_name]))

Cumulative = 
    VAR cur_rate = [Percentage]
    RETURN CALCULATE([TTL count],FILTER(ALL('Pareto Chart'),[Percentage] >=cur_rate))

Cumulative % = DIVIDE([Cumulative],SUM('Pareto Chart'[Count]))

Percentage = DIVIDE([Count],CALCULATE([TTL count],ALL('Pareto Chart')))

Price = CALCULATE(AVERAGE(olist_order_items_dataset[price]), FILTER('olist_products_dataset','olist_products_dataset'[product_category_name] = 'Pareto Chart'[product_category_name]))

Pareto Chart = DISTINCT('olist_products_dataset'[product_category_name])

TTL count = SUM('Pareto Chart'[Count])

Value = [Count]*[Price]

### State and code
Since the city and state code in raw data is abbreviation, so I checked the website for abbreviation and the whole stats name.
![image](https://github.com/e19931107/Power_BI-Brazilian_E_Commerce_Public_Dataset_by_Olist/assets/50692450/46f52244-aaf7-4ec2-a88e-489012f0bab5)

## DAX
% delivered success = DIVIDE('Measure'[TTL delivered],'Measure'[TTL order])

Average Customer value = DIVIDE('Measure'[TTL Revenue],'Measure'[TTL customer])

Average Flight Cost = DIVIDE('Measure'[TTL Flight Cost],'Measure'[TTL order])

Average Order Value = DIVIDE('Measure'[TTL Revenue],'Measure'[TTL order])

TTL customer = DISTINCTCOUNT('olist_customers_dataset'[customer_id])

TTL delivered = CALCULATE(COUNT(olist_orders_dataset[order_status]),'olist_orders_dataset'[order_purchase_timestamp].[Year] = 2017, 'olist_orders_dataset'[order_status] = "delivered")

TTL Flight Cost = CALCULATE(SUM('olist_order_items_dataset'[freight_value]), FILTER('olist_orders_dataset', 'olist_orders_dataset'[order_purchase_timestamp].[Year] =2017))

TTL order = CALCULATE(COUNT(olist_orders_dataset[order_status]),'olist_orders_dataset'[order_purchase_timestamp].[Year] = 2017)

TTL Revenue = CALCULATE(SUM('olist_order_payments_dataset'[payment_value]), FILTER('olist_orders_dataset', 'olist_orders_dataset'[order_purchase_timestamp].[Year] =2017))
