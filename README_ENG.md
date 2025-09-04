Welcome!
In this repository you will find all you need regarding the Power BI in one hour webinar!
⚠️You need a Power BI Desktop if you want to join the show: https://www.microsoft.com/download/details.aspx?id=58494

1) Data for the Hands on part (https://github.com/K-Borchert/webinar/blob/main/Household_Grocery_Spendings.xlsx)
2) Measures for KPI calculation (see below 👇)
3) Background for the Report (https://github.com/K-Borchert/webinar/blob/main/BG%202.png)

Measures:
1) Total spenndings = SUM(HouseholdSpending[Total])
2) Previous Month = CALCULATE([Total spenndings],DATEADD(DateTable[Date],1,MONTH))
3) % MoM growth = DIVIDE([Total spenndings]-[Previous Month],[Previous Month])
4) Color MoM = IF([% MoM growth]<0,"green","red")

   


DateTable =
ADDCOLUMNS (
    CALENDARAUTO(),
    "Year", YEAR ( [Date] ),
    "MonthNumber", MONTH ( [Date] ),
    "MonthName", FORMAT ( [Date], "MMMM" ),
    "MonthShort", FORMAT ( [Date], "MMM" ),
    "Quarter", "Q" & FORMAT ( [Date], "Q" ),
    "YearMonth", FORMAT ( [Date], "YYYY-MM" ),
    "Weekday", WEEKDAY ( [Date], 2 ),         -- 1 = Sunday, 2 = Monday
    "WeekdayName", FORMAT ( [Date], "dddd" ),
    "IsWeekend", IF ( WEEKDAY ( [Date], 2 ) > 5, TRUE(), FALSE() )
)
