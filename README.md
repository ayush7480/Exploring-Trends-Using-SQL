# 🚗 Exploring Trends Using SQL 📊

## 📖 Overview  
This project explores trends in a fictional `car_info` dataset using advanced SQL queries. It demonstrates the use of SQL for data analysis and includes insights into selling prices, mileage, ownership patterns, and more. Additionally, a **Sales Dashboard** was created using **Power BI** and **SQL**, with raw data sourced from **Microsoft Excel**.  

---

## 🗂️ Dataset Details  
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

---

## 🔍 Queries and Insights  

### 1️⃣ **Average Selling Price by Fuel Type**  
Calculate the average selling price for manual transmission cars owned by the first owner, grouped by fuel type.  
```sql
SELECT fuel, AVG(selling_price) AS avg_selling_price
FROM car_info
WHERE transmission = 'Manual' AND owner = 'First Owner'
GROUP BY fuel;
---

### 2️⃣ **Top 3 Car Models with Highest Average Mileage**  
Identify car models with more than 5 seats and the highest average mileage.  
```sql
SELECT Name, AVG(mileage) AS avg_mileage
FROM car_info
WHERE seats > 5
GROUP BY Name
ORDER BY avg_mileage DESC
LIMIT 3;
```

---

### 3️⃣ **Price Variance Greater than $10,000**  
Find car models where the price difference exceeds $10,000.  
```sql
SELECT Name
FROM car_info
GROUP BY Name
HAVING MAX(selling_price) - MIN(selling_price) > 10000;
```

---

### 4️⃣ **Above Average Price & Below Average Mileage**  
Retrieve cars priced above the average selling price but with mileage below average.  
```sql
SELECT Name
FROM car_info
WHERE selling_price > (SELECT AVG(selling_price) FROM car_info)
    AND mileage < (SELECT AVG(mileage) FROM car_info);
```

---

### 5️⃣ **Cumulative Selling Price Over Years**  
Calculate the cumulative sum of selling prices over years for each car model.  
```sql
SELECT Name, year, selling_price, 
       SUM(selling_price) OVER (PARTITION BY Name ORDER BY year) AS cumulative_sum
FROM car_info;
```

---

### 6️⃣ **Selling Prices Within 10% of Average**  
Identify car models priced within 10% of the average selling price.  
```sql
SELECT Name, selling_price
FROM car_info
WHERE selling_price BETWEEN 
      (SELECT AVG(selling_price) * 0.9 FROM car_info) 
      AND (SELECT AVG(selling_price) * 1.1 FROM car_info);
```

---

### 7️⃣ **Exponential Moving Average (EMA)**  
Compute the EMA for each car model, considering a smoothing factor of 0.2.  
```sql
SELECT Name, year, selling_price,
       AVG(selling_price) OVER (PARTITION BY Name ORDER BY year ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS ema_selling_price
FROM car_info;
```

---

### 8️⃣ **Price Decrease from Previous Year**  
Find car models with a decrease in selling price compared to the previous year.  
```sql
SELECT Name, year, selling_price
FROM (
    SELECT Name, year, selling_price,
           LAG(selling_price) OVER (PARTITION BY Name ORDER BY year) AS previous_year_price
    FROM car_info
) AS price_changes
WHERE selling_price < previous_year_price;
```

---

### 9️⃣ **Highest Total Mileage by Transmission**  
Retrieve car models with the highest total mileage for each transmission type.  
```sql
WITH TotalMileage AS (
    SELECT Name, transmission, SUM(km_driven) AS total_mileage
    FROM car_info
    GROUP BY Name, transmission
)
SELECT Name, transmission, total_mileage
FROM TotalMileage
WHERE (transmission, total_mileage) IN (
    SELECT transmission, MAX(total_mileage)
    FROM TotalMileage
    GROUP BY transmission
);
```

---

### 🔟 **Average Selling Price for Top Models**  
Calculate the yearly average selling price for the top 3 models with the highest overall selling prices.  
```sql
WITH RankedSellingPrices AS (
    SELECT Name, selling_price,
           RANK() OVER (PARTITION BY Name ORDER BY selling_price DESC) AS price_rank
    FROM car_info
)
SELECT Name, year, AVG(selling_price) AS avg_selling_price_per_year
FROM car_info
WHERE Name IN (
    SELECT Name
    FROM RankedSellingPrices
    WHERE price_rank <= 3
)
GROUP BY Name, year;
```

---

## 📊 **Power BI Dashboard**  
A **Sales Dashboard** was created with the following tools:  
- **Power BI**: For interactive visualizations.  
- **SQL**: For querying and aggregating data.  
- **Microsoft Excel**: As the raw data source.  

### Dashboard Features:  
- Average Selling Price by Fuel Type.  
- Yearly Trends in Selling Prices.  
- Top 3 Car Models with Highest Mileage.  
- Transmission-Based Mileage Analysis.  

---

## ⚙️ How to Use  

1. Clone this repository:  
   ```bash
   git clone https://github.com/ayush7480/Exploring-Trends-Using-SQL.git
   ```  
2. Load the `car_info` dataset into your SQL environment.  
3. Run the provided SQL queries to analyze the data.  
4. Explore the Power BI Dashboard for detailed visualizations.  

---

## 🔑 Key Takeaways  
This project showcases the application of SQL in data analytics and demonstrates how meaningful insights can be derived from structured datasets. Additionally, it highlights the integration of SQL, Power BI, and Excel for end-to-end analytics.  

---

## 📜 License  
This project is licensed under the **MIT License**.  
```

This README.md file includes structured sections, emojis, and clear formatting to make it GitHub-friendly and visually appealing. Let me know if you'd like further adjustments!
