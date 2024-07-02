---
tags:
---
# SQL CRUD Operators

## CRUD Operations
### Creation
``` SQL
CREATE TABLE table1 (
	id INTEGER,
	name TEXT NOT NULL,
	air NUMERIC,
	episodes INTEGER,
	PRIMARY KEY(id) NOT NULL
);
```

### Insertion
```SQL
INSERT INTO database (
	id,
	name,
	air,
	episodes
) VALUES = (
	"Ryan Gosling",
	"1998-03-03",
	"3, 4, 6"
);
```
### Adding New Columns
```SQL
ALTER TABLE table1
ADD column1 DATE;
```
### Read
``` SQL
SELECT show, year FROM database
WHERE id IN (SELECT show_id FROM database2
						WHERE main_actor = "Ryan Gosling")
```

### Update
```SQL
UPDATE database
SET column1 = "new1", column2 = "new2", column4 = "new4"
WHERE Country = "Germany";
```

### Delete
```SQL
DELETE FROM database
WHERE column1 = "name1";
```

```SQL
DROP DATABASE database;
```

```SQL
DROP TABLE table1;
```
To delete all related (via Primary/Foreign Key etc.), we need to specify the `CASCADE` keyword.
```SQL
DROP TABLE table1 CASCADE;
```
To do the reverse of this, that is to say don't drop the table if there's related table, we need the `RESTRICT` keyword:
```SQL
DROP TABLE table1 RESTRICT;
```

```SQL
TRUNCATE TABLE table1;
```
_DO NOT USE THE SECOND/THIRD CODE ABOVE NO MATTER WHAT_. This will remove the _ENTIRE DATABASE/TABLE!_ Deletion should always be treated with _extreme_ care, and we need to make sure we have backup in case something goes awry. 






---
Categories: [[SQL]], [[Database]]
References:
Created: 2024-06-13
