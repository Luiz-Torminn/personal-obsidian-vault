---
type: process
tags: [development, workflow]
---
# Database Design Process

The lifecycle of creating a database schema involves three main stages:

### 1. Requirements Gathering
- Focus on business information and user needs.

### 2. Analysis and Logic

- **Identify Subjects and Characteristics**: 
	- Use the "HAS/OWNS" rule: A "User" (Subject/Entity) HAS a "Password" (Characteristic/Attribute).
	- Naming convention: Use `snake_case` or `camelCase` consistently. Keep names short.
	- Use keywords
- [[Database Normalization |Normalization]]: Break tables into smaller, logical units to reduce redundancy.
- [[Relationship Mapping]]: Define how entities interact.

> [!NOTE]
> - Subject/Entity is a table and Characteristic/Attribute is a column
> - _Meeting transcripts and AI analysis can help in this step_

^0d2068

### 3. Implementation and Testing
- **Functionality**: Ensure the DB does what is intended.
- **Stress Testing**: Use AI to generate dummy data for performance and security checks.