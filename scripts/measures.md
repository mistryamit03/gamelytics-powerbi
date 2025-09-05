## 📈 Engagement

### DAU (last day)
```DAX
DAU (last day) =
CALCULATE(
    DISTINCTCOUNT(Activity[uid]),
    LASTDATE('Date'[Date])
)

MAU (30D rolling) =
CALCULATE(
    DISTINCTCOUNT(Activity[uid]),
    DATESINPERIOD('Date'[Date], LASTDATE('Date'[Date]), -29, DAY)
)
