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



---
Categories: [[SQL]]
References:
