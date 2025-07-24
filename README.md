# Hotel-Data-Analysis
Build a visual data story using sql and Power BI to present to your stakeholders
# 🏨 Hotel Revenue Analysis Dashboard

This project explores hotel booking data to analyze revenue trends, customer behavior, and overall business performance using **SQL** and **Power BI**.
---

## 📌 Objective

To build a data pipeline using SQL and Power BI that delivers clear insights into:
- Revenue trends over time
- Average Daily Rate (ADR)
- Occupancy (Total nights stayed)
- Discounts and promotional patterns
- City vs. Resort hotel performance

---

## 🧰 Tools Used

- **SQL Server**: Data cleaning, transformation, and revenue calculation
- **Power BI**: Data visualization and dashboard creation
- **Excel**: Source data input (assumed from `.xlsx` sheet names in queries)

---

## 🗂️ Project Structure

| File | Description |
|------|-------------|
| `SQL_queries_hotel_revenue.txt` | SQL scripts for data union, joins, and revenue calculations |
| `hotel_revenue.pbix` | Power BI dashboard showing revenue KPIs, trends, and segmentation |
| `dashboard_screenshot.png` | Preview of the final dashboard |

---

## 🧮 Key Metrics Displayed

- **Revenue**: $10.23M
- **ADR (Average Daily Rate)**: $10.52M
- **Total Nights Stayed**: 367.94K
- **Discount Rate**: 25.80%
- **Year-over-Year Revenue Trend**
- **City vs. Resort Hotel Performance (Pie Chart)**

---

## 💡 Insights Derived

- **City Hotels** account for ~54% of total revenue
- Revenue has shown consistent **year-over-year growth**
- Significant discounts (~25%) may be impacting ADR
- Strong occupancy with nearly **368K nights stayed**

---

## 🧾 SQL Highlights

```sql
-- Revenue Calculation
select arrival_date_year, hotel,
round(sum((stays_in_weekend_nights + stays_in_week_nights) * adr), 2) as revenue
from hotels
group by arrival_date_year, hotel
sql
Copy
Edit
-- Data Union and Joins
with hotels as (
  select * from dbo.['2018$']
  union
  select * from dbo.['2019$']
  union
  select * from dbo.['2020$']
)

select * from hotels 
left join dbo.market_segment$ on hotels.market_segment = dbo.market_segment$.market_segment
left join dbo.meal_cost$ on dbo.meal_cost$.meal = hotels.meal
