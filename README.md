# PostgreSQL



### 🟢 **Beginner Level**

#### 1. Introduction to Databases & PostgreSQL

* What is a DBMS and RDBMS
* PostgreSQL vs MySQL vs other RDBMS
* Installing PostgreSQL (Linux, Mac, Windows)
* PostgreSQL tools: `psql`, pgAdmin

#### 2. SQL Basics

* Data Types in PostgreSQL
* `CREATE`, `DROP`, `ALTER` tables
* `INSERT`, `UPDATE`, `DELETE`
* `SELECT` statements
* Filtering with `WHERE`, `BETWEEN`, `IN`, `LIKE`
* Sorting with `ORDER BY`
* Limiting with `LIMIT` and `OFFSET`

#### 3. Constraints

* `PRIMARY KEY`, `FOREIGN KEY`
* `NOT NULL`, `UNIQUE`, `CHECK`, `DEFAULT`

#### 4. Joins and Relationships

* `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL JOIN`
* Self Join
* Subqueries

#### 5. Aggregate Functions

* `COUNT`, `SUM`, `AVG`, `MAX`, `MIN`
* `GROUP BY`, `HAVING`

---

### 🟡 **Intermediate Level**

#### 6. Advanced SQL Features

* `CASE`, `COALESCE`, `NULLIF`
* Aliases (`AS`)
* Views (`CREATE VIEW`, `UPDATE` via view)

#### 7. Indexing & Performance

* Creating Indexes
* Unique Indexes
* `EXPLAIN` & Query Optimization

#### 8. Transactions and Concurrency

* `BEGIN`, `COMMIT`, `ROLLBACK`
* Isolation Levels
* ACID properties
* Locks (`FOR UPDATE`, `FOR SHARE`)

#### 9. Functions and Stored Procedures

* User-defined functions (SQL/PLpgSQL)
* Parameters and returns
* Error handling

#### 10. Triggers

* `BEFORE`, `AFTER`, `INSTEAD OF`
* Trigger functions

#### 11. Data Import/Export

* `COPY` command
* `pg_dump`, `pg_restore`

---

### 🔴 **Advanced Level**

#### 12. Advanced Data Types

* Arrays
* JSON/JSONB (querying, indexing)
* HSTORE
* Enums and Composite types

#### 13. Window Functions

* `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`
* `LEAD()`, `LAG()`
* `PARTITION BY`, `FRAME`

#### 14. CTEs and Recursive Queries

* `WITH` clause
* Recursive CTEs

#### 15. Full Text Search

* `tsvector`, `tsquery`
* `to_tsvector()`, `plainto_tsquery()`
* Ranking results

#### 16. Extensions & Tooling

* Using Extensions like `uuid-ossp`, `pgcrypto`, `postgis`
* Managing roles and permissions
* Logical replication & streaming replication
* Partitioning strategies

#### 17. PostgreSQL with Applications

* Connecting via Python (psycopg2), Node.js (pg), etc.
* ORMs (Sequelize, SQLAlchemy)
* Using PostgreSQL in Docker
* PostgreSQL + FastAPI (or other backend frameworks)


Here's a clear breakdown for the **first lesson** in a PostgreSQL course titled **"Introduction to Databases & PostgreSQL"**:

---

### 1️⃣ **What is a DBMS and RDBMS?**

**DBMS (Database Management System):**

* Software that manages databases (e.g., file-based DBs).
* Examples: MongoDB, Redis, Firebase, etc.

**RDBMS (Relational DBMS):**

* DBMS that uses **tables with rows & columns** and supports SQL.
* Maintains **relationships** between tables using keys.
* Ensures **ACID** properties (Atomicity, Consistency, Isolation, Durability).
* Examples: PostgreSQL, MySQL, Oracle, SQL Server.

---

### 2️⃣ **PostgreSQL vs MySQL vs Other RDBMS**

| Feature             | **PostgreSQL**                     | **MySQL**                     | **SQLite/Oracle/SQL Server** |
| ------------------- | ---------------------------------- | ----------------------------- | ---------------------------- |
| Type                | Object-relational DB               | Relational DB                 | Varies                       |
| Open Source         | ✅ Yes                              | ✅ Yes                         | SQLite – Yes; others – ❌     |
| SQL Compliance      | ✅ Highly compliant                 | ❌ Less compliant              | Oracle is highly compliant   |
| Performance         | Excellent for complex queries      | Fast for read-heavy workloads | Varies                       |
| JSON Support        | ✅ Best-in-class                    | ✅ Good                        | Oracle supports JSON         |
| Concurrency Control | ✅ MVCC (Multiversion)              | ❌ Lock-based                  | Varies                       |
| Extensibility       | ✅ Highly extensible (custom types) | ❌ Limited                     | SQL Server offers plugins    |

✅ Use **PostgreSQL** for analytics, data integrity, and modern web apps.

---

### 3️⃣ **Installing PostgreSQL**

#### 📦 **Linux (Debian/Ubuntu)**:

```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
```

#### 🍏 **macOS (using Homebrew)**:

```bash
brew update
brew install postgresql
brew services start postgresql
```

#### 🪟 **Windows**:

* Download the installer from: [https://www.postgresql.org/download/windows/](https://www.postgresql.org/download/windows/)
* Use the graphical setup wizard.

---

### 4️⃣ **PostgreSQL Tools**

* **`psql` (CLI Tool)**

  * Access and run SQL commands in terminal.
  * Common commands:

    ```bash
    psql -U postgres
    \l   -- list databases
    \c dbname -- connect to DB
    \dt  -- list tables
    ```

* **`pgAdmin` (GUI Tool)**

  * Graphical user interface to manage DB, run queries, design schema, etc.
  * Great for beginners who prefer UI over CLI.

Here's **Lesson 2: SQL Basics** for your PostgreSQL course — concise and structured:

---

### 2️⃣ **SQL Basics in PostgreSQL**

---

### 📌 **1. Data Types in PostgreSQL**

| Category      | Examples                                                                        |
| ------------- | ------------------------------------------------------------------------------- |
| **Numeric**   | `INTEGER`, `BIGINT`, `SERIAL`, `DECIMAL`, `NUMERIC`, `REAL`, `DOUBLE PRECISION` |
| **Text**      | `CHAR(n)`, `VARCHAR(n)`, `TEXT`                                                 |
| **Boolean**   | `BOOLEAN` (`TRUE`, `FALSE`, `NULL`)                                             |
| **Date/Time** | `DATE`, `TIME`, `TIMESTAMP`, `INTERVAL`                                         |
| **UUID**      | Universally unique identifiers                                                  |
| **JSON**      | `JSON`, `JSONB` (binary JSON)                                                   |

---

### 📌 **2. Table Operations**

```sql
-- CREATE table
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  age INT,
  email TEXT
);

-- DROP table
DROP TABLE users;

-- ALTER table
ALTER TABLE users ADD COLUMN created_at TIMESTAMP;
ALTER TABLE users RENAME COLUMN name TO full_name;
```

---

### 📌 **3. Data Manipulation**

```sql
-- INSERT
INSERT INTO users (name, age, email) VALUES ('Alice', 30, 'alice@email.com');

-- UPDATE
UPDATE users SET age = 31 WHERE name = 'Alice';

-- DELETE
DELETE FROM users WHERE name = 'Alice';
```

---

### 📌 **4. SELECT Queries**

```sql
-- Basic
SELECT * FROM users;
SELECT name, age FROM users;

-- WHERE filters
SELECT * FROM users WHERE age > 25;
SELECT * FROM users WHERE name = 'Bob';

-- BETWEEN
SELECT * FROM users WHERE age BETWEEN 20 AND 30;

-- IN
SELECT * FROM users WHERE name IN ('Alice', 'Bob');

-- LIKE
SELECT * FROM users WHERE email LIKE '%@gmail.com';
```

---

### 📌 **5. Sorting & Pagination**

```sql
-- ORDER BY
SELECT * FROM users ORDER BY age DESC;

-- LIMIT & OFFSET
SELECT * FROM users ORDER BY id LIMIT 5 OFFSET 10;
```

---

Here’s a clear and structured breakdown for:

---

### ✅ **Lesson 3: Constraints**

| Constraint    | Description                               | Example                              |
| ------------- | ----------------------------------------- | ------------------------------------ |
| `PRIMARY KEY` | Uniquely identifies each row              | `id SERIAL PRIMARY KEY`              |
| `FOREIGN KEY` | Links to a `PRIMARY KEY` in another table | `user_id INT REFERENCES users(id)`   |
| `NOT NULL`    | Prevents `NULL` values in a column        | `name TEXT NOT NULL`                 |
| `UNIQUE`      | Ensures all values are different          | `email TEXT UNIQUE`                  |
| `CHECK`       | Validates custom rules                    | `age INT CHECK (age >= 18)`          |
| `DEFAULT`     | Sets a default value                      | `created_at TIMESTAMP DEFAULT NOW()` |

```sql
CREATE TABLE orders (
  id SERIAL PRIMARY KEY,
  user_id INT REFERENCES users(id),
  amount DECIMAL NOT NULL CHECK (amount > 0),
  status TEXT DEFAULT 'pending'
);
```

---

### ✅ **Lesson 4: Joins and Relationships**

#### 🔗 `INNER JOIN`

Returns only matching rows in both tables.

```sql
SELECT users.name, orders.amount
FROM users
INNER JOIN orders ON users.id = orders.user_id;
```

#### 🔗 `LEFT JOIN`

Returns all rows from left table, matched or not.

```sql
SELECT users.name, orders.amount
FROM users
LEFT JOIN orders ON users.id = orders.user_id;
```

#### 🔗 `RIGHT JOIN`

Returns all rows from right table, matched or not.

```sql
SELECT users.name, orders.amount
FROM users
RIGHT JOIN orders ON users.id = orders.user_id;
```

#### 🔗 `FULL JOIN`

Returns all rows when there is a match in one of the tables.

```sql
SELECT users.name, orders.amount
FROM users
FULL JOIN orders ON users.id = orders.user_id;
```

---

### 🔁 **Self Join**

Joining a table to itself.

```sql
SELECT a.name AS manager, b.name AS employee
FROM employees a
JOIN employees b ON a.id = b.manager_id;
```

---

### 🔍 **Subqueries**

Nested queries inside another query.

```sql
-- Get users who placed orders
SELECT * FROM users
WHERE id IN (SELECT user_id FROM orders);

-- Get users with highest order
SELECT * FROM users
WHERE id = (SELECT user_id FROM orders ORDER BY amount DESC LIMIT 1);
```

---

Here’s a concise and clear breakdown for:

---

### ✅ **Lesson 5: Aggregate Functions & Grouping**

---

### 📊 **Aggregate Functions**

| Function  | Description               | Example                           |
| --------- | ------------------------- | --------------------------------- |
| `COUNT()` | Total number of rows      | `SELECT COUNT(*) FROM users;`     |
| `SUM()`   | Sum of values in a column | `SELECT SUM(amount) FROM orders;` |
| `AVG()`   | Average value             | `SELECT AVG(age) FROM users;`     |
| `MAX()`   | Maximum value             | `SELECT MAX(amount) FROM orders;` |
| `MIN()`   | Minimum value             | `SELECT MIN(age) FROM users;`     |

---

### 📁 **GROUP BY**

Used to **group rows** based on a column and apply aggregate functions.

```sql
-- Total orders per user
SELECT user_id, COUNT(*) AS total_orders
FROM orders
GROUP BY user_id;
```

```sql
-- Average order amount by status
SELECT status, AVG(amount) AS avg_amount
FROM orders
GROUP BY status;
```

---

### 📌 **HAVING**

Used to **filter groups** after `GROUP BY`.

```sql
-- Users with more than 2 orders
SELECT user_id, COUNT(*) AS order_count
FROM orders
GROUP BY user_id
HAVING COUNT(*) > 2;
```

```sql
-- Order statuses where total amount > 500
SELECT status, SUM(amount) AS total_amount
FROM orders
GROUP BY status
HAVING SUM(amount) > 500;
```

Here’s a well-structured breakdown for:

---

### ✅ **Lesson 6: Advanced SQL Features**

---

### 🔁 **CASE Expression**

Conditional logic in queries.

```sql
SELECT name,
  CASE 
    WHEN age >= 18 THEN 'Adult'
    ELSE 'Minor'
  END AS category
FROM users;
```

---

### 🔄 **COALESCE**

Returns the first non-null value.

```sql
SELECT name, COALESCE(email, 'no-email@example.com') FROM users;
```

---

### 🚫 **NULLIF**

Returns `NULL` if two values are equal.

```sql
SELECT NULLIF(10, 10); -- Returns NULL
```

---

### ✍️ **Aliases (AS)**

Renames columns or tables for clarity.

```sql
SELECT name AS full_name FROM users;
SELECT u.name FROM users AS u;
```

---

### 👁 **Views**

Virtual tables for reusability.

```sql
-- Create View
CREATE VIEW adult_users AS
SELECT * FROM users WHERE age >= 18;

-- Use View
SELECT * FROM adult_users;

-- Update through View (if allowed)
UPDATE adult_users SET name = 'Updated Name' WHERE id = 1;
```

---

### ✅ **Lesson 7: Indexing & Performance**

---

### 🚀 **Creating Indexes**

Speeds up `SELECT` and `WHERE` queries.

```sql
CREATE INDEX idx_users_email ON users(email);
```

---

### 🔐 **Unique Indexes**

Ensure uniqueness + speed.

```sql
CREATE UNIQUE INDEX unique_email_idx ON users(email);
```

---

### 🧠 **EXPLAIN**

Analyzes query execution plan.

```sql
EXPLAIN SELECT * FROM users WHERE email = 'test@example.com';
```

Returns cost, index usage, scan type, etc.

Here’s a clear and complete tutorial outline for:

---

## ✅ **Lesson 8: Transactions and Concurrency**

---

### 🔁 **BEGIN, COMMIT, ROLLBACK**

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

* `ROLLBACK;` undoes changes if something fails.

---

### 🔒 **ACID Properties**

* **A**tomicity – All or nothing
* **C**onsistency – DB moves from one valid state to another
* **I**solation – Transactions are independent
* **D**urability – Changes are permanent once committed

---

### 🔐 **Isolation Levels**

```sql
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
```

* `READ COMMITTED` (default)
* `REPEATABLE READ`
* `SERIALIZABLE` (most strict)

---

### 🔏 **Locks**

```sql
SELECT * FROM accounts WHERE id = 1 FOR UPDATE;
SELECT * FROM inventory WHERE id = 5 FOR SHARE;
```

* Prevents conflicts in concurrent access.

---

## ✅ **Lesson 9: Functions and Stored Procedures**

---

### 🛠 **User-Defined Function (SQL/PLpgSQL)**

```sql
CREATE FUNCTION get_discount(price NUMERIC)
RETURNS NUMERIC AS $$
BEGIN
  RETURN price * 0.9;
END;
$$ LANGUAGE plpgsql;
```

```sql
SELECT get_discount(100); -- Output: 90
```

---

### ⚙ **Parameters, RETURNS, and Errors**

* Can return `SCALAR`, `TABLE`, `VOID`
* Error handling with `EXCEPTION`

```sql
BEGIN
  -- logic
EXCEPTION
  WHEN OTHERS THEN RAISE NOTICE 'Error!';
END;
```

---

## ✅ **Lesson 10: Triggers**

---

### 🔁 **Types**

* `BEFORE` – Before operation
* `AFTER` – After operation
* `INSTEAD OF` – For views

---

### 🧠 **Trigger Function + Trigger**

```sql
CREATE FUNCTION log_update() RETURNS trigger AS $$
BEGIN
  INSERT INTO audit_log(table_name, operation, changed_at)
  VALUES (TG_TABLE_NAME, TG_OP, NOW());
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER after_update_trigger
AFTER UPDATE ON users
FOR EACH ROW EXECUTE FUNCTION log_update();
```

---

## ✅ **Lesson 11: Data Import/Export**

---

### 📥 **Import Using COPY**

```sql
COPY users(name, age) FROM '/path/users.csv' DELIMITER ',' CSV HEADER;
```

---

### 📤 **Export Using COPY**

```sql
COPY users TO '/path/users_export.csv' DELIMITER ',' CSV HEADER;
```

---

### 📦 **Backup & Restore**

```bash
-- Backup
pg_dump mydb > backup.sql

-- Restore
psql newdb < backup.sql

-- Compressed
pg_dump -Fc mydb > backup.dump
pg_restore -d newdb backup.dump
```

Here’s a complete **Advanced PostgreSQL Tutorial (Lessons 12–17)**—structured for clarity and practical use:

---

## 🔴 **Lesson 12: Advanced Data Types**

---

### 📦 **Arrays**

```sql
CREATE TABLE users (id SERIAL, tags TEXT[]);
INSERT INTO users(tags) VALUES (ARRAY['dev', 'admin']);
SELECT * FROM users WHERE 'admin' = ANY(tags);
```

---

### 🧩 **JSON / JSONB**

```sql
-- Create table with JSONB
CREATE TABLE products (id SERIAL, data JSONB);

-- Insert
INSERT INTO products(data) VALUES ('{"name": "laptop", "price": 999}');

-- Query
SELECT data->>'name' FROM products;
SELECT * FROM products WHERE data @> '{"price": 999}';

-- Index
CREATE INDEX idx_json_price ON products USING GIN (data jsonb_path_ops);
```

---

### 🏷️ **HSTORE**

```sql
CREATE EXTENSION IF NOT EXISTS hstore;

CREATE TABLE settings (id SERIAL, prefs HSTORE);
INSERT INTO settings(prefs) VALUES ('theme => dark, lang => en');
SELECT prefs -> 'theme' FROM settings;
```

---

### 🎭 **ENUM & Composite Types**

```sql
CREATE TYPE mood AS ENUM ('happy', 'sad', 'neutral');
CREATE TABLE people (id SERIAL, state mood);

-- Composite type
CREATE TYPE full_name AS (first TEXT, last TEXT);
CREATE TABLE staff (id SERIAL, name full_name);
```

---

## 🔍 **Lesson 13: Window Functions**

---

### 🪟 **Window Basics**

```sql
SELECT name, salary,
  ROW_NUMBER() OVER (ORDER BY salary DESC),
  RANK() OVER (ORDER BY salary DESC),
  DENSE_RANK() OVER (ORDER BY salary DESC)
FROM employees;
```

---

### 🔁 **LEAD / LAG**

```sql
SELECT name, salary,
  LEAD(salary) OVER (ORDER BY salary),
  LAG(salary) OVER (ORDER BY salary)
FROM employees;
```

---

### 📤 **PARTITION & FRAME**

```sql
SELECT department, name, salary,
  RANK() OVER (PARTITION BY department ORDER BY salary DESC)
FROM employees;
```

---

## 🔁 **Lesson 14: CTEs & Recursive Queries**

---

### 🧱 **WITH clause (CTE)**

```sql
WITH active_users AS (
  SELECT * FROM users WHERE active = true
)
SELECT * FROM active_users WHERE age > 30;
```

---

### 🌲 **Recursive CTE**

```sql
WITH RECURSIVE hierarchy AS (
  SELECT id, manager_id, name FROM employees WHERE manager_id IS NULL
  UNION ALL
  SELECT e.id, e.manager_id, e.name
  FROM employees e
  JOIN hierarchy h ON e.manager_id = h.id
)
SELECT * FROM hierarchy;
```

---

## 🔎 **Lesson 15: Full Text Search**

---

### 📄 **tsvector, tsquery**

```sql
-- Setup
ALTER TABLE articles ADD COLUMN document tsvector;
UPDATE articles SET document = to_tsvector(title || ' ' || content);
CREATE INDEX idx_docs ON articles USING GIN (document);

-- Query
SELECT * FROM articles WHERE document @@ plainto_tsquery('open source');
```

---

### 📈 **Ranking**

```sql
SELECT title, ts_rank(document, plainto_tsquery('open source')) AS rank
FROM articles
ORDER BY rank DESC;
```

---

## 🔧 **Lesson 16: Extensions & Tooling**

---

### 🧩 **Popular Extensions**

```sql
-- UUID generation
CREATE EXTENSION "uuid-ossp";
SELECT uuid_generate_v4();

-- Encryption
CREATE EXTENSION pgcrypto;
SELECT crypt('secret', gen_salt('bf'));

-- GIS
CREATE EXTENSION postgis;
```

---

### 👥 **Roles and Permissions**

```sql
CREATE ROLE readonly LOGIN PASSWORD 'pass';
GRANT CONNECT ON DATABASE mydb TO readonly;
GRANT USAGE ON SCHEMA public TO readonly;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO readonly;
```

---

### 🔁 **Replication**

* **Logical replication**: publish/subscribe to specific tables
* **Streaming replication**: full WAL-level sync

---

### 📂 **Partitioning**

```sql
CREATE TABLE orders (
  id SERIAL,
  created_at DATE
) PARTITION BY RANGE (created_at);

CREATE TABLE orders_2024 PARTITION OF orders FOR VALUES FROM ('2024-01-01') TO ('2025-01-01');
```

---

## 🔌 **Lesson 17: PostgreSQL with Applications**

---

### 🐍 **Python (psycopg2)**

```python
import psycopg2
conn = psycopg2.connect("dbname=db user=postgres password=123")
cur = conn.cursor()
cur.execute("SELECT * FROM users")
print(cur.fetchall())
```

---

### 🟢 **Node.js (pg)**

```js
const { Client } = require('pg');
const client = new Client();
await client.connect();
const res = await client.query('SELECT * FROM users');
console.log(res.rows);
```

---

### ⚙️ **ORMs**

* **Python**: SQLAlchemy
* **Node.js**: Sequelize, Prisma

---

### 🐳 **PostgreSQL in Docker**

```bash
docker run --name pg -e POSTGRES_PASSWORD=pass -p 5432:5432 -d postgres
```

---

### ⚡ **PostgreSQL + FastAPI**

```python
from fastapi import FastAPI
import psycopg2

app = FastAPI()
conn = psycopg2.connect("dbname=mydb user=postgres password=pass")

@app.get("/users")
def get_users():
    cur = conn.cursor()
    cur.execute("SELECT * FROM users")
    return cur.fetchall()
```






