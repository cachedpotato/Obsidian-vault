---
tags: []
---
# SQL Join Operations
One can say Join operations are at the core of SQL and data fetching. Because Databases are split up into multiple tables connected mostly by primary/foreign keys, we need to know how to connect the two tables (or more!) to get the exact info that we want. 
For example, we may want to get an Actor's filmography filtered by movie rating. IMDb Stores movie database and actor database separately, so we must first join the two tables. The Join operation uses the following syntax:
```SQL
SELECT * FROM table1 JOIN table2
ON table1.id = table2.f_id
WHERE (conditional);
```
There are 4 main ways of joining a table, plus union. Let's get over one by one.
![[Pasted image 20240701171709.png|600]]

1) (INNER) JOIN
Inner Join will only fetch database if and only if both tables have the column value that the JOIN operation is working on. For example, if there's a show id `0123` in the `shows` table but not in `ratings` table, it will not show up in the inner join. the `JOIN` operation defaults to Inner joins.
```SQL
SELECT title, rating FROM shows JOIN ratings
ON shows.id = ratings.show_id
WHERE rating >= 6.0
LIMIT 10;
```

2) LEFT (OUTER) JOIN
Left Join will include _ALL_ values of the column the join operation will act on, even if the right side table does not have that value. In this case, that part of the join table will be filled with _NULL_.
Unlike Inner joins, Left, Right and Full joins may have some "blank" entries. These are called _Outer Joins_. 
```SQL
SELECT title, rating FROM shows LEFT JOIN ratings
ON shows.id = ratings.show_id
WHERE rating >= 6.0
LIMIT 10;
```
3) RIGHT (OUTER) JOIN
Same as Left Join, but now all entries of the right table will be present.
4) FULL (OUTER) JOIN. As the name suggests, this join will include _ALL_ entries from _BOTH_ tables.
```SQL
SELECT * FROM table1 FULL OUTER JOIN table2
ON shows.id = ratings.show_id
WHERE rating > 6
LIMIT 20;
```

5) UNION
Similar to Join Operations, `UNION` aims to merge two tables/views together. However, unlike join, union uses _ALL THE COLUMNS PROVIDED_. This means that if we're trying to unionize two tables, we need to:
- give the _SAME AMOUNT OF COLUMNS_ for both tables
- the column types must be similar
```SQL
SELECT City, Country FROM Customers
WHERE NOT City = "Berlin"
UNION
SELECT City, Country FROM Suppliers
WHERE NOT City = "Seoul";
```
By default, Union operations will remove duplicates. To allow for duplicates, use `UNION ALL`:
```SQL
SELECT City, Country FROM Customers
WHERE NOT City = "Berlin"
UNION ALL
SELECT City, Country FROM Suppliers
WHERE NOT City = "Seoul";
ORDER BY City;
```


---
Categories: [[SQL]], [[Database]]
References:
Created: 2024-06-13
