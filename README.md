# Databases — Laboratory Work (Fall 2026)

## 1. Work environment and workflow

- **DBMS:** PostgreSQL 18.6 (Homebrew, macOS)
- **Interfaces:** `psql` in macOS Terminal; pgAdmin 4 for database structure and ER diagrams
- **Version control:** Git / GitHub
- **Submission format:** folders per lab; primarily numbered screenshots of executed commands and their output, with diagrams and exported files where applicable

**Practical workflow:** connect to the required database → inspect tables with `\dt` / `\d` → execute SQL in `psql` → verify results with `SELECT` and constraint checks → capture terminal/pgAdmin evidence → upload files to the corresponding lab folder.

Example commands (run in the appropriate environment):

```bash
# macOS Terminal: connect to a database
psql -h localhost -p 5432 -U <username> -d coffee_shop
```

```text
-- Inside psql (meta-commands do not require a semicolon)
\dt
\d products
```

> **Reproducibility note:** Most labs were performed interactively. Screenshots document the queries and their results; the repository should not be treated as a fully automated collection of executable SQL scripts.

## 2. Databases and schemas used

| Database | Tables / objects used | Purpose |
|---|---|---|
| `coffee_shop` | `products`, `orders`; an additional `import_test` table for Lab 17 | Data types, constraints, aggregation, joins, CSV import/export, backup |
| `primary_keys_lab07` | `students`, `courses`, `teachers`, `enrollments`, `serial_demo`, `identity_demo`; later `student_profiles`, `course_instructors` | Primary/foreign keys, referential integrity, 1:1 and M:N relationships |
| `university_design_lab09` | `departments`, `students`, `courses`, `enrollments`; an `employees` hierarchy example for recursive queries | ER design, normalization, filtering, joins, CTEs, recursion, set/window operations |
| `basic_operations` | `students` | `INSERT`, `UPDATE`, `DELETE` and bulk data modifications |
| `transactions_lab16` | `accounts` | Transactions, `COMMIT`, `ROLLBACK`, `SAVEPOINT` and ACID experiments |
| `coffee_shop_restore_lab17` | Restored copies of `products`, `orders`, `import_test` | Validation of `pg_dump` / `pg_restore` |

### 2.1 Coffee shop database

```text
products
  product_id         PRIMARY KEY (SERIAL)
  name               UNIQUE, NOT NULL
  category           constrained category values
  description
  price              NUMERIC, CHECK (price > 0)
  is_available       DEFAULT TRUE
  preparation_time
  created_at         DEFAULT CURRENT_TIMESTAMP

orders
  order_id           PRIMARY KEY (SERIAL)
  product_id         FOREIGN KEY -> products.product_id
  quantity           positive integer
  order_date         DATE, default current date
  customer_name
  discount           constrained percentage
  status             constrained order status
```

**Relationship:** `products (1) → (N) orders` through `product_id`. Initial practice data included Cappuccino, Matcha Latte, Americano and Cheesecake. Each order references a product, allowing product names/prices to be retrieved via `JOIN`.

### 2.2 University database

```text
departments(department_id PK, department_name UNIQUE)
      |
      | 1:N
      v
students(student_id PK, student_name, email UNIQUE, department_id FK)
      |
      | 1:N
      v
enrollments(student_id FK, course_id FK, semester, grade)
      ^                    PK = (student_id, course_id, semester)
      | 1:N
      |
courses(course_id PK, course_name, credits CHECK 1..6)
```

`enrollments` is the **junction table** implementing the M:N relationship between students and courses. Sample courses were Databases, Algorithms and Artificial Intelligence. For the recursive-query exercise, a separate `employees` table was introduced with `manager_id` referencing `employees.employee_id`.

### 2.3 Key and constraint exercises (Labs 07–08)

- `students.student_id`: primary key; **an integer PK does not automatically generate IDs** unless a sequence/identity mechanism is configured.
- `teachers.teacher_id`: example of a named primary-key constraint.
- `enrollments`: composite PK `(student_id, course_id, semester)` prevents duplicate enrollment records for the same student, course and semester.
- `student_profiles(profile_id, student_id, phone)`: `student_id` is both **UNIQUE** and a **FOREIGN KEY** to `students`, modeling a 1:1 relationship.
- `course_instructors(course_id, teacher_id)`: junction table with a **composite PK** and two FKs, modeling an M:N relationship.
- Referential actions tested included `ON DELETE CASCADE`, `SET NULL`, `SET DEFAULT`, `RESTRICT` / `NO ACTION`, and `ON UPDATE` behavior.

### 2.4 Data modification and transaction exercises

- `basic_operations.students(student_id, first_name, last_name, birth_date)`: practiced single- and multi-row inserts, conditional updates, deletion and before/after verification.
- `transactions_lab16.accounts(account_id PK, owner_name, balance NUMERIC(10,2))`: includes `CHECK (balance >= 0)` for consistency tests; used to simulate money transfers inside transactions.

## 3. Laboratory index and implementation details

| Lab | Topic / folder | Work performed |
|---|---|---|
| **03** | [Basic psql Commands](Lab-03-PSQL-Basics) | Connected to PostgreSQL; used `\l`, `\c`, `\dt`, `\d`; created and inspected a `students` table. |
| **04** | [First SQL Query](Lab-04-First-SQL-Query) | Practiced `SELECT`, selecting particular columns and inspecting query output. |
| **05** | [Databases Overview](Lab-05-Databases) | Created/accessed databases, changed the active database with `\c`, practiced SQL-file and terminal workflows. |
| **06** | [Tables, Data Types & Constraints](Lab-06-Tables-DT-Constraints) | Created `coffee_shop.products` and `coffee_shop.orders`; used `SERIAL`, `VARCHAR`, `NUMERIC`, `BOOLEAN`, `DATE`, `INTERVAL`, `TIMESTAMP`, defaults, PK, FK, `NOT NULL`, `UNIQUE` and `CHECK`; inserted sample products/orders. |
| **07** | [Primary Keys](Lab-07-PrimaryKeys) | Practiced inline, table-level and named PKs; composite key `(student_id, course_id, semester)`; compared manually supplied IDs, `SERIAL` and identity columns. |
| **08** | [Foreign Keys](Lab-08-ForeignKeys) | Defined inline/table-level FKs and FKs via `ALTER TABLE`; explored `ON DELETE` / `ON UPDATE` behaviors; created `student_profiles` (unique student FK, 1:1) and `course_instructors` (junction table, M:N). |
| **09** | [Database Design Basics](Lab-09-DB-design-basics) | Designed `departments`, `students`, `courses`, `enrollments` in `university_design_lab09`; mapped PK/FK relationships; studied entity–relationship design and 1NF/2NF/3NF. |
| **10** | [Viewing Database & Table Structure](Lab-10-ViewingDB-%26-TableStructure) | Inspected existing tables, attributes, constraints and relationships with `\dt` / `\d` and pgAdmin ER-diagram tools. |
| **11** | [Basic Data Operations](Lab-11-Basic-Data-Operations) | Worked in `basic_operations.students` (`student_id`, `first_name`, `last_name`, `birth_date`); performed single/multi-row `INSERT`, conditional `UPDATE` / `DELETE` and bulk modifications. |
| **12** | [Querying Data](Lab-12-Querying-Data) | Queried university tables with `SELECT`, `WHERE`, `BETWEEN`, `LIKE` / `ILIKE`, regular expressions, `IN`, `EXISTS`, `CASE` and `WITH` (CTEs). |
| **13** | [Aggregate Functions](Lab-13-Aggregate-Functions) | Analyzed `coffee_shop.products` / `orders`: `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`, `GROUP BY` (single/multiple columns), `HAVING`, conditional aggregation, `STRING_AGG`, `ARRAY_AGG`, statistics and window aggregates. |
| **14** | [Joining Tables](Lab-14-Joining-Tables) | Compared `INNER`, `LEFT`, `RIGHT`, `FULL OUTER`, `CROSS` joins on coffee-shop data; used university tables for multi-table joins, self joins and M:N relationships; examined indexes and unmatched records. |
| **15** | [Advanced Querying](Lab-15-Advanced-Querying) | Scalar subqueries, grouped CTEs, `WITH RECURSIVE` for an employee hierarchy, `UNION` / `UNION ALL` / `INTERSECT` / `EXCEPT`, window ranking, `PARTITION BY`, `LAG` / `LEAD`, pivot/unpivot, `FILTER`, custom sorting and `EXPLAIN`. |
| **16** | [Transactions & ACID](Lab-16-Transactions-%26-ACID) | Used `transactions_lab16.accounts` with non-negative balance constraint; tested `BEGIN`, `COMMIT`, `ROLLBACK`, `SAVEPOINT`, isolation levels and ACID scenarios, including balance checks before and after changes. |
| **17** | [Data Import/Export & Backup](Lab-17-Data-Export-Import) | Exported/imported coffee-shop data via `\copy` and CSV; created a custom-format backup with `pg_dump`; restored to `coffee_shop_restore_lab17` using `pg_restore`; checked restored table names and counts. |

## 4. Specific validation: Labs 16–17

### Lab 16 — transaction behavior

The practice `accounts` table uses `account_id` (PK), `owner_name`, and `balance NUMERIC(10,2) CHECK (balance >= 0)`. A transfer is implemented as two `UPDATE` statements inside one transaction:

```sql
BEGIN;
UPDATE accounts SET balance = balance - 300 WHERE account_id = 1;
UPDATE accounts SET balance = balance + 300 WHERE account_id = 2;
COMMIT;
```

Other exercises tested reversing uncommitted changes with `ROLLBACK`, rolling back part of a transaction with `SAVEPOINT`, and rejecting an invalid negative balance via `CHECK`. Isolation and durability were discussed/tested with separate-session visibility and committed data persistence; a reconnect test is not the same as a simulated server crash.

### Lab 17 — export, import, backup and recovery

1. Export selected `products` columns to `lab17_products.csv` using **`\copy ... TO`** (`psql` client-side file access).
2. Import the CSV into the separate `import_test` table using **`\copy ... FROM`**.
3. Create a custom-format `coffee_shop_lab17.dump` archive with **`pg_dump -Fc`** (macOS Terminal).
4. Restore the archive into **`coffee_shop_restore_lab17`** using **`pg_restore`**.
5. Verify the restoration with `\dt` and row counts.

**Verified restored result shown in the terminal:**

| Table | Row count |
|---|---:|
| `products` | 4 |
| `orders` | 4 |
| `import_test` | 4 |

`pg_dump` and `pg_restore` are **shell commands**, while `\copy` is a **psql meta-command**. Full/incremental backup, WAL, PITR and migration strategies were also covered conceptually; production-scale point-in-time recovery was not performed.

## 5. Evidence and limitations

- Screenshots (often `01.png`, `02.png`, etc.) show commands, table definitions and results in their execution order.
- Depending on the lab, additional files may include ER diagrams, CSV exports and a PostgreSQL `.dump` archive.
- Screenshot-based labs document *what was executed*; they are not a replacement for runnable `.sql` files or a complete database dump. Lab 17 additionally documents a tested database restore.
- Numbered screenshots can remain as-is. New screenshots may use descriptive names such as `01-create-tables.png` and `02-verify-joins.png`.
- Lab 01–02 are not represented by folders in this repository; the documented lab portfolio starts at Lab 03.

**Course scope:** relational modeling, SQL DDL/DML, data integrity, normalized schemas, querying and analytics, transactions, indexing concepts, and backup/recovery.
