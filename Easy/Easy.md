# SQL StrataScratch EASY Difficulty Questions

### Question 1 ID:2024
> #### Unique Users Per Client Per Month
> Write a query that returns the number of unique users per client for each month. Assume all events occur within the same year, so only month needs to be be in the output as a number from 1 to 12.
>
>     SELECT client_id,
>            MONTH(time_id) AS m,
>            COUNT(DISTINCT user_id) AS user_num
>     FROM fact_events
>     GROUP BY client_id, m;

### Question 2 ID:2056
> #### Number of Shipments Per Month
> Write a query that will calculate the number of shipments per month. The unique key for one shipment is a combination of shipment_id and sub_id. Output the year_month in format YYYY-MM and the number of shipments in that month.
>
>      SELECT DATE_FORMAT(shipment_date, '%Y-%m') AS year_months,
>             COUNT(shipment_id) AS shipments
>      FROM amazon_shipment
>      GROUP BY year_months;

