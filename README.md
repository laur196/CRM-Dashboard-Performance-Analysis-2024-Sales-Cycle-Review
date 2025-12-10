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

![CRM Data struture](https://github.com/laur196/CRM-Dashboard-Performance-Analysis-2024-Sales-Cycle-Review/blob/main/Untitled.png)

# Technical Details 
This project used Power BI for all stages of data cleaning and analysis, with a focus on CRM lead value in 2024.

## Skill Details
Skills: Format, Calculate, Aggregate Function (Sum, Divide, AVERAGEX)

Steps Details
Initial Inspection: Checked all source tables (DimDate, FactCRM) for missing values, duplicate entries and inconsistent data types.
Cleaning & Standardization: Converted Types and Renamed Columns.
Calculated Metrics: Leads lost, Leads won, Leads closed, Conversion Rate, No. of Leads.

## Data Cleaning Action
Here are the key cleaning operation
	Renamed Column
Purpose: To understand my table better, I had to rename the row ‘Owner’ to ‘Sales Agent’.

	Converted Types
Purpose: Organization and country columns were converted from number to text in other to make calculation possible for accurate analysis. 

## Date Table Details
The date was inserted into the StartDate and the last day was inserted as the EndDate and this helped to create a date table which contains day, week, month, month year, Quarter year, year.

## Steps Details

The date table was created through this method;

let 
// Create parameter 
    StartDate = #date(2023,1,1),
    EndDate = #date(2025,5,31),
    Step = Duration.Days(EndDate - StartDate)+1, 
// Create the List of date
    Source = List.Dates(StartDate,Step, #duration(1,0,0,0)), 
    #"Converted to Table" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
    #"Changed Type" = Table.TransformColumnTypes(#"Converted to Table",{{"Column1", type date}}),
    #"Renamed Columns" = Table.RenameColumns(#"Changed Type",{{"Column1", "Date"}}),
// Create additional columns 
    #"Inserted Year" = Table.AddColumn(#"Renamed Columns", "Year", each Date.Year([Date]), Int64.Type),
    #"Inserted Quarter" = Table.AddColumn(#"Inserted Year", "Quarter", each Date.QuarterOfYear([Date]), Int64.Type),
    #"Inserted Quarter Year" = Table.AddColumn(#"Inserted Quarter", "Quarter Year", each Text.Combine({"Q", Text.From([Quarter], "en-US"), " ", Text.From([Year], "en-US")}), type text), 
    #"Inserted Month" = Table.AddColumn(#"Inserted Quarter Year", "Month", each Date.Month([Date]), Int64.Type),
    #"Inserted Month Name" = Table.AddColumn(#"Inserted Month", "Month Name", each Text.Start(Date.MonthName([Date]),3), type text),
    #"Inserted Month Year" = Table.AddColumn(#"Inserted Month Name", "Month Year", each Text.Combine({[Month Name], " ", Text.From([Year], "en-US")}), type text),
    #"Inserted Month Year S" = Table.AddColumn(#"Inserted Month Year", "Month Year S", each Text.Combine({Text.From([Year], "en-US"), Text.PadStart(Text.From([Month], "en-US"), 2, "0")}), type text),
    #"Inserted End of Month" = Table.AddColumn(#"Inserted Month Year S", "End of Month", each Date.EndOfMonth([Date])),
    #"Inserted Week Day Name" = Table.AddColumn(#"Inserted End of Month", "Week Day", each Text.Start(Date.DayOfWeekName([Date]),3), type text),
    #"Inserted Day of Week" = Table.AddColumn(#"Inserted Week Day Name", "Day of Week", each Date.DayOfWeek([Date]), Int64.Type),
    #"Inserted Day" = Table.AddColumn(#"Inserted Day of Week", "Day", each Date.Day([Date]), Int64.Type),
    #"Inserted Week of Month" = Table.AddColumn(#"Inserted Day", "Week of Month", each Date.WeekOfMonth([Date]), Int64.Type),
    #"Inserted Week of Month W" = Table.AddColumn(#"Inserted Week of Month", "Week", each Text.Combine({"W", Text.From([Week of Month], "en-US")}), type text),
    #"Inserted Week of Year" = Table.AddColumn(#"Inserted Week of Month W", "Week of Year", each Date.WeekOfYear([Date]), Int64.Type),
    #"Inserted Week of Year W" = Table.AddColumn(#"Inserted Week of Year", "Week of Year W", each Text.Combine({"W", Text.From([Week of Year], "en-US")}), type text),
    #"Added Fiscal Month" = Table.AddColumn(#"Inserted Week of Year W", "Fiscal Month", each if Date.Month([Date]) <= 3 then Date.Month([Date]) + 9 else Date.Month([Date]) - 3),
    #"Added Fiscal Year" = Table.AddColumn(#"Added Fiscal Month", "Fiscal Year", each if Date.Month([Date]) <= 3 then Date.Year([Date]) else Date.Year([Date]) + 1),
    #"Added Fiscal Quarter" = Table.AddColumn(#"Added Fiscal Year", "Fiscal Quarter", each Number.RoundUp([Fiscal Month]/3))
in
    #"Added Fiscal Quarter"

   # Executive Summary
    
This dashboard reveals a strong but highly seasonal sales cycle. The cause of sales fluctuation was a case of High-Value Seasonal Volatility and this seasonality represents a major risk to consistent annual revenue. Also, there is an overall conversion rate of $11.60, total closed value of $931.3K yet there's a substantial Lost Lead Value of $200.12K indicating poor initial lead qualification in later-stage pipeline management.
Though, the sales pipeline peaks in June/July but suffers a sharp decline through the rest of the year, particularly after August. 
The 'SAAS' product is the primary value driver, contributing $44.83 of closed leads by count and $38.36 by value. Country performance is led by the Netherlands $15.00 and Portugal $13.75 in conversion rate, sales agents like Laura Thompson drive the highest closed deal value. 

# Key Insights

	High-Value Seasonal Volatility: Values contributed by both total deals and closed deals peaks sharply in June/July before dropping to its lowest point from September onwards. This seasonality represents a major risk to consistent annual revenue. The contribution from churned customers follows a similar seasonal curve.
 
	Product and Lead Value Concentration: The SAAS product is the largest driver of closed leads by volume with $44.83 and value with $38.36. Custom Solutions is the second largest driver by volume with $23.48 but the lowest by value with $23.48, suggesting that while they close, they might be lower-value or higher-effort deals compared to SAAS.

	Conversion Rate Leaders: The overall conversion rate is $11.60.The Netherlands with $15.00 and Portugal with $13.75 significantly outperform the average, pointing to potential best practices in these regions that could be repeated globally. Germany has the lowest conversion rate at $9.32.

	Sales Agent Impact: The top three agents Laura Thompson, Michael Brown, and Jessica Martinez contributed over $60 of the total closed value, highlighting a concentration of high-value deal closers. However, agents with fewer closed leads like David Wilson have lower conversion rates $7.69 rate, suggesting a need for targeted coaching.

# Recommendations

	Seasonal Demand: Implement a proactive campaign strategy. Specifically, introduce incentives, product bundles, or targeted marketing efforts to stabilize the pipeline during the slower months. To mitigate the steep decline in deal value and leads closed during the post-summer months and ensure a smoother revenue stream.

	Process Improvement: Conduct a 'Lost Lead' Root Cause Analysis. Focus on the $61 lost leads and $200.12K lost value by analyzing the specific 'Stages' they dropped out from. 

	Conversion Rate (CRO): Globalize Best Practices from the Netherlands and Portugal. Analyze the sales script, lead sourcing, and objection handling techniques used in these top-performing countries and mandate their implementation in lower-performing regions like Germany. To boost the global average conversion rate above the $12 project goal by replicating proven success. To boost the global average conversion rate above the $12 project goal by replicating proven success.


	Product Strategy: Prioritize SAAS Lead Qualification. Given SAAS drives the most volume and value, implement a stricter qualification (e.g., using BANT or MEDDIC) for SAAS leads to ensure sales agent focus is on the most promising opportunities. To maximize ROI on sales effort by concentrating resources on the highest-value product line.

![CRM Data struture](https://github.com/laur196/CRM-Dashboard-Performance-Analysis-2024-Sales-Cycle-Review/blob/main/CRM%201.JPG)

![CRM Data struture](https://github.com/laur196/CRM-Dashboard-Performance-Analysis-2024-Sales-Cycle-Review/blob/main/CRM%202.JPG)
