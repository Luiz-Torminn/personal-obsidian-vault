---
id: 20260601-1430
type: permanent
tags: [sql, database, programming]
up: "[[* Database MOC]]"
created: 2026-06-04
---
# SQL Language Concepts

SQL is a **Declarative** language.

Unlike imperative programming, you specify **what** you want to retrieve, not **how** the database should retrieve it. Because of this, the most important skill in SQL is learning how to design "smart questions" (queries) rather than focusing on the underlying algorithm.

## Rules

Rules dictate how you write code to interact with databases.

```sql
CREATE TABLE users (
  id           INT PRIMARY KEY,
  email        VARCHAR(255) UNIQUE,
  display_name VARCHAR(100) NOT NULL
);
```

### Constraint

Constraints enforce rules on table data to improve consistency and reliability.

### Primary Key

^f77a46

- Definition and usage of primary keys [[#^f77a46 |here]].
- _Used with key values._
- When using a constraint:
    - Explicitly naming it improves understanding and maintainability.

### Unique

- Ensures values in a column (or set of columns) are unique.
- _Used with non-key values._
- Can contain `NULL` values (behavior can vary slightly by database, but multiple `NULL`s are commonly allowed).

```sql
CREATE TABLE users (
  id    INT PRIMARY KEY,
  email VARCHAR(255) UNIQUE
);
```

### NULL

`NULL` means “no value” / “unknown”. It is not the same as `0` or an empty string.

```sql
INSERT INTO users (id, email) VALUES (1, NULL);
```

### NOT NULL

`NOT NULL` prevents the column from storing `NULL`, forcing a value to be provided.

```sql
CREATE TABLE users (
  id    INT PRIMARY KEY,
  email VARCHAR(255) NOT NULL
);
```

## Referential Actions

Referential actions define what happens to rows in a child table when the referenced row in the parent table is updated or deleted.

Types:

- `RESTRICT` (block the change if dependent rows exist)
- `CASCADE`
- `SET NULL`

```sql
CREATE TABLE orders (
  id      INT PRIMARY KEY,
  user_id INT,
  CONSTRAINT fk_orders_user
    FOREIGN KEY (user_id)
    REFERENCES users(id)
    ON DELETE SET NULL
    ON UPDATE CASCADE
);
```