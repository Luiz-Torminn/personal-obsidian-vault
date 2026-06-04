---
type: concept
tags: [database, architecture, design]
---
# Meaning

The visual representation of how [[Database Design Process#^0d2068 |entities]] interact and relate to each other within a database schema.

# Cardinality

## What is it

Cardinality defines the numerical constraints of a relationship by specifying how many instances of one entity can be associated with instances of another entity (e.g., 1:1, 1:N, N:M).

## Syntax

### How to Read

![[Captura de Tela 2026-06-01 às 08.09.41.png|340]]

### Symbol Meaning

![[Captura de Tela 2026-06-01 às 08.09.55.png|341]]

## Types of Relationship

### One to one (1:1)

Each record in Table A can be associated with only one record in Table B, and vice versa.
### One to many (1:N)

A single record in Table A can be related to multiple records in Table B, but a record in Table B relates back to only one record in Table A. 
### Many to many (N:M)

Multiple records in Table A can be associated with multiple records in Table B. In relational database implementation, this is achieved by creating a "Junction Table" (or Associative Table) that maps the Primary Keys of both entities.