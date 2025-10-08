SELECT 
    a.Timestamp,
    ROUND(a.NET_PROD) AS NET_PROD,
    ROUND(a.NET_PRODUCTIVITY, 1) AS NET_PRODUCTIVITY,
    ROUND(a.ACTUAL_AVAILABILITY, 1) AS ACTUAL_AVAILABILITY,
    ROUND(b.FE, 1) AS FE,
    ROUND(b.CAO / DECODE(b.SIO2, 0, NULL, b.SIO2), 2) AS B2,
    ROUND(b.AL2O3, 2) AS AL2O3,
    ROUND(b.P, 3) AS P,
    ROUND(b.K2O, 3) AS K2O,
    ROUND(b.CCS_CRMT) AS CCS_CRMT,
    ROUND(b.TUMBLER_PLS_6P3_MM, 2) AS TUMBLER_PLS_6P3_MM,
    ROUND(b.TUMBLER_MIN_0P5_MM, 2) AS TUMBLER_MIN_0P5_MM,
    ROUND(b.SWELLING_INDEX_CRMT, 2) AS SWELLING_INDEX_CRMT,
    ROUND(b.RDI, 2) AS RDI,
    ROUND(b.RI, 1) AS RI,
   nvl(Avg(case when COST_ELEMENT like '%120000056%' and area like '%100021212%' then ACTUAL_QUANTITY else NULL end),0)+
   nvl(((nvl(Avg(case when COST_ELEMENT like '%120000055%' and area like '%100021212%' then ACTUAL_QUANTITY else NULL end),0)+nvl(avg(case when COST_ELEMENT like '%120000057%' and area like '%100021212%' then ACTUAL_QUANTITY else NULL end),0))/avg(case when COST_ELEMENT like '%100021211%' and area like '%100021211%' then ACTUAL_QUANTITY else NULL end))*1000,0)+
   nvl(((nvl(avg(case when COST_ELEMENT like '%120005660%' and area like '%100021212%' then ACTUAL_QUANTITY else NULL end),0))/avg(case when COST_ELEMENT like '%100021211%' and area like '%100021211%' then ACTUAL_QUANTITY else NULL end))*1000,0)+
   nvl(((nvl(avg(case when COST_ELEMENT like '%120005731%' and area like '%100021212%' then ACTUAL_QUANTITY else NULL end),0)+
nvl(avg(case when COST_ELEMENT like '%120006250%' and area like '%100021212%' then ACTUAL_QUANTITY else NULL end),0)+
nvl(avg(case when COST_ELEMENT like '%120006280%' and area like '%100021212%' then ACTUAL_QUANTITY else NULL end),0))/avg(case when COST_ELEMENT like '%100021211%' and area like '%100021211%' then ACTUAL_QUANTITY else NULL end))*1000,0)
    AS IRON_ORE_FINES
FROM 
    (imtg.t_Pellet_production_monthly a
     FULL OUTER JOIN imtg.t_Pellet_quality_monthly b ON a.Timestamp = b.Date_Time)
FULL OUTER JOIN 
    imtg.T_COST_DATA c ON (a.Timestamp = b.Date_Time OR a.Timestamp = TRUNC(c.Date_Time, 'MON'))

WHERE 
    b.SOURCE = 'PRODUCT'
    AND a.Timestamp IS NOT NULL AND a.Timestamp>='01-APR-2025'

GROUP BY 
    a.Timestamp,
    a.NET_PROD,
    a.NET_PRODUCTIVITY,
    a.ACTUAL_AVAILABILITY,
    b.FE,
    b.CAO,
    b.SIO2,
    b.AL2O3,
    b.P,
    b.K2O,
    b.CCS_CRMT,
    b.TUMBLER_PLS_6P3_MM,
    b.TUMBLER_MIN_0P5_MM,
    b.SWELLING_INDEX_CRMT,
    b.RDI,
    b.RI;
