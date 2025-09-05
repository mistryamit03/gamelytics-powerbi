# 🧠 Measures (DAX)

```DAX
-- example
DAU (last day) =
CALCULATE( DISTINCTCOUNT(Activity[uid]), LASTDATE('Date'[Date]) )
