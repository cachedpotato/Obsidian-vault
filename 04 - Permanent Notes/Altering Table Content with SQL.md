---
tags:
---
# Altering Table Content with SQL
We've seen in the [[SQL CRUD Operators]] How to do basic creation/deletion etc. This is for altering the table values we've created. This is done by the `ALTER` Keyword, and the syntax goes a little something like this:
```SQL
ALTER TABLE database
(OPERATION NAME) (Expression)
WHERE (condition);
```

## Add
Unlike _inserting_ a new data, _adding a column_ requires _altering_ the table, so it uses the `ALTER TABLE` keyword.
```SQL
ALTER TABLE table1
ADD newColumn DATE;
```
When we add columns we must also specify exactly what type that column values are going to be. If we want to set a default value, we need to use the `DEFAULT` keyword:
```SQL
ALTER TABLE table1
ADD newColumn INT(3) DEFAULT 0;
``` 

## Alter Column
Instead of adding a column, we sometimes may want to change column types (for example, maybe using 8 bit integer to store IDs weren't enough). In cases like this, we use the `ALTER COLUMN` operation:
```SQL
ALTER TABLE table1
MODIFY column1 Char(255);
```

If we want to change the name as well, we need to use the `CHANGE` keyword:
```SQL
ALTER TABLE table
CHANGE name nm VARCHAR(15);
```
## Drop Column
If we have column addition, then we must also have the option to drop columns as well. As always, proceed with caution!
```SQL
ALTER TABLE table1
DROP COLUMN column1;
```


---
Categories: [[SQL]]
References:
