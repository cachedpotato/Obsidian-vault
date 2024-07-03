---
tags:
---
# Window Functions
Window Functions act similar to aggregate functions, except that the resulting table will _NOT_ be a summarized table. Instead, the result will be cast to individual rows.
![[sql-window-functions.png]]

The basic syntax for window functions are is as follows:
```SQL
[window function name] OVER (
	[partition clause]
	[order clause]
	[frame clause]
)
```

## Partition Clause
Partition clause sets the "group" for the window functions, just like how we use `GROUP BY` for aggregate functions.
```SQL
SELECT ROW_NUMBER() OVER (
	PARTITION BY Name
	ORDER BY Occupation ASC
) AS row_num
FROM table1;
```



---
Categories: 
References:
