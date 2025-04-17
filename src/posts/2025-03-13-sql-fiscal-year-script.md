---
title: SQL Fiscal Year Script
description: A straightforward script to generate fiscal year data.
date: '2025-03-14'
categories:
  - sql
published: true
---

### 📅

During previous projects involving SQL data analysis, I've encountered situations where filtering data by fiscal year was necessary.
<br>
I sought to develop a self-maintaining table that would automatically manage dates and columns, with the ability to update itself annually without too much manual intervention.
<br><br>
To address this need, I created a script that successfully met these requirements.
<br><br>

```sql
-- Set to the start of your fiscal year
DECLARE @d DATE = CONCAT(YEAR(GETDATE()),'-04-01');

WITH [x]
AS (
    -- Adjust this if there are more than 52 weeks in a year
    SELECT TOP (52) ROW_NUMBER() OVER (ORDER BY [object_id]) - 1 AS [n]
    FROM [sys].[all_objects]
    ORDER BY [object_id]
)
-- Remove commented lines when ready to insert the data into the desired table.
--INSERT INTO [dbo].[FiscalYear] (
--    [Week]
--   ,[Month]
--   ,[Year]
--   ,[FiscalYear]
--   ,[StartDate]
--   ,[EndDate]
--)
SELECT DATEADD(WEEK, [n], @d) AS [WeekStartDate]
      ,DATEADD(DAY, [n] * 7 + 6, @d) AS [WeekEndDate]
	    ,[n] + 1 AS [Week]
      ,MONTH(DATEADD(WEEK, [n], @d)) AS [Month]
	    ,YEAR(DATEADD(WEEK, [n], @d)) AS [Year]
			,CASE WHEN MONTH(DATEADD(WEEK, [n], @d)) BETWEEN 4 AND 6 THEN 'Q1'
			      WHEN MONTH(DATEADD(WEEK, [n], @d)) BETWEEN 7 AND 9 THEN 'Q2'
						WHEN MONTH(DATEADD(WEEK, [n], @d)) BETWEEN 10 AND 12 THEN 'Q3'
						WHEN MONTH(DATEADD(WEEK, [n], @d)) BETWEEN 1 AND 3 THEN 'Q4'
						ELSE 'Error'
	     END AS [FiscalQuarters]
      ,CONCAT(YEAR(GETDATE()), YEAR(GETDATE()) + 1) AS [FiscalYear]
FROM [x]
ORDER BY [n];
```

<br>

> I need to fix the code block 🤦🏻‍♂️

<br>
I acknowledge this script has limitations. It assumes 1st April, as the fiscal year start date, so modifications would be necessary for organizations with different fiscal calendars. Furthermore, the current implementation accommodates a standard 52-week year, not accounting for years that occasionally contain 53 weeks.
<br><br>
Ideally, I'd prefer developing a more robust solution that eliminates the need to manually adjust for fiscal year start dates or varying week counts, allowing for complete automation. Addressing the 52/53 week variation seems particularly achievable.
<br><br>
When time permits, I plan to revisit and enhance this script, with a priority on resolving at least the week count variability issue.
