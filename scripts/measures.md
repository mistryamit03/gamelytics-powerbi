# 🧠 Measures (DAX)

Below are the DAX measures used in the Gamelytics Power BI dashboard.  
Formatting (currency/percent) is applied in the model.

## 📈 Engagement
**DAU (last day)**
```DAX
--DAU (last day) = 
CALCULATE(
    DISTINCTCOUNT(Activity[uid]),
    LASTDATE('Date'[Date])
)
