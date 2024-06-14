---
tags:
  - NeedWork
---
# SQL Join Operations
1) INNER JOIN
```SQL
SELECT title, rating FROM shows JOIN ratings
ON id = show_id
WHERE rating >= 6.0
LIMIT 10;
```
2) LEFT (OUTER) JOIN
3) RIGHT (OUTER) JOIN
4) FULL (OUTER) JOIN
5) UNION

---
Categories: [[SQL]], [[Database]]
References:
Created: 2024-06-13
