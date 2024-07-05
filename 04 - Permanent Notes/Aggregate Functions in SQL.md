---
tags:
---
# Aggregate Functions in SQL
Aggregate Functions will give aggregated results of column(s), such as average or minimum. Aggregate functions are used in tandem with GROUP BY functions to get the function results by certain condition. For example, we may not want to find the average price of fruit of the entire table, rather average price by country.
```SQL
SELECT AVG(Price) FROM FruitPrice
GROUP BY Country;
```
## COUNT
Returns the number of rows
```SQL
SELECT COUNT(student) FROM FavoriteLanguage
GROUP BY language;
```
## AVG
Returns the Average Value.
## SUM
Returns the sum of all column values.
```SQL
SELECT SUM(column1) FROM table1
GROUP BY column2;
```
## MIN, MAX
Returns the minimum/maximum value of a given column.
```SQL
SELECT MIN(Price), MAX(Price) FROM FruitPrices
GROUP BY Country;
```
## HAVING Clause
The `WHERE` equivalent for aggregate functions is the `HAVING` clause.
```SQL
SELECT MAX(Price) FROM FruitPrices
GROUP BY Country
HAVING COUNT(Fruit) > 3;
```
## Aggregate Functions with Conditionals
You can add CASE statements within Count for conditional counting:
```SQL
SELECT
	ad_id,
	COUNT(CASE WHEN event_type = "impression" THEN 1 ELSE NULL END) AS i,
	SUM(CASE WHEN event_type = "click" THEN 1 ELSE 0 END) AS c
FROM
	table1;
```

## Caution on GROUP BY
When we use `GROUP BY`, we need to make sure that all the columns we want to return in the `SELECT` statement is "affected" by this grouping. For example,
```SQL
SELECT
	ID,
	MAX(column1) AS MAXC1,
FROM
	table1
GROUP BY
	column2;
```
Will _NOT_ work because SQL doesn't know what ID to show when grouped by column2. Normally we'd want it to be the ID where the max value resides, but SQL does not assume in such ways.
In cases like these, [[Window Functions in SQL|Partitioning]] would be a better option:
```SQL
SELECT
	ID,
	column1
FROM
	SELECT
		ROW_NUMBER() OVER(PARTITION BY column2 ORDER BY column1 DESC) as rank
		ID
	FROM table1
AS tmp
WHERE
	rank = 1;
	--This would be the one with the highest column1 value per column2 partitions
	
		
```


---
Categories: [[SQL]]
References:
