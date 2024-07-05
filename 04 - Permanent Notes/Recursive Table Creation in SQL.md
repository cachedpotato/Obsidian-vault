---
tags:
---
# Recursive Table Creation in SQL
Consider a data like this:

| ID  | PARENT_ID | SIZE_OF_COLONY | DIFFERENTIATION_DATE |
| --- | --------- | -------------- | -------------------- |
| 1   | NULL      | 10             | 2019/01/01           |
| 2   | NULL      | 2              | 2019/01/01           |
| 3   | 2         | 100            | 2020/01/01           |
| 4   | 2         | 15             | 2020/01/01           |
| 5   | 2         | 19             | 2020/01/01           |
| 6   | 4         | 101            | 2021/01/01           |
| 7   | 4         | 101            | 2021/01/01           |
| 8   | 7         | 1              | 2022/01/01           |
We want to find the generation number for each colony. For example, 1 and 2 is generation 1, colonies 3, 4 and 5 is generation 2 because they come from colony 2 which is generation 1, etc.

Using standard SQL queries, this seem quite the impossible task to automate. Do we really need to do this one by one?
Fear not - Recursive function is here to help!

This is what we're going to do.
1) Define base case: Generation 1, which are colonies with no parents
2) Generation n will have parents from Generation n - 1. Define this with standard SQL syntax (which we'll see in a minute)
3) `UNION ALL` the generations into a single table
4) Don't forget to use the `RECURSIVE` Keyword!

```SQL
WITH RECURSIVE GENDATA AS (
	--base case
	SELECT
		ID,
		PARENT_ID,
		1 AS GENERATION --first gen
	FROM
		ECOLI_DATA
	WHERE
		PARENT_ID IS NULL

	UNION ALL
	--recursive definition
	SELECT
		D.ID,
		D.PARENT_ID,
		GENDATA.GENERATION + 1 AS GENERATION
	FROM
		--GENDATA acts as previous
		--ECOLI_DATA acts as the current
		GENDATA JOIN ECOLI_DATA D
		ON GENDATA.ID = D.PARENT_ID
)
SELECT * FROM GENDATA;
```
This process is somewhat similar to the induction process, where
- we define the first case
- we define case n in relation to n + 1




---
Categories: [[SQL]]
References:
