# 🧠 Measures (DAX)

Below are the DAX measures used in the Gamelytics Power BI dashboard.
(Formatting for currency/percent is set in the model.)

------------------------------------------------------------
## 📈 Engagement (all engagement metrics)
------------------------------------------------------------

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

------------------------------------------------------------
## 💰 Monetization
------------------------------------------------------------

Total Revenue =
SUM ( ABTest[revenue] )

Paying Users =
CALCULATE ( DISTINCTCOUNT ( ABTest[user_id] ), ABTest[revenue] > 0 )

ARPU =
DIVIDE ( [Total Revenue], [Total Users] )

ARPPU =
DIVIDE ( [Total Revenue], [Paying Users] )

Conversion Rate =
DIVIDE ( [Paying Users], [Total Users] )

------------------------------------------------------------
## 🧪 A/B Summary (Control vs Test)
-- Use with ABTest[testgroup_label] on the visual axis/columns.
------------------------------------------------------------

Users (by group) =
DISTINCTCOUNT ( ABTest[user_id] )

Paying Users (by group) =
CALCULATE ( DISTINCTCOUNT ( ABTest[user_id] ), ABTest[revenue] > 0 )

Revenue (by group) =
SUM ( ABTest[revenue] )

ARPU (by group) =
DIVIDE ( [Revenue (by group)], [Users (by group)] )

Conversion (by group) =
DIVIDE ( [Paying Users (by group)], [Users (by group)] )

------------------------------------------------------------
## 🔁 Cohorts & Retention
------------------------------------------------------------

Cohort Size =
CALCULATE (
    DISTINCTCOUNT ( Users[uid] ),
    TREATAS ( VALUES ( Activity[CohortMonth] ), Users[CohortMonth] )
)

Retained Users =
DISTINCTCOUNT ( Activity[uid] )

Retention Rate =
DIVIDE ( [Retained Users], [Cohort Size] )

Retained Users D1 =
CALCULATE ( [Retained Users], Activity[DaysSinceSignup] = 1 )

Retention D1 % =
DIVIDE ( [Retained Users D1], [Cohort Size] )

Retained Users D7 =
CALCULATE ( [Retained Users], Activity[DaysSinceSignup] = 7 )

Retention D7 % =
DIVIDE ( [Retained Users D7], [Cohort Size] )

Retained Users D30 =
CALCULATE ( [Retained Users], Activity[DaysSinceSignup] = 30 )

Retention D30 % =
DIVIDE ( [Retained Users D30], [Cohort Size] )

------------------------------------------------------------
## 🎨 Utility (for bar colors)
-- Apply as Format by → Field value on ARPU-by-group chart.
------------------------------------------------------------

Color by Testgroup =
SWITCH (
    SELECTEDVALUE ( ABTest[testgroup_label] ),
    "Control", "#64748B",
    "Test",    "#10B981",
    "#2563EB"
)
