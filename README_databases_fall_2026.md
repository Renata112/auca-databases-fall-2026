# Databases — Fall 2026

**American University of Central Asia (AUCA)**  
**Department:** Software Engineering  
**Course:** Databases (COM-424.1) · 6 credits  
**Instructor:** Ph.D., Associate Professor Gulzada Esenalieva  
**Student:** Renata Balbaeva

## About This Repository

This repository documents my hands-on laboratory work for the **Databases** course at AUCA during the Fall 2026 semester. The assignments follow the course syllabus and focus on relational database design, PostgreSQL, SQL queries, data integrity, transactions, and database backup and recovery.

Most exercises were performed interactively using **PostgreSQL's `psql` command-line interface on macOS**. The lab folders primarily contain screenshots of commands and their results; some assignments also include diagrams, CSV data, or backup files. The folder contents are evidence of the work completed and are not necessarily standalone executable SQL projects.

## Tools and Environment

- **PostgreSQL** — relational database management system
- **SQL and psql** — queries, database operations, and command-line practice
- **pgAdmin 4** — inspecting database structure and ER diagrams
- **macOS Terminal** — interactive PostgreSQL commands and backup tools
- **Git and GitHub** — organization and submission of laboratory work

## Laboratory Work

### Lab 03 — Basic psql Commands
**[Open Lab 03](Lab-03-PSQL-Basics)**

- Practiced connecting to PostgreSQL and navigating databases and tables with `psql` commands.
- Created and inspected a simple `students` table; explored table structure and query output.
- **Evidence:** terminal screenshots showing commands and results.

### Lab 04 — First SQL Query
**[Open Lab 04](Lab-04-First-SQL-Query)**

- Practiced basic SQL query structure and retrieving records using `SELECT`.
- Worked with selected columns and complete table output.
- **Evidence:** SQL execution screenshots.

### Lab 05 — Databases Overview
**[Open Lab 05](Lab-05-Databases)**

- Practiced database-level operations and switching between databases in `psql`.
- Worked with SQL commands and a file-based SQL workflow.
- **Evidence:** database and terminal screenshots.

### Lab 06 — Tables, Data Types and Constraints
**[Open Lab 06](Lab-06-Tables-DT-Constraints)**

- Designed a small **coffee shop** database with `products` and `orders` tables.
- Practiced PostgreSQL data types and constraints, including `PRIMARY KEY`, `FOREIGN KEY`, `NOT NULL`, `UNIQUE`, `CHECK`, and default values.
- Inserted sample products and orders, then checked table structures and data.
- **Evidence:** table definitions and query results.

### Lab 07 — Primary Keys
**[Open Lab 07](Lab-07-PrimaryKeys)**

- Compared column-level, table-level, named, and composite primary keys.
- Explored automatically generated identifiers using `SERIAL` and `IDENTITY`.
- **Evidence:** SQL and `psql` table-structure screenshots.

### Lab 08 — Foreign Keys and Relationships
**[Open Lab 08](Lab-08-ForeignKeys)**

- Defined foreign keys inline, at table level, and through `ALTER TABLE`.
- Examined referential integrity and `ON DELETE` / `ON UPDATE` behaviors.
- Practiced one-to-one, one-to-many, and many-to-many relationships, including junction tables.
- **Evidence:** relationship and constraint demonstrations.

### Lab 09 — Database Design Basics
**[Open Lab 09](Lab-09-DB-design-basics)**

- Designed a university database with `departments`, `students`, `courses`, and `enrollments`.
- Studied entity–relationship modeling and normalization principles: **1NF, 2NF, and 3NF**.
- Implemented primary keys, foreign keys, and a composite key for course enrollments.
- **Evidence:** database-design work, table structures, and diagrams where provided.

### Lab 10 — Viewing Database and Table Structure
**[Open Lab 10](Lab-10-ViewingDB-%26-TableStructure)**

- Inspected database objects and constraints with commands such as `\dt` and `\d`.
- Explored the database structure and ER-diagram tools in pgAdmin.
- **Evidence:** schema inspection and database visualization screenshots.

### Lab 11 — Basic Data Operations
**[Open Lab 11](Lab-11-Basic-Data-Operations)**

- Practiced `INSERT`, `UPDATE`, and `DELETE`, including operations affecting multiple rows.
- Used filtering conditions to update and delete specific records safely.
- **Evidence:** before-and-after table results.

### Lab 12 — Querying Data
**[Open Lab 12](Lab-12-Querying-Data)**

- Worked with `SELECT`, `WHERE`, `BETWEEN`, `LIKE`, `ILIKE`, and regular-expression matching.
- Practiced `IN`, `EXISTS`, `CASE`, subqueries, and common table expressions (`WITH`).
- **Evidence:** query screenshots and returned results.

### Lab 13 — Aggregate Functions
**[Open Lab 13](Lab-13-Aggregate-Functions)**

- Analyzed the **coffee shop** data using `COUNT`, `SUM`, `AVG`, `MIN`, and `MAX`.
- Practiced `GROUP BY`, multi-column grouping, `WHERE` versus `HAVING`, and conditional aggregation.
- Explored `STRING_AGG`, `ARRAY_AGG`, statistical aggregates, and window-based calculations.
- **Evidence:** analytical query results using `products` and `orders`.

### Lab 14 — Joining Tables
**[Open Lab 14](Lab-14-Joining-Tables)**

- Practiced `INNER`, `LEFT`, `RIGHT`, `FULL OUTER`, and `CROSS JOIN`.
- Used multi-table joins, self joins, join conditions, and relationships between tables.
- Worked with the coffee shop and university databases to compare join behavior.
- **Evidence:** join queries and their outputs.

### Lab 15 — Advanced Querying
**[Open Lab 15](Lab-15-Advanced-Querying)**

- Practiced scalar subqueries, common table expressions, and recursive CTEs for employee hierarchies.
- Used `UNION`, `UNION ALL`, `INTERSECT`, and `EXCEPT` to combine result sets.
- Explored window functions, `PARTITION BY`, ranking, pivot/unpivot techniques, and `FILTER`.
- Examined query plans with `EXPLAIN` and `EXPLAIN ANALYZE`.
- **Evidence:** advanced queries and execution results.

### Lab 16 — Transactions and ACID Properties
**[Open Lab 16](Lab-16-Transactions-%26-ACID)**

- Created a practice `accounts` table to demonstrate transactions.
- Used `BEGIN`, `COMMIT`, `ROLLBACK`, `SAVEPOINT`, and transaction isolation settings.
- Examined **Atomicity, Consistency, Isolation, and Durability** through practical examples.
- **Evidence:** account-balance checks, transaction results, and isolation demonstrations.

### Lab 17 — Data Import/Export and Backup
**[Open Lab 17](Lab-17-Data-Export-Import)**

- Exported coffee shop product data to CSV and imported it into a separate test table using `\copy`.
- Created a logical database backup using `pg_dump` and inspected it with `pg_restore`.
- Restored the backup into a separate database (`coffee_shop_restore_lab17`) and verified the restored tables and row counts.
- Studied full/incremental backups, WAL, point-in-time recovery, and migration concepts; server-level recovery was not performed.
- **Evidence:** export/import results, CSV data, backup verification, and restoration screenshots. A `.dump` archive may also be included.

## How to Read the Lab Evidence

Each `Lab-XX-...` folder is organized around its assignment. Screenshot files may use sequential names such as `01.png`, `02.png`, and `03.png`; these numbers indicate the order in which evidence was captured. Some files may instead have descriptive names.

The screenshots show the actual terminal or pgAdmin commands, table structures, and outputs. For practical data-transfer work, CSV and PostgreSQL backup files may be included alongside the screenshots.

> **Note:** PostgreSQL databases themselves are stored locally. Screenshots and exported files document the work; they do not necessarily reproduce every database automatically.

## Learning Outcomes

This portfolio reflects practice with relational modeling, SQL querying, referential integrity, aggregation, joins, advanced querying, transaction management, and backup/restore workflows.

---

**Course:** Databases · COM-424.1  
**Institution:** American University of Central Asia  
**Semester:** Fall 2026
