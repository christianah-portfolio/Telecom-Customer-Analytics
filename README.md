# MTN Customer Overview Dashboard

**A Power BI dashboard that shows who the customers are, how much revenue they bring, how satisfied they are, and why some of them leave.**

![MTN Customer Analysis](https://github.com/christianah-portfolio/Telecom-Customer-Analytics/blob/main/01_customer_overview.png.png)

---

## Project Overview

**Brief Description**
A two-page Power BI dashboard analysing customer behaviour, churn, revenue, data usage, and satisfaction, built from a telecom dataset of 974 purchase records from 496 customers.

**Tools & Skills Used**
Power BI, Power Query, DAX, Data Cleaning, Dashboard Design, Data Storytelling.

**Project Goals**
To understand why customers leave, which plans earn the most, and how satisfied customers are, and to give recommendations that could reduce churn.

**Results**
146 of 496 customers (about 29%) had churned. The top reasons were better offers from competitors and high call tariffs. The 1.5TB Yearly Broadband Plan earned the most revenue (₦40.20M), and revenue followed the number of purchases each month.

---

## Business Problem

A telecom company loses money when customers leave, and it needs to know why. The data covers each customer's device, plan, age, location, data usage, rating, and purchases, plus the reason they left if they churned. I built a two-page dashboard to answer four questions:

1. How big is the customer base, and how much revenue does it bring?
2. How many customers have left, and why?
3. Which subscription plans earn the most, and how does revenue vary by month and state?
4. How satisfied are customers with each type of device?

---

## Key Findings

| Finding | Detail |
|---|---|
| About 29% of customers churned | **146 of 496** customers; 350 were still active |
| Competition and price drive most churn | Better offers from competitors (**29** customers), high call tariffs (**26**), poor network (**20**) and costly data plans (**20**). The other 51 left because of fast data consumption (18), poor customer service (18), or relocation (15) |
| One plan earns far more than the rest | The **1.5TB Yearly Broadband Plan** earned **₦40.20M**; the next four plans earned between ₦18.38M and ₦26.25M |
| A few plans bring in most of the revenue | The top five of 21 plans earn about **65%** of revenue, and the 1.5TB Yearly Broadband Plan alone earns about **20%** |
| Revenue followed the number of purchases | **₦63.37M** in January (271 purchase records), **₦87.17M** in February (450), and **₦48.81M** in March (253). February's peak came from more purchases, not bigger ones |
| Satisfaction is similar across devices | Average ratings ranged from **2.86** (Mobile SIM Card) to **3.02** (Broadband MiFi and 5G Broadband Router), out of 5 |
| The customer base is balanced by gender | **250** female (50.4%) and **246** male (49.6%) |

Total revenue was **₦199.35M**, and average data usage was **99.30 GB** per purchase record.

---

## Recommendations

1. **Respond to competitor offers and high call tariffs.** These two reasons alone account for 55 of the 146 churned customers. Competitive bundles, loyalty discounts, or price matching for customers at risk could help.
2. **Review the pricing and size of data plans.** Costly data plans (20) and fast data consumption (18) together suggest some customers need better-value or larger bundles.
3. **Find out what drove February's purchases.** Revenue rose and fell with the number of purchases, so understanding what happened in February (for example a promotion or season) could show how to repeat it.
4. **Promote long-term broadband plans.** The yearly plan earns the most, and customers on long plans are committed for longer. Check whether its high revenue comes from many subscribers or from a high price.
5. **Look at the Mobile SIM and 4G Router experience.** They had the lowest satisfaction ratings, and filtering the dashboard by device shows slightly higher churn for them than for the other two devices. The gaps are small, so treat this as a signal to watch.
6. **Improve network quality and customer service.** Poor network (20) and poor customer service (18) together explain 38 churned customers.

---

## Dashboard

The dashboard has two pages. Both share the same KPI cards (revenue, average data usage, total, active and churned customers) and slicers to filter by gender, MTN device, and customer review.

### Page 1: Customer Overview
*Where does the revenue come from?*

- Revenue by month, with a drill-down to revenue by state
- Revenue by subscription plan, for all 21 plans

![MTN Customer Overview](https://github.com/christianah-portfolio/Telecom-Customer-Analytics/blob/main/01_customer_overview.png.png)

### Page 2: Customer Analysis
*Who are the customers, how satisfied are they, and why do they leave?*

- Top 5 subscription plans by revenue
- Satisfaction by device (Broadband MiFi, 5G Broadband Router, 4G Router, Mobile SIM Card)
- Revenue trend from January to March
- Customers by gender
- Top churn reasons

![MTN Customer Analysis](dashboard-pages/02_customer_analysis.png)

---

## Dataset

A telecom customer practice dataset with **974 purchase records from 496 customers**, covering January to March, across 35 Nigerian states and territories. Each customer appears one to three times, so customer counts use distinct customer IDs, while revenue and data usage use every purchase record.

Fields include: customer ID, name, date of purchase, age, state, MTN device, gender, satisfaction rate (1 to 5), customer review, tenure in months, subscription plan, unit price, number of times purchased, total revenue, data usage, customer response, customer status (active or churn), and reason for churn.

The dataset is not included in this repository because it contains customer names.

---

## Approach

1. **Explored** the dataset to understand each column and what it measures.
2. **Cleaned and prepared** the data in Power Query:
   - Changed data types, for example setting the purchase date as a date so revenue can be grouped by month
   - Renamed columns, for example the customer status column, so names are clean and consistent
   - Corrected a misspelt churn reason ("Tarriffs" to "Tariffs") so it reads correctly on the dashboard
3. **Wrote DAX measures** for the KPI cards:

```DAX
Total Customer = DISTINCTCOUNT('MTN Dataset'[Customer ID])

TotalRevenue = SUM('MTN Dataset'[Total Revenue])

Active Customers =
CALCULATE(DISTINCTCOUNT('MTN Dataset'[Customer ID]),
    'MTN Dataset'[Customer Status] = "Active")

Churned Customers =
CALCULATE(DISTINCTCOUNT('MTN Dataset'[Customer ID]),
    'MTN Dataset'[Customer Status] = "Churn")

Average Data Usage = FORMAT(AVERAGE('MTN Dataset'[Data Usage]), "0.00") & " GB"
```

4. **Designed the two-page dashboard** with slicers so users can filter by gender, device, and customer review.
5. **Wrote the findings and recommendations** from what the charts show.

---

## Limitations

- This is a practice dataset, so the findings should not be treated as conclusions about a real company.
- The data covers only three months, so the revenue trend cannot show a long-term pattern.
- Many customers used more than one device across their purchases, so device comparisons overlap.
- Satisfaction ratings are close to each other across devices, so the differences are small.
- Reasons for churn are only recorded for customers who churned.

---

## Project Files

```
telecom-customer-analytics/
├── README.md
├── dashboard/
│   └── MTN_Customer_Overview_Dashboard.pbix
└── dashboard-pages/
    ├── 01_customer_overview.png
    └── 02_customer_analysis.png
```
