---
tags:
---
# An Introduction to SQL
SQL (pronounced "sequel") is a _DECLARATIVE_ language to interact with online database. SQL follows the CRUD operations, where data can be used in only four ways:

- CREATE: create new data
- READ: read preexisting data
- UPDATE: change preexisting data
- DELETE: remove data from database

## Basics
1) creating a `.db` file
SQL languages (such as sqlite3) uses the `.db` extension for databases. using this, we can use the CRUD operations for data manipulation. To create a `.db` file from a local `.csv` file, we do the following:
```SQL
sqlite3 database.db
.mode csv
.import file.csv database
.quit
```
we can then access this database file again when we do `sqlite3 database.db` again. The `sqlite3` command will put us into `sqlite3` "mode", where everything we time then will be considered an SQL command. to exit, simply do `.quit`

2) getting the schema
Let's say we got a database from the internet, but we do not know how it actually is structured. a `schema` is basically the blueprint of the database, and outlines what columns there are, the types each columns are associated to, and its [[Keys in SQL|keys]]. An example schema would look like this:
```SQL
sqlite3 > .schema database
CREATE TABLE database {
	id INTEGER,
	name TEXT NOT NULL,
	year NUMERIC,
	episodes INTEGER,
	PRIMARY KEY(id),
}
sqlite3 > .schema database2
CREATE TABLE database2 {
	shows_id INTEGER,
	ratings INT NOT NULL,
	FOREIGN KEY(shows_id) REFERENCES database(id)
}
```

3) accessing the database
SQL command generally follows the form of `COMMAND something COMMAND something`. Note that commands are all capitalized. let's try to get all the contents of our database:
```SQL
SELECT * FROM database
+----------+---------+---------+
|COLUMN    |COLUMN   |COLUMN   |
+------------------------------+
|ROW ...-- I'm too lazy
```
the `*` is the wildcard operator, and we can replace this with specific column name(s), like so:
```SQL
SELECT name, age FROM database
+---------+----------+
| name    | age      |
+---------|----------+
| sth     | sth... 
```

## Useful Commands
There are some useful commands in SQL we should know to fully utilize the database
1) AVG
``` SQL
SELECT AVG(price) FROM database;
```
3) COUNT: give the total number of rows/columns passed into the function argument
```SQL
SELECT COUNT(*) FROM database;
```
3) DISTINCT: gives unique entries within a given column
```SQL
SELECT DISTINCT(language) FROM database;
```
4) MAX: gives the max value of column
```SQL
SELECT MAX(price) FROM database;
```
5) MIN: gives the min value of column
6) UPPER: change text into uppercase
```SQL
SELECT UPPER(languages) FROM database as capitalizedLanguages;
```
7) LOWER: change text into lowercase
8) SUM: Sum of values
```SQL
SELECT SUM(Price) FROM database
WHERE Country = "Germany";
```

...The list goes on. We can also mix call functions within functions, such as `SELECT COUNT(DISTINCT(column)) FROM database`. The example here will give us the total number of unique entries in column `column`.

## Useful Predicates
These predicates are used to further filter out the data we do not need.

1) WHERE
```SQL
SELECT language FROM database WHERE country = "Korea";
```
Note that if queries get too long we can split it with newlines.
```SQL
SELECT languages FROM database
WHERE country = "Korea";
```
_SQL USES SINGLE EQUATIONS FOR COMPARISONS!_
To add multiple conditions, use `ADD` or `OR`.
```SQL
SELECT languages FROM database
WHERE country="Korea" AND population >= 1000000;
```

2) NOT
```SQL
SELECT * FROM database
WHERE NOT City = "Berlin"; 
```
For every condition that needs the `NOT` clause, we need to add one at the front of said condition.
```SQL
SELECT * FROM database
WHERE NOT City = "Berlin" AND
NOT City = "Seoul";
```

4) LIKE: used to search _patterns_. Rules include:
- `%` represent 0 or more characters
- `_` represent single character
```SQL
SELECT language, frequency FROM database
WHERE language LIKE "C%";
+------------+------------+
| language   | frequency  |
+------------+------------+
| C          |  29        |
| C++        |  33        |
| C#         |  5         |
+------------+------------+
```
NOT Operator can be applied:
```SQL
SELECT language, frequency FROM database
WHERE language NOT LIKE "C%";
```
As well as grouping values!
```SQL
SELECT language, frequency FROM database
WHERE language LIKE "[abc]%b_thon";
```
This will choose entries that starts with a, b or c, then the rest of the conditional. Like in Regex, ranges work as well.
```SQL
SELECT language, frequency FROM database
WHERE language LIKE "[a-f]%b_thon";
```
To _exclude_ letters/numbers in groups, put `!` within the brackets:
```SQL
SELECT language, frequency FROM database
WHERE language LIKE "[!acf]%b_thon";
```

3) ORDER BY: sort the returned table by given column's values
```SQL
SELECT * FROM database
ORDER BY columnname;
```


4) LIMIT: limits the amount of rows returned
```SQL
SELECT * FROM database
LIMIT 3;
```


5) GROUP BY: Group rows into, well, groups, given by some condition. The commands will done in a per-group basis. Full syntax of `GROUP BY` is as follows:
```SQL
SELECT column1, column2 FROM database
WHERE condition LIKE "pattern"
GROUP BY column3
ORDER BY column4;
```

6) IN: Just like the python's `in` syntax. Checks if a column value is within the given list.
```SQL
SELECT column1, column2 FROM database
WHERE column1 in ("Name1", "Name2", "Name3");
```
Unlike the `LIKE` operator where we used `[]`, we use `()` here. Of course, `NOT` can be applied here too:
```SQL
SELECT column1, column2 FROM database
WHERE column1 NOT IN ("Name1", "Name2", "Name3");
```

7) BETWEEN: For selecting values within a set range. Uses `BETWEEN x AND y` syntax. Note that both start and end is inclusive so `BETWEEN 10 AND 20` means 10 to 20 inclusive.
```SQL
Select column1, column2 FROM database
WHERE column3 BETWEEN 30 AND 40;
```

```SQL
Select column1, column2 FROM database
WHERE column3 NOT BETWEEN 30 AND 40;
```
Cool part about this is that we can use string values as well
```SQL
Select column1, column2 FROM database
WHERE column3 BETWEEN "Banger" AND "Tweet";
```

8) AS: Creates an Alias
```SQL
Select column1, column2, column3 from database
where column3 LIKE "A_[b-f]%d" AS randomView;
```

9) CASE: Views created with `WITH` cannot be used within CASE statements nor can we make aliases within an arm.
```SQL
SELECT
	CASE
		WHERE Name IN ("John", "Katie") THEN "Hi"
		WHERE Name IN ("Bob", "Jason") THEN "Hello"
		ELSE "Howdy"
	END
FROM database
ORDER BY Name ASC;
```
### Null
Instead of equal sign, we use `IS NULL` for checking if a certain value is null
```SQL
SELECT * FROM database
WHERE Country is NULL;
```


---
Categories: [[CS50 - Introduction]], [[Database]], [[SQL]]
References:
Created: 2024-06-13
