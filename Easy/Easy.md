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

### Question 3 ID:9622
> #### Number Of Bathrooms And Bedrooms
> Find the average number of bathrooms and bedrooms for each city’s property types. Output the result along with the city name and the property type.
>
>     SELECT city,
>            property_type,
>            AVG(bathrooms) AS bathroom,
>            AVG(bedrooms) AS bedroom
>     FROM airbnb_search_details
>     GROUP BY city, property_type;

### Question 4 ID:9653
> #### MacBookPro User Event Count
> Count the number of user events performed by MacBookPro users.
>Output the result along with the event name.
>Sort the result based on the event count in the >descending order.
>
>     SELECT event_name, COUNT(event_name)
>     FROM playbook_events
>     WHERE device = "macbook pro"
>     GROUP BY event_name
>     ORDER BY COUNT(event_name) DESC;

### Question 5 ID:9663
> #### Most Profitable Financial Company
> Find the most profitable company from the financial sector. Output the result along with the continent.
>
>     SELECT company, continent
>     FROM forbes_global_2010_2014
>     WHERE sector = "Financials"
>     AND profits = (SELECT MAX(profits) FROM forbes_global_2010_2014);

### Question 6 ID:9688
> #### Churro Activity Date
> Find the inspection date and risk category (pe_description) of facilities named 'STREET CHURROS' that received a score below 95.
>
>     SELECT activity_date,
>            pe_description
>     FROM los_angeles_restaurant_health_inspections
>     WHERE facility_name = "STREET CHURROS"
>     AND score < 95;

### Question 7 ID:9728
> #### Number of violations
> You are given a dataset of health inspections that includes details about violations. Each row represents an inspection, and if an inspection resulted in a violation, the violation_id column will contain a value.
>
> Count the total number of violations that occurred at 'Roxanne Cafe' for each year, based on the inspection date. Output the year and the corresponding number of violations in ascending order of the year.
>
>     SELECT
>       EXTRACT(YEAR FROM inspection_date) AS "Year",
>       COUNT(violation_id)
>     FROM sf_restaurant_health_violations
>     WHERE business_name = "Roxanne Cafe"
>     GROUP BY year;

### Question 8 ID:9845
> #### April Admin Employees
> Find the number of employees working in the Admin department that joined in April or later, in any year.

>
>     SELECT COUNT(worker_id) AS n_admins
>     FROM worker
>     WHERE
>         department = "Admin"
>         AND MONTH(joining_date) >= 4;

### Question 9 ID:9847
> #### Workers by Department Since April
> Find the number of workers by department who joined on or after April 1, 2014.
>
> Output the department name along with the corresponding number of workers.
>
> Sort the results based on the number of workers in descending order.
>
>     SELECT
>         department,
>         COUNT(worker_id) AS no_of_workers
>     FROM worker
>     WHERE joining_date > '2014-04-01'
>     GROUP BY department
>     ORDER BY no_of_workers DESC

### Question 10 ID:9891
> #### Customer Details
> Find the details of each customer regardless of whether the customer made an order. Output the customer's first name, last name, and the city along with the order details.
> Sort records based on the customer's first name and the order details in ascending order.
>
>     SELECT
>         c.first_name,
>         c.last_name,
>         c.city,
>         o.order_details
>     FROM customers AS c
>     LEFT JOIN orders AS o
>         ON c.id = o.cust_id
>     ORDER BY c.first_name ASC;

### Question 11 ID:9913
> #### Order Details
> Find order details made by Jill and Eva.
> Consider the Jill and Eva as first names of customers.
> Output the order date, details and cost along with the first name.
> Order records based on the customer id in ascending order.
>
>     SELECT
>         o.order_date,
>         o.order_details,
>         o.total_order_cost,
>         c.first_name
>     FROM customers AS c
>     INNER JOIN orders AS o
>         ON c.id = o.cust_id
>     WHERE c.first_name IN ("Jill", "Eva")
>     ORDER BY c.id ASC

### Question 12 ID:9917
> #### Average Salaries
> Compare each employee's salary with the average salary of the corresponding department.
> Output the department, first name, and salary of employees along with the average salary of that department.
>
>     SELECT
>         department,
>         first_name,
>         salary,
>         AVG(salary) OVER (PARTITION BY department) AS avg_sal
>     FROM employee

### Question 13 ID:9991
> #### Top Ranked Songs
> Find songs that have ranked in the top position. Output the track name and the number of times it ranked at the top. Sort your records by the number of times the song was in the top position in descending order.
>
>     SELECT
>         trackname,
>         COUNT(position) AS ntimes
>     FROM spotify_worldwide_daily_song_ranking
>     WHERE position = 1
>     GROUP BY trackname
>     ORDER BY ntimes DESC

### Question 14 ID:9992
> #### Artist Appearance Count
> Find how many times each artist appeared on the Spotify ranking list.
> Output the artist name along with the corresponding number of occurrences.
> Order records by the number of occurrences in descending order.
>
>     SELECT
>         artist,
>         COUNT(position) AS no_of_times
>     FROM spotify_worldwide_daily_song_ranking
>     GROUP BY artist
>     ORDER BY no_of_times DESC


### Question 15 ID:10003
> #### Lyft Driver Wages
> Find all Lyft drivers who earn either equal to or less than 30k USD or equal to or more than 70k USD.
> Output all details related to retrieved records.
>
>     SELECT *
>     FROM lyft_drivers
>     WHERE yearly_salary <= 30000 OR yearly_salary >= 70000

### Question 16 ID:10061
> #### Popularity of Hack
> Meta/Facebook has developed a new programing language called Hack.To measure the popularity of Hack they ran a survey with their employees. The survey included data on previous programing familiarity as well as the number of years of experience, age, gender and most importantly satisfaction with Hack. Due to an error location data was not collected, but your supervisor demands a report showing average popularity of Hack by office location. Luckily the user IDs of employees completing the surveys were stored.
> Based on the above, find the average popularity of the Hack per office location.
> Output the location along with the average popularity.
>
>     SELECT
>         fe.location,
>         AVG(fhe.popularity)
>     FROM facebook_employees AS fe
>     INNER JOIN facebook_hack_survey AS fhe
>         ON fe.id = fhe.employee_id
>     GROUP BY location

### Question 17 ID:10176
> #### Bikes Last Used
> Find the last time each bike was in use. Output both the bike number and the date-timestamp of the bike's last use (i.e., the date-time the bike was returned). Order the results by bikes that were most recently used.
>
>     SELECT
>         bike_number,
>         MAX(end_time)
>     FROM dc_bikeshare_q1_2012
>     GROUP BY bike_number
>     ORDER BY end_time DESC


### Question 18 ID:10299
> #### Finding Updated Records
> We have a table with employees and their salaries, however, some of the records are old and contain outdated salary information. Find the current salary of each employee assuming that salaries increase each year. Output their id, first name, last name, department ID, and current salary. Order your list by employee ID in ascending order.
>
>     SELECT
>         s.id,
>         s.first_name,
>         s.last_name,
>         s.department_id,
>         s.salary
>     FROM
>         (
>             SELECT
>                 *,
>                 ROW_NUMBER() OVER (PARTITION BY id ORDER BY salary DESC) AS rn
>             FROM ms_employee_salary
>        ) AS s
>     WHERE s.rn = 1
>     ORDER BY s.id ASC;

