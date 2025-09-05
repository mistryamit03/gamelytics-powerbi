# 🧠 Measures (DAX)

Below are the DAX measures used in the Gamelytics Power BI dashboard.  
Formatting (currency/percent) is applied in the model.

## 📈 Engagement
**DAU (last day)**
```DAX
DAU (last day) = 
CALCULATE(
    DISTINCTCOUNT(Activity[uid]),
    LASTDATE('Date'[Date])
)

**MAU (30D rolling)**
```DAX
MAU (30D rolling) = 
CALCULATE (
    DISTINCTCOUNT ( Activity[uid] ),
    DATESINPERIOD ( 'Date'[Date], LASTDATE ( 'Date'[Date] ), -29, DAY )
)

**Stickiness**
```DAX
Stickiness = DIVIDE( [DAU (last day)], [MAU (30D rolling)] )

**Total Sessions**
```DAX
Total Sessions = SUM ( Activity[Sessions])

**Total Users**
```DAX
Total Users = DISTINCTCOUNT(Users[uid])


## 💰 Monetization


