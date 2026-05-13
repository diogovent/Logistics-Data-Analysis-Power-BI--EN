# 🚚 Logistics-Data-Analysis-Power-BI--EN

> Analysis of logistics data focusing on delivery performance, punctuality, delivery channels and salesperson performance, covering the years 2019 and 2020.

---

## 📌 Index

- About the Project
- Objectives of the Analysis
- Tools Used
- Dataset Structure
- Dashboard
- DAX Measures
- Key Findings
- How to View

---

## 📁 About the Project

This project was developed using a logistics dataset containing records of orders, deliveries and seller reviews for the years **2019 and 2020**.

The main objective is to understand the operational performance of deliveries — identifying delays, the most efficient channels and the best-performing teams.

---

## 🎯 Analysis Objectives

- Monitor the total number of deliveries and the on-time delivery rate
- Identify the delivery channels with the highest volume and efficiency
- Analyse performance by delivery team
- Identify the cities with the most delayed deliveries
- Evaluate seller performance by rating

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| **Power BI Desktop** | Building the dashboard and visualisations |
| **DAX** | Creating calculated measures |
| **Excel (.xlsx)** | Source of logistics data |

---

## 📂 Dataset Structure

The `dataset.xlsx` file contains a table called **Logistics** with the following columns:

| Variable | Type | Description |
|---|---|---|
| `ID_Pedido` | Numeric | Unique order identifier |
| `ID_Vendedor` | Numeric | Seller identifier |
| `ID_Cliente` | Numeric | Customer identifier |
| `Equipe_Entrega` | Categorical | Team responsible for delivery (North, South, etc.) |
| `Cliente` | Categorical | Customer name |
| `Canal_Entrega` | Categorical | Channel used for delivery |
| `ID_Cidade` | Numeric | Delivery city identifier |
| `Data_Pedido` | Date | Date on which the order was placed |
| `Data_Entrega_Prevista` | Date | Expected delivery date |
| `Data_Entrega_Realizada` | Date | Date on which the delivery was actually made |
| `Status_Entrega` | Categorical | Delivery status — Early, On Time or Late |

---

## 📊 Dashboard

![Dashboard Preview](https://github.com/diogovent/Logistics-Data-Analysis-Power-BI--PT/blob/main/Dashboard.png)

**Top KPIs:**
- **Total Deliveries:** 54K
- **Total On-Time Deliveries:** 47K

**Visuals included:**
- **Total On-Time Deliveries by Delivery Channel** — Area chart showing trends by channel
- **Percentage of Deliveries by Team** — Horizontal bar chart; the North team leads with 27.44%
- **Total Deliveries per Month** — Line chart showing monthly trends throughout the year
- **Percentage of Deliveries by Status** — Bar chart showing Early (70.71%), On Time (16.31%) and Late (12.98%)
- **Table: Top Sellers** — Ranking by seller ID with total deliveries and star rating
- **Table: Late Deliveries by City** — Cities with the highest number of late deliveries

**Filter available:**
- Selection by year (2019 / 2020)

---


## 🧮 DAX Metrics

Total Deliveries:
```dax
Total de Entregas = COUNTROWS(Logistica)
```

Total On-Time Deliveries:
```dax
Total de Entregas no Prazo = CALCULATE([Total de Entregas], FILTER(Logistica, Logistica[Status_Entrega] = "Antecipado" || Logistica[Status_Entrega]= "No Prazo"))
```

Rating:
```dax
Rating = 
VAR __MAX_NUMBER_OF_STARS = 5
VAR __MIN_RATED_VALUE = 1500
VAR __MAX_RATED_VALUE = 2500
VAR __BASE_VALUE = [Total de Entregas]
VAR __NORMALIZED_BASE_VALUE =
	MIN(
		MAX(
			DIVIDE(
				__BASE_VALUE - __MIN_RATED_VALUE,
				__MAX_RATED_VALUE - __MIN_RATED_VALUE
			),
			0
		),
		1
	)
VAR __STAR_RATING = ROUND(__NORMALIZED_BASE_VALUE * __MAX_NUMBER_OF_STARS, 0)
RETURN
	IF(
		NOT ISBLANK(__BASE_VALUE),
		REPT(UNICHAR(9733), __STAR_RATING)
			& REPT(UNICHAR(9734), __MAX_NUMBER_OF_STARS - __STAR_RATING)
	)
```

---

## 🔍 Key Findings

1. **Most Deliveries Are Early:**  70.71% of deliveries were made before the scheduled date, which is an excellent performance indicator

2. **The Late Delivery Rate is 12.98%:**  Around 1 in 8 deliveries arrives late, a figure to monitor

3. **The North Team Dominates in Terms of Volume:**  Accounting for 27.44% of all deliveries, followed by the South-East with 24.87%

4. **City 79 Has the Highest Number of Delays:**  With 589 late deliveries, it clearly stands out from the rest

5. **Salesperson 3894 Is the Most Productive:**  With 2,208 deliveries and a 4-star rating

6. **The Distribution, Direct Sales and Central-West Channels Have Very Low Performance:**  With percentages close to 0%, this may indicate operational problems in these channels

---

## 💡 Recommendations

1. **Investigate Delays in City 79:** It accounts for almost twice as many delays as the second most problematic city

2. **Analyse Underperforming Channels:** Distributors (0.33%), Direct Sales (0.16%) and the Midwest (0.00%) require attention

3. **Replicate the Northern Team’s Practices:** As the team with the highest volume, understand what they do well and apply it to the other teams

4. **Monitor the Drop in Deliveries from September Onwards:** The monthly chart shows a sharp decline in the second half of the year

---

## 📌 How to view

1. Download the `.pbix` file available in this repository
2. Open it in **Power BI Desktop** (free)
3. The `dataset.xlsx` data file is included in the repository
4. Use the **2019 / 2020** buttons to filter by year
5. Alternatively, if you prefer, you can access it via this link: https://app.powerbi.com/groups/me/reports/dd0c01aa-ab22-4d45-885e-546b96c2c640?pbi_source=desktop
---

## 👤 Author

Developed as a data analysis project for a personal portfolio.
