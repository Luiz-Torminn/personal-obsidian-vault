---
id: 20260601-1005
type: permanent
tags: [database, design, optimization]
up: "[[* Database MOC]]"
created: 2026-06-04
---
# What is it 

The process of organizing tables in a relational database to reduce data redundancy and improve data integrity by ensuring that data is stored logically. 
# Normal Forms (NF) 

Normal Forms are a series of progressive design rules used to organize relational tables.
## First NF

- Criteria: 
	- Every instance within a column has the same datatype
	- Each row is unique
	- Each cell has only ONE value

### Example 

**Bad (Violates 1NF):** 

| Student | Courses       |
| :------ | :------------ |
| Alice   | Math, Science |

**Good (Meets 1NF):** 

| Student | Course  |
| :------ | :------ |
| Alice   | Math    |
| Alice   | Science |
## Second NF (2NF)

- **Criteria**: 
	- Meets all requirements of **1NF**.
	- Every non-key column must be **fully dependent** on the entire Primary Key. 

![[Captura de Tela 2026-06-01 às 10.05.54.png|323]]

## Third NF (3NF)

^0bb316

- **Criteria**:
	- Meets all requirements of **1NF** and **2NF**.
	- It has **NO** [[Database Keys and Identity#^f71051|transitive dependencies]].

	- *Rule of thumb:* Attributes must depend on "single primary key, and nothing but that single primary key."

### Example 

**Bad (Violates 3NF):** 

![[Captura de Tela 2026-06-01 às 11.04.00.png|455]]

**Good (Meets 3NF):** 

![[Captura de Tela 2026-06-01 às 11.04.09.png|317]]

---

> [!NOTE]
> For a table to progress to the next Normal Form, it must satisfy all requirements of the previous normal forms.
> 
> ![[Captura de Tela 2026-06-01 às 09.59.55.png|228]]

# Practical Rule

For most application databases:

- **Use 1NF always**: Never store multiple values in one cell.
- **Aim for 3NF**: This is the standard for most transactional (OLTP) systems.
- **Advanced Forms**: Use BCNF, 4NF, or 5NF only when the specific data model complexity requires it.
- **Denormalize Intentionally**: Only break these rules when performance, reporting, or specific read-heavy requirements (OLAP) justify the redundancy.