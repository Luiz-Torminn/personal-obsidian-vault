---
type: concept
tags: [sql, database, relational]
---
# Relational Database Fundamentals

The relational model organizes data into tables that are linked based on shared data.

### Related Tables
- **Foreign Key (FK)**: A column that references a Primary Key in a "parent" table. 
- **Data Integrity**: Foreign keys prevent disagreements. You cannot delete a parent row if children exist, nor create a child with a non-existent foreign key value.

### Joining Data
To combine tables, use the `JOIN` command (the Cartesian product filtered by a condition).

```sql
SELECT 
    col1_new_table AS custom_name1, 
    col2_new_table AS custom_name2 
FROM table1 
JOIN table2 ON table1.column = table2.column;
```

- `AS`: Alias for column names.
- `ON`: The filter logic for the join.