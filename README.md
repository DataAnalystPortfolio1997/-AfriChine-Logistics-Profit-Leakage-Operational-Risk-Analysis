**Problem: The board has identified two critical issues:Profit leakage – Shipping costs and transit times vary wildly by transport mode and route, but we don't know which combinations are secretly unprofitable.
Delivery risk – We have no reliable way to predict which shipments will be delayed. Delays cost us penalty fees and lost contracts.
I need you to build a diagnostic framework that identifies exactly where our logistics operation is failing and quantifies the financial impact.**

[Data link](https://docs.google.com/spreadsheets/d/15aPtQZTlqfnfACfkcawgpT7oWdh2TfTs/edit?usp=drive_link&ouid=104791159130726046761&rtpof=true&sd=true)

**I made this project in 4 platforms:**
1. Excel (power query, pivot table, DAX measures, excel functions)
2. PL/SQL
3. Python (numpy, pandas)
4. Power BI (charts, DAX measures)

**Data cleaning, duplicate removal, and other processes were performed in PowerQuery on the original dataset. All programs use the pre-processed dataset.**

**Conclusions drawn from the data analysis:**
1. Top 5 "departure_port + arrival_port" combination by margin : "Qingdao + Dar es Salaam", "Shenzhen + Tema", "Shenzhen + Cairo", "Qingdao + Addis Ababa", "Shanghai + Cairo" .
   Bottom 5 "departure_port + arrival_port" combination by margin : "Shanghai + Mombasa", "Guangzhou + Durban", "Shenzhen + Addis Ababa", "Beijing + Tema", "Beijing + Lagos" .
2. The most cost-efficient on a per-kilogram basis transport mode is "Ship", shipping cost per kg = 0.44 .
3. The percentage difference between shipments that were Delayed and On-Time shipments = 0.31% .
4. Commodities with the highest total declared value but also the highest delay rate : "Minerals", "Machinery" .
5. Shipments flagged as anomaly flag are systematically overpaying, shipping cost per kg for anomaly shipments vs non-anomaly shipments (2.61 , 2.46) .
6. Top 3 departure ports with the highest average delay status = 'Delayed' rate : "Qingdao", "Shanghai", "Guangzhou" .
   Total declared value usd lost to delays from these ports : 35,019,919 , 33,681,168 , 32,835,108 .
7. Correlation between quantity and shipping cost usd per transport_mode : (Air, 0.34) , (Rail,	0.35) , (Road,	0.32) , (Ship,	0.31) .
   Does shipping more units always mean higher relative costs? - No (weak relationship between indicators) .
8. There is not import country where the average shipping cost usd exceeds the average declared value usd per shipment .
9. There are not outlier delays. "Air" transport mode has the largest gap between median transit time and average transit time .
10. "Minerals" commodity has max count of Critical Failures and the total financial impact (declared_value_usd lost) : (49 ; 4,316,679$)
