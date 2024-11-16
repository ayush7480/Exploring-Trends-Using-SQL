# Exploring Trends Using SQL 🚗📊

## Overview
This project demonstrates advanced SQL techniques applied to a dataset containing information about cars (`car_info`). The queries aim to uncover insights such as average selling prices, top-performing car models, and trends over time. This repository is ideal for anyone looking to learn or practice SQL with real-world use cases.

## Dataset
The project uses a fictional `car_info` dataset with the following fields:
- **Name**: Car model name.
- **selling_price**: Selling price of the car.
- **mileage**: Mileage of the car in km/l.
- **fuel**: Fuel type (e.g., Petrol, Diesel).
- **transmission**: Type of transmission (Manual/Automatic).
- **owner**: Ownership details (e.g., First Owner, Second Owner).
- **year**: Year of manufacture.
- **km_driven**: Total kilometers driven.
- **seats**: Number of seats in the car.

## Queries and Insights
### 1. **Average Selling Price by Fuel Type**  
Calculate the average selling price for cars with manual transmission and owned by the first owner, grouped by fuel type.  
```sql
SELECT fuel, AVG(selling_price) AS avg_selling_price
FROM car_info
WHERE transmission = 'Manual' AND owner = 'First Owner'
GROUP BY fuel;
