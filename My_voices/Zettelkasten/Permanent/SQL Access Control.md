---
id: 20260601-1500
type: permanent
tags: [sql, database, security, access-control]
up: "[[* Database MOC]]"
created: 2026-06-04
---
# What is it

SQL access control limits what users (or applications) can read or modify in a database. It is a key part of enforcing the **principle of least privilege**.

# Access Control Process

1. Create a role

```sql
CREATE ROLE app_readonly;
```

2. Grant permissions

```sql
GRANT SELECT ON TABLE public.users TO app_readonly;
```

3. Assign the role

```sql
GRANT app_readonly TO some_user;
```

## Example (full workflow)

```sql
-- 1) Create role
CREATE ROLE app_readonly;

-- 2) Grant permissions
GRANT SELECT ON TABLE public.users TO app_readonly;
GRANT SELECT ON TABLE public.orders TO app_readonly;

-- 3) Assign role to a user
GRANT app_readonly TO some_user;
```
