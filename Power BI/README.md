**You can download my Power BI project using this link:**
[Project in Power BI](https://drive.google.com/file/d/1evOyJN4eY3nDgnj1VwxRyHCmDN_BW7L1/view?usp=drive_link)

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
    
**This project used various charts, the following measures and one additional table created via DAX:**
1) Count critical failures = COUNTROWS(FILTER('Dataset', 'Dataset'[transit_time_days] >= PERCENTILE.INC('Dataset'[transit_time_days], 0.9) && 'Dataset'[delay_status] = "Delayed"))
2) Declared value for delayed = SUMX(FILTER('Dataset', 'Dataset'[delay_status] = "Delayed"), 'Dataset'[declared_value_usd])
3) Delay rate = DIVIDE(COUNTROWS(FILTER('Dataset', 'Dataset'[delay_status] = "Delayed")), COUNTROWS('Dataset'), 0)
4) Gap between median vs average = ABS(MEDIAN('Dataset'[transit_time_days]) - AVERAGE('Dataset'[transit_time_days])) 
5) Outlier delay = IF( MEDIAN('Dataset'[transit_time_days]) < AVERAGE('Dataset'[transit_time_days]), "Yes", "No") 
6) Profit margin = SUMX('Dataset', 'Dataset'[declared_value_usd] - 'Dataset'[shipping_cost_usd]) 
7) Quantity vs shipping cost correlation = 
VAR Average_quantity = AVERAGE('Dataset'[quantity])
VAR Average_shipping_cost = AVERAGE('Dataset'[shipping_cost_usd])
VAR Sumproduct = SUMX('Dataset', ('Dataset'[quantity] - Average_quantity)*('Dataset'[shipping_cost_usd] - Average_shipping_cost))
VAR Quantitysqsum = SUMX('Dataset', ('Dataset'[quantity] - Average_quantity)^2)
VAR Shipping_costsqsum = SUMX('Dataset', ('Dataset'[shipping_cost_usd] - Average_shipping_cost)^2)
RETURN DIVIDE(Sumproduct, SQRT(Quantitysqsum*Shipping_costsqsum), 0)
8) Shipping cost per kg = AVERAGEX('Dataset', DIVIDE('Dataset'[shipping_cost_usd], 'Dataset'[weight_kg], 0)) 
9) Total financial impact = SUMX(FILTER('Dataset', 'Dataset'[transit_time_days] >= PERCENTILE.INC('Dataset'[transit_time_days], 0.9) && 'Dataset'[delay_status] = "Delayed"), 'Dataset'[declared_value_usd])
10) **Table created via DAX** : Commodities with highest declared value and delay rate = 
 VAR Grouped_commodities = SUMMARIZE('Dataset', 'Dataset'[commodity], "total declared value", SUM('Dataset'[declared_value_usd]), "delay rate", DIVIDE(COUNTROWS(FILTER('Dataset', 'Dataset'[delay_status] = "Delayed")), COUNTROWS('Dataset'), 0))
 VAR Median_declared_value = MEDIANX(Grouped_commodities, [total declared value])
 RETURN FILTER(Grouped_commodities, [total declared value] > Median_declared_value)


