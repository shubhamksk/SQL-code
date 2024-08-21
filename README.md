SQL queries used to query the Vehicle Coupon dataset

SELECT *
FROM dataset_1 d ;

--Select, Where and Order By Clause
SELECT 
destination,
passanger ,
time as 'The Time'
from	dataset_1
WHERE passanger = 'Alone'
or time ='2pm'
order by time DESC ;

--Aggregate Functions and Group By

SELECT destination, avg(temperature), ROUND(avg(age),1)
from dataset_1 d 
group by destination;
 
 SELECT destination, weather, ROUND(AVG(temperature),2) as 'Average Weather'
 FROM dataset_1 d 
 group by destination, weather;

--Having Clause
SELECT weather, destination , time, ROUND(AVG(temperature),2) as 'Average Weather'
FROM dataset_1 d 
WHERE destination <> 'Home'
group by weather, destination, time
HAVING time = '10AM';

SELECT weather, AVG(temperature) 
FROM dataset_1 d
GROUP BY weather
HAVING weather ='Sunny';

SELECT gender, COUNT(gender), ROUND(AVG(age),2)
from dataset_1 d
group by gender
HAVING maritalStatus = 'Single';

--Union Test Query to check if Union is Working
SELECT DISTINCT destination 
from dataset_1 d ;

--Joins and Unions Combining Data
--Combining Data Using Union while removing duplicates
SELECT *
from dataset_1 d
union
select *
from table_to_union ttu;

--Subquery-->selecting distinct destination using the Combined Table after Union inside a subquery.
SELECT DISTINCT destination
from
(
SELECT *
from dataset_1 d
union
select *
from table_to_union ttu
);

--Combining Data Using Union ALL to keep duplicates
SELECT *
from dataset_1 d
union ALL
select *
from table_to_union ttu;

--Subquery-->selecting distinct destination using the Combined Table after Union ALL inside a subquery.
SELECT DISTINCT destination
from
(
SELECT *
from dataset_1 d
union ALL
select *
from table_to_union ttu
);

--Using the Join to map time and part_of_data from tables_to_join with dataset 1 values

SELECT destination , d.time, ttj.part_of_day
from dataset_1 d
left join table_to_join ttj 
on d.time = ttj.time;
