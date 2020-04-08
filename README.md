# 1st-SQL-project
source from codecademy

/*World Population Practice*/

-- How many entries in the database are from Africa?

SELECT COUNT(*)
FROM countries
WHERE continent = "Africa";

/*Answer = 56*/

-- What was the total population of Oceania in 2005?

WITH joint_table AS (
SELECT *
FROM population_years
LEFT JOIN countries
ON population_years.country_id = countries.id)
SELECT SUM(population)
FROM joint_table
WHERE continent = "Oceania" and year = "2005";

/*Answer = 32.66417*/

-- What is the average population of countries in South America in 2003?

WITH joint_table AS (
SELECT *
FROM population_years
LEFT JOIN countries
ON population_years.country_id = countries.id)
SELECT name, AVG(population)
FROM joint_table
WHERE continent = 'South America' AND year = '2003'
GROUP BY 1
ORDER BY 2 DESC;

/*Answer :
Brazil|183.95992
Colombia|40.35102
Argentina|38.33688
Peru|27.2752
Venezuela|24.54543
Chile|15.67191
Ecuador|13.07418
Bolivia|8.71906
Paraguay|5.72855
Uruguay|3.38734
Guyana|0.77981
Suriname|0.44993
French Guiana|0.18692
Falkland Islands (Islas Malvinas)|0.00297*/

-- What country had the smallest population in 2007?

WITH joint_table AS (
SELECT *
FROM population_years
LEFT JOIN countries
ON population_years.country_id = countries.id)
SELECT name, MIN(population)
FROM joint_table
WHERE year = "2007";

/*Answer:
Niue|0.00216*/


-- What is the average population of Poland during the time period covered by this dataset?

WITH joint_table AS (
SELECT *
FROM population_years
LEFT JOIN countries
ON population_years.country_id = countries.id)
SELECT name, AVG(population)
FROM joint_table
WHERE name = "Poland";

/*Answer:
Poland|38.5606790909091*/

-- How many countries have the word "The" in their name?

SELECT COUNT(DISTINCT name)
FROM countries
WHERE name LIKE '%The%';

/*Answer = 4*/


-- What was the total population of each continent in 2010?

WITH joint_table AS (
SELECT *
FROM population_years
LEFT JOIN countries
ON population_years.country_id = countries.id)
SELECT continent, SUM(population)
FROM joint_table
WHERE year = '2010'
GROUP BY 1
ORDER BY 2 DESC;
   
/*Answer:
Asia|4133.09148
Africa|1015.47846
Europe|723.06044
North America|539.79456
South America|396.58235
Oceania|34.95696*/
