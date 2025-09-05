# 🧠 Measures (DAX)

Below are the DAX measures used in the Gamelytics Power BI dashboard.
Formatting (currency/percent) is applied in the model.

---

## 📈 Engagement

**DAU (last day)**
```DAX
DAU (last day) =
CALCULATE (
    DISTINCTCOUNT ( Activity[uid] ),
    LASTDATE ( 'Date'[Date] )
)

MAU (30D rolling) =
CALCULATE (
    DISTINCTCOUNT ( Activity[uid] ),
    DATESINPERIOD ( 'Date'[Date], LASTDATE ( 'Date'[Date] ), -29, DAY )
)

Stickiness =
DIVIDE ( [DAU (last day)], [MAU (30D rolling)] )

Total Sessions =
SUM ( Activity[Sessions] )

Total Users =
DISTINCTCOUNT ( Users[uid] )

Registrations =
CALCULATE (
    DISTINCTCOUNT ( Users[uid] ),
    USERELATIONSHIP ( 'Date'[Date], Users[RegDate] )
)
