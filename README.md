## CRM Dashboard Performance Analysis: 2024 Sales Cycle Review

# Problem Statement

Lavender group of companies specializes in different product and offering services to various organizations. In 2024, the CRM department experienced variability in its lead conversion rate and significant fluctuations in the Total Deal Value and Closed Leads Value in 2024.Sales performance appears to be heavily reliant on a few top sales agents and certain countries, indicating potential inefficiencies or untapped opportunities in other areas. This analysis is needed to identify the root causes of the sales performance dips and to strategically allocate resources to maximize revenue growth and improve lead quality.

The project has important key metrics like Lead acquisition, sales agent, product, geographic region, industry.

This project was carried out to understand how the CRM department handled leads and their conversion rates across geographic regions in 2024.

# Project Question

	What is the cause of sales performance fluctuations?

	How can we reduce the Lost Lead Value and ensure a high-value closed deal pipeline throughout the year.


# Data Structure 

This Dataset contains important metrics such as Lead acquisition, sales agent, product, geographic region, industry, lead value, lead conversion rate, closed lead value, lost lead value and won leads in 2024.

	FactCRM: This dataset contains key metrics such as Lead acquisition, sales agent, product and geographic region, industry.

Metrics calculated for this table are: Lead lost (Calculate [No. of leads], ‘FACT_CRM’ [All Stage] = ‘lost’, Lead Closed (Calculate [No. of leads], ‘FACT_CRM’ [All Stage] = ‘Closed’, Lead won (Calculate [No. of leads], ‘FACT_CRM’ [All Stage] = ‘won’, : Lead lost (Calculate [No. of leads], ‘FACT_CRM’ [All Stage] = ‘lost’, Conversion Rate=Divide ([leads closed], [No. of leads] .
 
	DimDate: The table contains column with day, weeks, months, month year and year.

https://github.com/laur196/CRM-Dashboard-Performance-Analysis-2024-Sales-Cycle-Review/blob/main/Untitled.png
