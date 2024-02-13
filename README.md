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

DAX
  % delivered success = DIVIDE('Measure'[TTL delivered],'Measure'[TTL order])
