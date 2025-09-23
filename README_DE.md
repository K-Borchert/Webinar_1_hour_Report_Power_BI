Willkommen!
```
In diesem Repository finden Sie alles, was Sie zum einstündigen Webinar „Power BI Report in einer Stunde“ benötigen!
🔗Webinar Teil 1: https://www.youtube.com/live/MeykuS1vUG8?si=LLXK-Lt2TK94241b
🔗Webinar Teil 2: https://youtube.com/live/cDQLhQRRt6U
⚠️Sie benötigen Power BI Desktop, wenn Sie an der Veranstaltung teilnehmen möchten: https://www.microsoft.com/download/details.aspx?id=58494

1) Daten für den praktischen Teil (https://github.com/K-Borchert/webinar/blob/main/Haushaltsausgabenliste_Lebensmittel.xlsx)
2) Kennzahlen für die KPI-Berechnung (siehe unten 👇)
3) Hintergrund für den Bericht (https://github.com/K-Borchert/Webinar_1_hour_Report_Power_BI/blob/main/Background_Report.png)
```

Kennzahlen:
```
1) Total spendings = SUM(HouseholdSpending[Total])
2) MoM = CALCULATE([Total spenndings],DATEADD(DateTable[Date],1,MONTH))
3) % MoM growth = DIVIDE([Total spenndings]-[MoM],[MoM])
4) Color MoM = IF([% MoM growth]<0,"green","red")

(Für Teil 2)
5) Überschrift Karte= SELECTEDVALUE(Ausgaben[Kategorie],"Gesamtausgaben")
6) Überschrift Säulendiagramm = "Monatsvergleich für " & SELECTEDVALUE(Ausgaben[Kategorie],"Gesamtausgaben")
7) Farbe = 
Var _MoM = [% MoM]
Var _Color =
SWITCH(
    TRUE(),
    _MoM=0, "grey",
    _MoM<0, "green",
    _MoM>0, "red")

Return
_Color
```
   


```
Datumstabelle= 
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
