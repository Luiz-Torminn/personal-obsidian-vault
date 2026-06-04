---
id: 20260601-1400
type: permanent
tags: [sql, database, development, reference]
up: "[[* Database MOC]]"
created: 2026-06-04
---
# SQL Data Types

Choosing the correct data type is essential for storage optimization and performance.

## Primitive Data Types

### String Types

- **Char**: Used for strings with fixed and uniform lengths (e.g., Typically used for <= 100 characters). ^6e49b1
- **Varchar**: Used for variable lengths with a specified maximum (e.g., `VARCHAR(255)`, >= 100 characters).
- **Text**: For large-scale string storage.

### Numeric Data Types

- **Int**: For whole numbers.
- **Float**: For approximate decimal values.
	- 32-bit: 7 decimal digit precision.
	- 64-bit: 15 decimal digit precision.
- **Decimal**: For exact decimal values.
	```sql 
	DECIMAL(P, S)
	```
	%% P = Precision (Total number of digits) %%
	%% S = Scale (Number of decimal digits) %%
### Time and Dates

- **Date**: Stores a fixed calendar date .
- **Time**: Stores a fixed time of day.
- **Datetime**: Stores a date and time combination that remains fixed *regardless* of timezone.
- **Timestamp**: Stores a date and time combination that *adjusts* to the client's local timezone (stored in UTC).

- **Timestamp vs. Datetime**: 
	- Use **Timestamp** for global applications where the time context needs to adapt to the viewer's location.
	- Use **Datetime** for fixed calendar events and historical records.

## Special Data Types

### Enum 

Fixed set of values that are stored as integer indexes mapping to their position in the defined list.

```sql
ENUM('Low', 'Medium', 'High')
```

(e.g., `'Low' = 1`, `'Medium' = 2`, `'High' = 3`)

---

> [!NOTE]
> You can always use AI to help you set the data types.
