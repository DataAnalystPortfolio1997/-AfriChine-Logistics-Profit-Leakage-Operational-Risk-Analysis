**You can view my Excel project online in Microsoft 365 Excel using this link:**
[Project in Excel online](https://1drv.ms/x/c/8f7ed22bb67ac06c/IQADvY2q-hUES7lfzWx-iJaWASy7B5GaPc8fvcR8uLr1DcQ?e=LrnMX9)

**Or you can download this Excel file, but keep in mind that the file must be opened in Excel version 16.0 and in more modern versions of Excel:**
[Project in Excel for download](https://docs.google.com/spreadsheets/d/1gcRLZmxlfD8zAShfLm9HSWq0ZAWLCHdY/edit?usp=drive_link&ouid=104791159130726046761&rtpof=true&sd=true)

**Tasks that were solved in this file:**
1. Profit Margin by Route – Calculate the profit_margin (assuming profit_margin = declared_value_usd - shipping_cost_usd) for each unique departure_port + arrival_port combination.
   Show me the top 5 and bottom 5 routes by margin .
2. Cost Efficiency Index – Create a ranking of transport_mode (Air, Ship, Rail, Road) by shipping_cost_usd per weight_kg. Which mode is the most cost-efficient on a per-kilogram basis?
3. Delay Risk Identification – For shipments that were Delayed, calculate the average transit_time_days compared to the average transit_time_days for On-Time shipments. What is the percentage difference?
4. Commodity Vulnerability Analysis – Identify the top 3 commodities (commodity column) with the highest total declared value but also the highest delay rate (percentage of shipments marked Delayed).
   We need to know where we are risking the most money.
5. Anomaly Flag Investigation – For shipments flagged as anomaly_flag = 1, calculate the average shipping_cost_usd per weight_kg vs. non-anomaly shipments. Are anomalies systematically overpaying?
6. Port Performance Audit – List the top 3 departure ports with the highest average delay_status = 'Delayed' rate. Also show the total declared_value_usd lost to delays from each port.
7. Volume vs. Cost Relationship – Calculate the correlation between quantity and shipping_cost_usd per transport_mode. Does shipping more units always mean higher relative costs?
8. Loss Leader Detection – Identify any specific import_country where the average shipping_cost_usd exceeds the average declared_value_usd per shipment. Show me the countries where we are operating at a loss.
9. Transit Time Efficiency – For each transport_mode, calculate the median transit time and compare it to the mean. 
   If the median is significantly lower than the mean, it indicates outlier delays. Show me which mode has the largest gap.
10. High-Risk Customer Segmentation – Create a flag: shipments with transit_time_days in the top 10% longest durations AND delay_status = 'Delayed' are "Critical Failures." 
    Provide the count of Critical Failures by commodity and the total financial impact (declared_value_usd lost).

**The assignments were completed by creating a pivot table and pivot measures for each assignment separately. Each assignment was completed in a new Excel sheet.**
