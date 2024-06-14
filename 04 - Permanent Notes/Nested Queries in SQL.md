---
tags:
  - NeedWork
---
# Nested Queries in SQL
``` SQL
SELECT * FROM shows
WHERE id IN 
(SELECT show_id FROM ratings WHERE rating >= 6.0);
```

---
Categories: [[SQL]], [[Database]], [[CS50 - Introduction]]
References:
Created: 2024-06-13
