Willkommen!
In diesem Repository finden Sie alles, was Sie zum einstündigen Webinar „Power BI Report in einer Stunde“ benötigen!
⚠️Sie benötigen Power BI Desktop, wenn Sie an der Veranstaltung teilnehmen möchten: https://www.microsoft.com/download/details.aspx?id=58494

1) Daten für den praktischen Teil (https://github.com/K-Borchert/webinar/blob/main/Haushaltsausgabenliste_Lebensmittel.xlsx)
2) Kennzahlen für die KPI-Berechnung (siehe unten 👇)
3) Hintergrund für den Bericht (https://github.com/K-Borchert/webinar/blob/main/BG%202.png)

Kennzahlen:
1) Gesamtausgaben = SUM(HouseholdSpending[Total])
2) Vormonat = CALCULATE([Gesamtausgaben],DATEADD(DateTable[Datum],1,MONTH))
3) % Wachstum gegenüber dem Vormonat = DIVIDE([Gesamtausgaben]-[Vormonat],[Vormonat])
4) Farbe gegenüber dem Vormonat = IF([% Wachstum gegenüber dem Vormonat]<0,„grün“,„rot“)
