# 🚗 Exploring Trends Using SQL 📊

## 📖 Overview
This project explores data trends in a fictional dataset of cars (`car_info`) using SQL. It includes advanced queries to analyze selling prices, mileage, ownership trends, and more. Additionally, a **Sales Dashboard** was created using **Power BI** and **SQL**, with raw data sourced from **Microsoft Excel**.

## 📊 Dataset Details
The `car_info` dataset contains the following fields:
- **Name**: Car model name.
- **selling_price**: Selling price of the car.
- **mileage**: Mileage of the car in km/l.
- **fuel**: Fuel type (e.g., Petrol, Diesel).
- **transmission**: Type of transmission (Manual/Automatic).
- **owner**: Ownership details (e.g., First Owner, Second Owner).
- **year**: Year of manufacture.
- **km_driven**: Total kilometers driven.
- **seats**: Number of seats in the car.

## 🚀 Queries and Insights
### 1️⃣ **Average Selling Price by Fuel Type**  
Calculate the average selling price for manual transmission cars owned by the first owner, grouped by fuel type.
```sql
SELECT fuel, AVG(selling_price) AS avg_selling_price
FROM car_info
WHERE transmission = 'Manual' AND owner = 'First Owner'
GROUP BY fuel;

#### 2️⃣ **Top 3 Car Models with Highest Average Mileage** 🚘  
Identify car models with more than 5 seats and the highest average mileage.
```sql
SELECT Name, AVG(mileage) AS avg_mileage
FROM car_info
WHERE seats > 5
GROUP BY Name
ORDER BY avg_mileage DESC
LIMIT 3;









