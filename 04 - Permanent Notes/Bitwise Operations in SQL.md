---
tags:
---
# Bitwise Operations in SQL
SQL does in fact support bitwise operation! The same syntax applies:
- & for AND
- | for OR
- ~ for NOT
- ^ for XOR
- >> for SHIFT RIGHT (Divide by 2)
- << for SHIFT LEFT (Multiply by 2)
```SQL
SELECT * FROM bitwise
WHERE
	column1 & column2 = 3; -- c1 AND c2 = 101;
```
We can also do bitwise assignment
```SQL
DECLARE @bitwise = 1;
SET @bitwise &= 3;
SELECT @bitwise;
```


---
Categories: [[SQL]]
References:
