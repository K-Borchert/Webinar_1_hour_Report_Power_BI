Welcome!
```
In this repository you will find all you need regarding the Power BI in one hour webinar!
🔗Webinar - Part I: https://www.youtube.com/live/WrxXxBph62g?si=53rRyeb2SbCH1GQW
🔗Webinar - Part II: https://youtube.com/live/r43Dr2CcZ3M?feature=share
⚠️You need a Power BI Desktop if you want to join the show: https://www.microsoft.com/download/details.aspx?id=58494

1) Data for the Hands on part (https://github.com/K-Borchert/webinar/blob/main/Household_Grocery_Spendings.xlsx)
2) Measures for KPI calculation (see below 👇)
3) Background for the Report (https://github.com/K-Borchert/Webinar_1_hour_Report_Power_BI/blob/main/Background_Report.png)
```

Measures:
```
1) Total spendings = SUM(HouseholdSpending[Total])
2) MoM = CALCULATE([Total spenndings],DATEADD(DateTable[Date],-1,MONTH))
3) % MoM growth = DIVIDE([Total spenndings]-[MoM],[MoM])
4) Color MoM = IF([% MoM growth]<0,"green","red")

(For Part 2)
5) Header Card Visual = SELECTEDVALUE(Spendings[Category],"Total spendings")
6) Header Column Visual = "Monthly comparison for " & SELECTEDVALUE(Spendings[Category],"Total spendings")
7) Color dark= 
Var _MoM = [% MoM]
Var _Color =
SWITCH(
    TRUE(),
    _MoM=0, "grey",
    _MoM<0, "green",
    _MoM>0, "red")

Return
_Color

8) Color light = 
Var _MoM = [%MoM]
Var Color =
SWITCH(
    TRUE(),
    _MoM = 0, "grey",
    _MoM > 0, "#ea899a",
    _MoM < 0, "#b2d4b2"
)
RETURN
Color
```
   


```

DateTable = 
ADDCOLUMNS (
    CALENDARAUTO(),
    "Year", YEAR ( [Date] ),
    "MonthNumber", MONTH ( [Date] ),
    "MonthName", FORMAT ( [Date], "MMMM" ),
    "MonthShort", FORMAT ( [Date], "MMM" ),
    "Month-Year", FORMAT ( [Date], "MMM YYYY" ),       -- e.g. Jan 2024
    "YearMonth", FORMAT ( [Date], "YYYYMM" ),          -- good for sorting
    "Quarter", "Q" & FORMAT ( [Date], "Q" ),
    "Weekday", WEEKDAY ( [Date], 2 ),                  -- 1 = Sunday, 2 = Monday
    "WeekdayName", FORMAT ( [Date], "dddd" ),
    "IsWeekend", IF ( WEEKDAY ( [Date], 2 ) > 5, TRUE(), FALSE() ),
    "CalendarWeek", WEEKNUM ( [Date], 2 )              -- 2 = week starts Monday
)
```

