Willkommen!
```
In diesem Repository finden Sie alles, was Sie zum einstündigen Webinar „Power BI Report in einer Stunde“ benötigen!
🔗Webinar Teil 1: https://www.youtube.com/live/MeykuS1vUG8?si=LLXK-Lt2TK94241b
🔗Webinar Teil 2: https://youtube.com/live/cDQLhQRRt6U
⚠️Sie benötigen Power BI Desktop, wenn Sie an der Veranstaltung teilnehmen möchten:
https://www.microsoft.com/download/details.aspx?id=58494

1) Daten für den praktischen Teil (https://github.com/K-Borchert/webinar/blob/main/Haushaltsausgabenliste_Lebensmittel.xlsx)
2) Kennzahlen für die KPI-Berechnung (siehe unten 👇)
3) Hintergrund für den Bericht (https://github.com/K-Borchert/Webinar_1_hour_Report_Power_BI/blob/main/Background_Report.png)
```

Kennzahlen:
```
1) Totale Ausgaben = SUM(HouseholdSpending[Total])
2) Vormonat = CALCULATE([Total spenndings],DATEADD(DateTable[Date],-1,MONTH))
3) % Wachstumsrate gegenüber dem Vormonat = DIVIDE([Total spenndings]-[MoM],[MoM])
4) Farbe = IF([% MoM growth]<0,"green","red")


(Für Teil 2 - https://youtube.com/live/cDQLhQRRt6U)
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
Datumstabelle =
VAR _Kalender = CALENDARAUTO()
RETURN
ADDCOLUMNS(
    _Kalender,
    "Jahr", YEAR([Date]),
    "Monat", MONTH([Date]),
    "Monatsname", FORMAT([Date], "MMMM"),
    "Jahr-Monat", FORMAT([Date], "YYYY-MM"),
    "Quartal", "Q" & FORMAT([Date], "Q"),
    "Wochentag", WEEKDAY([Date], 2),
    "Wochentagname", FORMAT([Date], "dddd"),
    "Kalenderwoche", WEEKNUM([Date], 2),
    "Ist Wochenende", IF(WEEKDAY([Date],2)>5, TRUE(), FALSE())
)

```
