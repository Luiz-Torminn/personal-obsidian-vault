---
id: 20260601-1219
type: permanent
tags: [database, logic]
up: "[[* Database MOC]]"
created: 2026-06-04
---
# Database Keys and Identity

Keys are the unique identifiers that ensure data integrity within a table.

---

## Definitions

### Candidate Keys

The smallest possible combination of attributes that can uniquely identify a row. A table can have multiple candidate keys.

### Primary Key (PK)

^77f28a

- The best candidate key chosen for the table (usually the ID). 
- Every table has only ONE primary key
- It can NEVER be a NULL value
- It must NEVER have a duplicate value in the same table

%% If no natural key exists, a **surrogate key** (like an ID) is created. %%

![[Captura de Tela 2026-06-01 às 12.19.17.png|224]]

### Identity (ID)

A column that auto-fills based on an increment rule (e.g., +1 for every new row). It is often used as the Primary Key.

### Functional Dependency

You can ***always*** figure the value of **B** from the value of **A**. If you know A, you know B.

### Transitive Dependency

^f71051

A **non-key** value is dependent on another **non-key** value, which only then is dependent on a primary key.

![[Captura de Tela 2026-06-01 às 10.29.55.png|273]]

> [!ABSTRACT] Analogy
> " Imagine you have a best friend named Alex. Alex has a favorite toy, and that toy has a special name. You only know the toy's name because it belongs to Alex.
> 
> It is like a little chain: To find out the toy's name, you first have to find your friend Alex! One thing leads to another, which leads back to the main person. "

---

Related to: [[Relational Database Fundamentals]]