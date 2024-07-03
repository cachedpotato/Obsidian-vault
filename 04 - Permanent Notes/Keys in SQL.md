---
tags:
---
# Keys in SQL

## Primary Key
While we can only have one primary key constraint per table, that primary key can have multiple columns. This can come in handy for "connector" tables that connects many-to-many relations:
```SQL
CREATE TABLE userRoles (
	userId INTEGER NOT NULL,
	roleId INTEGER NOT NULL,
	PRIMARY KEY (userId, roleId),
);
```
## Foreign Key
Foreign Key are references to primary keys in other tables. Unlike Primary Keys, There can be multiple Foreign Keys in a table.
```SQL
CREATE TABLE IHAVEREFERENCE (
	id INTEGER AUTO_INCREMENT UNIQUE,
	fk INTEGER NOT NULL,
	fk2 INTEGER NOT NULL,
	name VARCHAR(10) NOT NULL,
	FOREIGN KEY fk REFERENCES SOMEOTHERTABLE(id),
	FOREIGN KEY fk2 REFERENCES YETANOTHERTABLE(id)
);
```





---
Categories: 
References:
