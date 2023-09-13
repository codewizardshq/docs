# SQL Language

SQL (Structured Query Language) is a language used to interact with databases. We use SQL in the following courses at CodeWizardsHQ:

| Middle School       | High School                      |
| ------------------- | -------------------------------- |
| Intro to Databases  | APIs and Databases               |
| Mastering APIs      | Professional Web App Development |
| Mastering Databases | Capstone 2                       |
| Capstone 3          | Mastering MVC Framework          |
|                     | Object Relational Mapping        |
|                     | Capstone 3                       |

In this section of our documentation, you'll find references to most of the core SQL language features that we use in our CodeWizardsHQ courses. All of our courses interact with databases using Python + SQL, so we'll show the core SQL syntax first and then give a working example in Python.

You'll also find many _Further reading_ sections, which pull from these excellent SQL/Python resources:

-   [SQLBolt](https://sqlbolt.com/lesson/introduction)
-   [SQLite Tutorial](https://www.sqlitetutorial.net/)
-   [Python.org Documentation](https://www.python.org/doc/)
-   [Mode SQL Tutorial](https://mode.com/sql-tutorial/)

<hr>

## What Is A Relational Database?

In a relational database, you structure your data in tables made up of rows and columns, kind of like an Excel spreadsheet. You can combine data from multiple tables using `JOIN`s or just pull data from a single table.

For example, consider the two tables below:

_users table_

| user_id | username | password   |
| ------- | -------- | ---------- |
| 1       | djs      | mypa$$word |
| 2       | django   | w0ff       |
| 3       | alecg    | c0de       |

_teachers table_

| teacher_id | user_id | username | is_admin |
| ---------- | ------- | -------- | -------- |
| 1          | 1       | djs      | 1        |
| 2          | 3       | alecg    | 0        |

We could get the username and password of all users that are teachers and admins like this:

```sql
SELECT
    users.username, users.password
FROM
    users
JOIN
    teachers
USING
    (user_id)
WHERE
    teachers.is_admin = 1;
┌──────────┬────────────┐
│ username │  password  │
├──────────┼────────────┤
│ djs      │ mypa$$word │
└──────────┴────────────┘
```

There are many different relational database implementations (MySQL, Postgres, etc.) but we use SQLite at CodeWizardsHQ because it is easy to work with and supports most of the common SQL features.

## Why Do We Need SQL?

When working with a database, you need a way to talk to the database and get data into/out of it. SQL is the language we use to do this in a SQLite database. SQL allows you to express relationships in a database in a structured way.

## Why Do We Use Python And SQL Together?

Although you can use raw SQL commands to talk to a SQL database, we use Python at CodeWizardsHQ because often you'll interact with databases this way in the real world. Think about apps you've used that store data about you between visits. That's using a database and a programming language (like Python) to interact with the database!

The SQL portions of a Python DB query will be a Python `str`. Consider this `INSERT` statement in raw SQL:

```text
INSERT INTO users (username, password) VALUES ("djs", "mypa$$word");
```

To run that from Python, we would do this:

```python
import sqlite3

con = sqlite3.connect("users-database.db")
sql = con.cursor()

query = """
    INSERT INTO users (username, password) VALUES ("djs", "mypa$$word");
"""

sql.execute(query)
con.commit()
```

The important thing to remember is that the `query` is just a `str` that you pass to `sql.execute()`. If you make a change to a table in the database (as we did above) then you use the `con.commit()` method to save the change (although in some CWHQ courses you merely view the results without changing the database). The semi-colon (`;`) isn't required when using a query from Python, but we'll keep it for consistency between the raw SQL examples.

### Bounded Parameters

When accepting user input in a Python program that modifies a SQL database, you'll use `?` as placeholders for any user-entered data and then pass the data to `sql.execute()` as a `list` like this:

```python
import sqlite3

con = sqlite3.connect("users-database.db")
sql = con.cursor()

username = input("Enter your username: ")
password = input("Enter your password: ")

# Use `?` for any user-entered data
query = """
    INSERT INTO users (username, password) VALUES (?, ?);
"""

# The `username` and `password` are bound to the `?` in the `query`
sql.execute(query, [username, password])
con.commit()
```

**Further Reading**

-   [Python Documentation - sqlite3](https://docs.python.org/3/library/sqlite3.html)

## Aggregate Functions

Just like programming languages such as Python and JavaScript, SQL has functions to perform common tasks on result set called _Aggregate Functions_. The example below shows the different _Aggregate Functions_ we use in CWHQ courses.

**Raw SQL**

```sql
SELECT * FROM products;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

-- Get the average price of all products
SELECT AVG(product_price) AS average_product_price FROM products;
┌───────────────────────┐
│ average_product_price │
├───────────────────────┤
│ 800.7525              │
└───────────────────────┘

-- Count the number of products
SELECT COUNT(*) AS total_products FROM products;
┌────────────────┐
│ total_products │
├────────────────┤
│ 8              │
└────────────────┘

-- Get the most expensive product
SELECT product_name || " $" || MAX(product_price) AS most_expensive_product
FROM products;
┌────────────────────────┐
│ most_expensive_product │
├────────────────────────┤
│ MacBook Pro 16 $2100.5 │
└────────────────────────┘

-- Get the least expensive product
SELECT product_name || " $" || MIN(product_price) AS least_expensive_product
FROM products;
┌─────────────────────────┐
│ least_expensive_product │
├─────────────────────────┤
│ Logitech M1 $34.99      │
└─────────────────────────┘

-- Get the total cost of all products combined
SELECT SUM(product_price) AS total_cost_all_products FROM products;
┌─────────────────────────┐
│ total_cost_all_products │
├─────────────────────────┤
│ 6406.02                 │
└─────────────────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("products-database.db")
sql = con.cursor()

def execute_query_and_display_rows(query):
    result = sql.execute(query)
    rows = result.fetchall()

    for row in rows:
        print(row)


query = """
    SELECT * FROM products;
"""

print("All products:")
execute_query_and_display_rows(query)

query = """
    SELECT AVG(product_price) AS average_product_price FROM products;
"""

print("\nAverage cost of all products:")
execute_query_and_display_rows(query)

query = """
    SELECT COUNT(*) AS total_products FROM products;
"""

print("\nTotal number of products:")
execute_query_and_display_rows(query)

query = """
    SELECT product_name || " $" || MAX(product_price) AS most_expensive_product
    FROM products;
"""

print("\nMost expensive product:")
execute_query_and_display_rows(query)

query = """
    SELECT product_name || " $" || MIN(product_price) AS least_expensive_product
    FROM products;
"""

print("\nLeast expensive product:")
execute_query_and_display_rows(query)

query = """
    SELECT SUM(product_price) AS total_cost_all_products FROM products;
"""

print("\nTotal cost of all products:")
execute_query_and_display_rows(query)
```

**Output**

```text
All products:
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(6, 'MacBook Pro 16', 2100.5, 'Computers')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')

Average cost of all products:
(800.7524999999999,)

Total number of products:
(8,)

Most expensive product:
('MacBook Pro 16 $2100.5',)

Least expensive product:
('Logitech M1 $34.99',)

Total cost of all products:
(6406.0199999999995,)
```

**Further Reading**

-   [SQLBolt - Queries with aggregates - Pt. 1](https://sqlbolt.com/lesson/select_queries_with_aggregates)
-   [SQLite Tutorial - SQLite Aggregate Functions](https://www.sqlitetutorial.net/sqlite-aggregate-functions/)

## Arithmetic Operators

When writing queries, you may find that the table does not have a column for a certain value but has columns which could be used to calculate it. SQL supports arithmetic operations in selections and `WHERE` clauses. In a selection, this will add a column to the result which calculates the expression for each result.

**Raw SQL**

```sql
SELECT name, price, price * 0.07 FROM products;

┌───────────┬──────────┬─────────────────┐
│ name      │ price    │  price * 0.07   │
├───────────┼──────────┼─────────────────┤
│ cookies   │ 10.00    │ 10.70           │
│ ice cream │ 5.00     │ 5.35            │
│ donuts    │ 7.00     │ 7.49            │
└───────────┴──────────┴─────────────────┘

```

You can alias the calculated column using `AS` for a clearer output.

**Raw SQL**
```sql
SELECT name, price, price * 0.07 AS sales_tax FROM products;

┌───────────┬──────────┬─────────────────┐
│ name      │ price    │  sales_tax      │
├───────────┼──────────┼─────────────────┤
│ cookies   │ 10.00    │ 0.70            │
│ ice cream │ 5.00     │ 0.35            │
│ donuts    │ 7.00     │ 0.49            │
└───────────┴──────────┴─────────────────┘

```

The operations are also supported in `WHERE` clauses.


```sql

-- select all rows where tax is greater than 10 dollars
SELECT * FROM products WHERE price * 0.07 > 10.00
```

## Subqueries

A subquery, also known as a nested query or inner query, is a query that is embedded within another SQL query. Subqueries allow you to retrieve data from one or more tables and use that result within another query. They are an essential feature of SQL for performing complex queries and data manipulation.

There are two primary types of subqueries:

1. **Scalar Subquery**:
A scalar subquery is a subquery that returns a single value. This type of subquery is typically used within a `SELECT` or `WHERE` clause to compare a single value with the result of the subquery.
```sql
-- Find the average salary of employees
SELECT AVG(salary) FROM employees;
┌────────────────┐
| AVG(salary)    │ 
├────────────────┤
│ 85000          |
└────────────────┘

-- Use the above query in a subquery
SELECT name, salary FROM employees 
    WHERE salary > (SELECT AVG(salary) FROM employees);
┌──────────┬─────────────┐
│ name     │ salary      │ 
├──────────┼─────────────┤
│ Alice    │ 100000      │
│ Bob      │ 90000       │
│ Charlie  │ 85001       │
└──────────┴─────────────┘

```
The subquery `SELECT AVG(salary) FROM employees` is a single, or scalar, value. When used in the `WHERE` clause, the full query finds all employees whose salary is greater than the average salary.

2. **Table Subquery**:
A table subquery, also known as a derived table or inline view, returns a result set (a table) that can be used in a `FROM` clause or joined with other tables in the main query.
```sql

-- Count the number of courses by the programming language they use
SELECT language, COUNT(*) as num_courses 
    FROM programming_courses GROUP BY language;
┌──────────┬─────────────┐
│ language │ num_courses │ 
├──────────┼─────────────┤
│ Python   │ 10          │
│ HTML/CSS │ 6           │
│ SQL      │ 3           │
└──────────┴─────────────┘


-- Using the above query in a subquery, we can use the MAX() function on the count column
SELECT language, MAX(num_courses) FROM 
    (SELECT language, COUNT(*) as num_courses 
        FROM programming_courses GROUP BY language
    ); 
┌──────────┬──────────────────┐
│ language │ MAX(num_courses) │ 
├──────────┼──────────────────┤
│ Python   │ 10               │
└──────────┴──────────────────┘
```

**Further Reading**


-   [SQL Subqueries - w3resource](https://www.w3resource.com/sql/subqueries/understanding-sql-subqueries.php)
-   [SQL - Sub Queries - TutorialsPoint](https://www.tutorialspoint.com/sql/sql-sub-queries.htm)


## ALTER TABLE

After creating a table, you may need to add or rename a column. The `ALTER TABLE` command allows you to do this.

**Raw SQL**

```sql
SELECT * FROM users;
┌─────────┬──────────┬────────────┐
│ user_id │ username │  password  │
├─────────┼──────────┼────────────┤
│ 1       │ djs      │ mypa$$word │
│ 2       │ django   │ w0ff       │
│ 3       │ alecg    │ c0de       │
└─────────┴──────────┴────────────┘

-- Renaming a column
ALTER TABLE users RENAME username TO teacher_name;

SELECT * FROM users;
┌─────────┬──────────────┬────────────┐
│ user_id │ teacher_name │  password  │
├─────────┼──────────────┼────────────┤
│ 1       │ djs          │ mypa$$word │
│ 2       │ django       │ w0ff       │
│ 3       │ alecg        │ c0de       │
└─────────┴──────────────┴────────────┘

-- Adding a new column with a default value for each row
ALTER TABLE users ADD is_admin INTEGER DEFAULT 0;

SELECT * FROM users;
┌─────────┬──────────────┬────────────┬──────────┐
│ user_id │ teacher_name │  password  │ is_admin │
├─────────┼──────────────┼────────────┼──────────┤
│ 1       │ djs          │ mypa$$word │ 0        │
│ 2       │ django       │ w0ff       │ 0        │
│ 3       │ alecg        │ c0de       │ 0        │
└─────────┴──────────────┴────────────┴──────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("users-database.db")
sql = con.cursor()

def display_all_users_and_column_names():
    # Don't worry about this, it just shows us the column names
    query = """
        SELECT name FROM PRAGMA_TABLE_INFO('users');
    """

    result = sql.execute(query)
    print("\nColumn names:")
    print(*result.fetchall())

    query = """
        SELECT * FROM users;
    """

    result = sql.execute(query)
    rows = result.fetchall()

    print("\nRows:")
    print(rows)


display_all_users_and_column_names()

query = """
    ALTER TABLE users RENAME username TO teacher_name;
"""

sql.execute(query)
display_all_users_and_column_names()

query = """
    ALTER TABLE users ADD is_admin INTEGER DEFAULT 0;
"""

sql.execute(query)
display_all_users_and_column_names()

# Make sure to commit the changes to the DB
con.commit()
```

**Output**

```text
Column names:
('user_id',) ('username',) ('password',)

Rows:
[(1, 'djs', 'mypa$$word'), (2, 'django', 'w0ff'), (3, 'alecg', 'c0de')]

Column names:
('user_id',) ('teacher_name',) ('password',)

Rows:
[(1, 'djs', 'mypa$$word'), (2, 'django', 'w0ff'), (3, 'alecg', 'c0de')]

Column names:
('user_id',) ('teacher_name',) ('password',) ('is_admin',)

Rows:
[(1, 'djs', 'mypa$$word', 0), (2, 'django', 'w0ff', 0), (3, 'alecg', 'c0de', 0)]
```

**Further Reading**

-   [SQLBolt - Altering Tables](https://sqlbolt.com/lesson/altering_tables)
-   [SQLite Tutorial - SQLite Alter Table](https://www.sqlitetutorial.net/sqlite-alter-table/)

## AS

The `AS` clause is used to alias a column or table name. We only use it at CWHQ for column aliases though, so that's all that is covered here.

### Aliasing Column Names

When aliasing column names, the `AS` clause comes in handy when you are using the concatenation operator (`||`) to combine multiple columns or when using _Aggregate Functions_ to perform some calculation on a group of rows.

**Raw SQL**

```sql
SELECT * FROM products;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

/*
*   Build a result set that combines `product_name` and `product_price`
*   into a single column
*/
SELECT product_name || " : $" || product_price AS product_description
FROM products;
┌───────────────────────────────────┐
│        product_description        │
├───────────────────────────────────┤
│ Dell XPS 17 : $1599.99            │
│ Blue Snowball Microphone : $99.5  │
│ System76 Thelio B1 : $1255.55     │
│ Logitech M1 : $34.99              │
│ Seagate S1 SSD : $88.75           │
│ MacBook Pro 16 : $2100.5          │
│ Rode Z28 : $275.99                │
│ Lenovo ThinkPad : $950.75         │
└───────────────────────────────────┘

-- Get the total cost of all the computers in the `products` table
SELECT SUM(product_price) AS total_price_computers
FROM products
WHERE product_category = "Computers";
┌───────────────────────┐
│ total_price_computers │
├───────────────────────┤
│ 5906.79               │
└───────────────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("products-database.db")
sql = con.cursor()

def execute_query_and_display_rows(query):
    result = sql.execute(query)
    rows = result.fetchall()

    for row in rows:
        print(row)


query = """
    SELECT * FROM products;
"""

print("All products:")
execute_query_and_display_rows(query)

query = """
    SELECT product_name || " : $" || product_price AS product_description
    FROM products;
"""

print("\nFormatted product descriptions:")
execute_query_and_display_rows(query)

query = """
    SELECT SUM(product_price) AS total_price_computers
    FROM products
    WHERE product_category = "Computers";
"""

print("\nThe total price of all computers in the `products` table:")
execute_query_and_display_rows(query)
```

**Output**

```text
All products:
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(6, 'MacBook Pro 16', 2100.5, 'Computers')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')

Formatted product descriptions:
('Dell XPS 17 : $1599.99',)
('Blue Snowball Microphone : $99.5',)
('System76 Thelio B1 : $1255.55',)
('Logitech M1 : $34.99',)
('Seagate S1 SSD : $88.75',)
('MacBook Pro 16 : $2100.5',)
('Rode Z28 : $275.99',)
('Lenovo ThinkPad : $950.75',)

The total price of all computers in the `products` table:
(5906.79,)
```

**Further Reading**

-   [SQLBolt - Queries with expressions](https://sqlbolt.com/lesson/select_queries_with_expressions)

## CASE

The `CASE` statement is similar to a chain of conditional statements in a language like Python or JavaScript. You use it to generate different values based on some condition. At CWHQ, we use the `CASE` statement to generate an additional column with a range of values generated from our other columns.

Consider a shopping app where we want to rank products by their affordability. Any product that costs $100 or less is considered "Cheap", any product between $100 and $1000 is considered "Affordable", and anything else is "Expensive".

Our `products` table has the following structure:

```sql
SELECT * FROM products;

┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘
```

Notice that there is no `affordability` column? We can create one and populate it with values based on the `product_price` by using the `CASE` statement and using `AS` to ensure the result is placed in a column called `affordability`.

The `THEN` keyword is what populates the values in whatever column name we created with `END AS`. If you have an `ELSE` clause, it doesn't need a `THEN` clause.

**Raw SQL**

```sql
SELECT product_name, product_price,
CASE
    WHEN product_price <= 100
        THEN 'Cheap'
    WHEN product_price > 100 AND product_price <= 1000
        THEN 'Affordable'
    ELSE
        'Expensive'
END AS affordability
FROM products
ORDER BY product_price;

┌──────────────────────────┬───────────────┬───────────────┐
│       product_name       │ product_price │ affordability │
├──────────────────────────┼───────────────┼───────────────┤
│ Logitech M1              │ 34.99         │ Cheap         │
│ Seagate S1 SSD           │ 88.75         │ Cheap         │
│ Blue Snowball Microphone │ 99.5          │ Cheap         │
│ Rode Z28                 │ 275.99        │ Affordable    │
│ Lenovo ThinkPad          │ 950.75        │ Affordable    │
│ System76 Thelio B1       │ 1255.55       │ Expensive     │
│ Dell XPS 17              │ 1599.99       │ Expensive     │
│ MacBook Pro 16           │ 2100.5        │ Expensive     │
└──────────────────────────┴───────────────┴───────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("products.db")
sql = con.cursor()

query = """
    SELECT product_name, product_price,
    CASE
        WHEN product_price <= 100
            THEN 'Cheap'
        WHEN product_price > 100 AND product_price <= 1000
            THEN 'Affordable'
        ELSE
            'Expensive'
    END AS affordability
    FROM products
    ORDER BY product_price;
"""

result = sql.execute(query)
rows = result.fetchall()

for row in rows:
    print(row)

```

**Output**

```text
('Logitech M1', 34.99, 'Cheap')
('Seagate S1 SSD', 88.75, 'Cheap')
('Blue Snowball Microphone', 99.5, 'Cheap')
('Rode Z28', 275.99, 'Affordable')
('Lenovo ThinkPad', 950.75, 'Affordable')
('System76 Thelio B1', 1255.55, 'Expensive')
('Dell XPS 17', 1599.99, 'Expensive')
('MacBook Pro 16', 2100.5, 'Expensive')
```

**Further Reading**

-   [Mode SQL Tutorial - SQL CASE](https://mode.com/sql-tutorial/sql-case/)

## Concatenation

SQLite uses the `||` operator for string concatenation. This is used at CWHQ to combine column names together (possibly with other string data) to merge the data from multiple columns into a single column. This is often used in conjunction with the `AS` clause to rename the combined columns.

**Raw SQL**

```sql
SELECT * FROM products;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

/*
*   Build a result set that combines `product_name` and `product_price`
*   into a single column using `||` and `AS`
*/
SELECT product_name || " : $" || product_price AS product_description
FROM products;
┌───────────────────────────────────┐
│        product_description        │
├───────────────────────────────────┤
│ Dell XPS 17 : $1599.99            │
│ Blue Snowball Microphone : $99.5  │
│ System76 Thelio B1 : $1255.55     │
│ Logitech M1 : $34.99              │
│ Seagate S1 SSD : $88.75           │
│ MacBook Pro 16 : $2100.5          │
│ Rode Z28 : $275.99                │
│ Lenovo ThinkPad : $950.75         │
└───────────────────────────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("products-database.db")
sql = con.cursor()

def execute_query_and_display_rows(query):
    result = sql.execute(query)
    rows = result.fetchall()

    for row in rows:
        print(row)


query = """
    SELECT * FROM products;
"""

print("All products:")
execute_query_and_display_rows(query)

query = """
    SELECT product_name || " : $" || product_price AS product_description
    FROM products;
"""
```

**Output**

```text
All products:
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(6, 'MacBook Pro 16', 2100.5, 'Computers')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')

Formatted product descriptions:
('Dell XPS 17 : $1599.99',)
('Blue Snowball Microphone : $99.5',)
('System76 Thelio B1 : $1255.55',)
('Logitech M1 : $34.99',)
('Seagate S1 SSD : $88.75',)
('MacBook Pro 16 : $2100.5',)
('Rode Z28 : $275.99',)
('Lenovo ThinkPad : $950.75',)
```

## CREATE TABLE

Relational databases are made up of tables, and you'll need to create tables to hold your data if we don't provide one for you. We often use `IF NOT EXISTS` in CWHQ courses when creating a table because we'll run the statement every time our Python script runs, and an error would occur if you tried to create a table that already existed. Most tables should also have a `PRIMARY KEY` integer to uniquely identify each row of data.

The general format of a `CREATE TABLE` statement is:

```sql
CREATE TABLE IF NOT EXISTS table_name (
    column_one DATATYPE OPTIONAL_CONSTRAINTS...,
    column_two DATATYPE OPTIONAL_CONSTRAINTS...,
    column_three DATATYPE OPTIONAL_CONSTRAINTS...
    -- etc...
);
```

Note that each column definition is separated by a comma (`,`) but the final column definition should _not_ have a comma.

Here's an example of a `CREATE TABLE` statement for the `users` table from the [What Is A Relational Database?](#what-is-a-relational-database) section earlier in these docs:

**Raw SQL**

```sql
CREATE TABLE IF NOT EXISTS users (
    user_id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT UNIQUE NOT NULL,
    password TEXT NOT NULL
);
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("users-database.db")
sql = con.cursor()

query = """
    CREATE TABLE IF NOT EXISTS users (
        user_id INTEGER PRIMARY KEY AUTOINCREMENT,
        username TEXT UNIQUE NOT NULL,
        password TEXT NOT NULL
    );
"""

sql.execute(query)
```

### Column Datatypes

When writing column definitions, your column can be one of 5 storage classes (which are a generic datatype) in SQLite:

-   `NULL`: Represents "nothingness"
-   `INTEGER`: Whole numbers
-   `REAL`: Decimal numbers
-   `TEXT`: Text data
-   `BLOB`: Binary data (like images, music, etc.)

You'll mainly use `INTEGER` and `TEXT` for CWHQ projects.

### Column Constraints

Besides the datatype, you can also put additional constraints on a column definition to enforce that a column is `UNIQUE`, or `NOT NULL`, or even a `PRIMARY KEY`. You can see all of those at work in this example:

```sql
CREATE TABLE IF NOT EXISTS users (
    user_id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT UNIQUE NOT NULL,
    password TEXT NOT NULL
);
```

**Further Reading**

-   [SQLBolt - Creating tables](https://sqlbolt.com/lesson/creating_tables)
-   [SQLite Tutorial - SQLite Create Table](https://www.sqlitetutorial.net/sqlite-create-table/)

## DELETE

To remove data in a SQL table, use the `DELETE` statement. Make sure to use a `WHERE` clause so that you only delete the rows you intend to.

**Raw SQL**

```sql
SELECT * FROM users;
┌─────────┬──────────┬────────────┐
│ user_id │ username │  password  │
├─────────┼──────────┼────────────┤
│ 1       │ djs      │ mypa$$word │
│ 2       │ django   │ w0ff       │
│ 3       │ alecg    │ c0de       │
└─────────┴──────────┴────────────┘

DELETE FROM users WHERE user_id = 3;

SELECT * FROM users;
┌─────────┬──────────┬────────────┐
│ user_id │ username │  password  │
├─────────┼──────────┼────────────┤
│ 1       │ djs      │ mypa$$word │
│ 2       │ django   │ w0ff       │
└─────────┴──────────┴────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("users-database.db")
sql = con.cursor()

# We'll use this twice, so it makes sense to be a function
def display_all_users():
    query = """
        SELECT * FROM users;
    """

    result = sql.execute(query)
    rows = result.fetchall()

    print(rows)


display_all_users()

query = """
    DELETE FROM users WHERE id = 3;
"""

sql.execute(query)

# Make sure to commit the changes to the DB
con.commit()

display_all_users()
```

**Output**

```text
[(1, 'djs', 'mypa$$word'), (2, 'django', 'w0ff'), (3, 'alecg', 'c0de')]
[(1, 'djs', 'mypa$$word'), (2, 'django', 'w0ff')]
```

### Deleting all rows from a table

If you leave out the `WHERE` clause in a `DELETE` statement, you remove all rows from the table. This is a handy way to clear out all the rows if you need to start with a fresh table:

**Raw SQL**

```sql
SELECT * FROM users;
┌─────────┬──────────┬────────────┐
│ user_id │ username │  password  │
├─────────┼──────────┼────────────┤
│ 1       │ djs      │ mypa$$word │
│ 2       │ django   │ w0ff       │
│ 3       │ alecg    │ c0de       │
└─────────┴──────────┴────────────┘

DELETE FROM users;

SELECT * FROM users;
-- nothing returned because the table is empty
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("users-database.db")
sql = con.cursor()

# We'll use this twice, so it makes sense to be a function
def display_all_users():
    query = """
        SELECT * FROM users;
    """

    result = sql.execute(query)
    rows = result.fetchall()

    print(rows)


display_all_users()

query = """
    DELETE FROM users;
"""

sql.execute(query)

# Make sure to commit the changes to the DB
con.commit()

display_all_users()
```

**Output**

```text
[(1, 'djs', 'mypa$$word'), (2, 'django', 'w0ff'), (3, 'alecg', 'c0de')]
[]
```

**Further Reading**

-   [SQLBolt - Deleting rows](https://sqlbolt.com/lesson/deleting_rows)
-   [SQLite Tutorial - SQLite Delete](https://www.sqlitetutorial.net/sqlite-delete/)

## DISTINCT

If you want to get unique column values for a set of rows, use the `DISTINCT` clause of a `SELECT` query

For example, in the `products` table below, it may be hard at a glance to see what categories are present, but with `DISTINCT` it's easy to see we only have three!

**Raw SQL**

```sql
SELECT * FROM products;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

-- Get only the unique categories for our products.
SELECT DISTINCT product_category FROM products;
┌──────────────────┐
│ product_category │
├──────────────────┤
│ Computers        │
│ Microphones      │
│ Accessories      │
└──────────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("products-database.db")
sql = con.cursor()

query = """
    SELECT * FROM products;
"""

result = sql.execute(query)
rows = result.fetchall()

# Easier to read if we loop then print each row since there are 8 rows.
for row in rows:
    print(row)

query = """
    SELECT DISTINCT product_category FROM products;
"""

result = sql.execute(query)
rows = result.fetchall()

print("\nDistinct categories:")
print(rows)
```

**Output**

```text
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(6, 'MacBook Pro 16', 2100.5, 'Computers')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')

Distinct categories:
[('Computers',), ('Microphones',), ('Accessories',)]
```

**Further Reading**

-   [SQLBolt - Filtering and sorting Query results](https://sqlbolt.com/lesson/filtering_sorting_query_results)
-   [SQLite Tutorial - SQLite Select Distinct](https://www.sqlitetutorial.net/sqlite-distinct/)

## DROP TABLE

The `DROP TABLE` query deletes an entire table and it's definition from the database. You should usually use the `IF EXISTS` clause with this query to ensure an error isn't thrown if the table you're trying to drop doesn't exist.

**Raw SQL**

```sql
SELECT * FROM users;
┌─────────┬──────────┬────────────┐
│ user_id │ username │  password  │
├─────────┼──────────┼────────────┤
│ 1       │ djs      │ mypa$$word │
│ 2       │ django   │ w0ff       │
│ 3       │ alecg    │ c0de       │
└─────────┴──────────┴────────────┘

DROP TABLE IF EXISTS users;

SELECT * FROM users;
-- Error: no such table: users
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("users-database.db")
sql = con.cursor()

# We'll use this twice, so it makes sense to be a function
def display_all_users():
    query = """
        SELECT * FROM users;
    """

    result = sql.execute(query)
    rows = result.fetchall()

    print(rows)


display_all_users()

query = """
    DROP TABLE IF EXISTS users;
"""

sql.execute(query)

# This will throw an error since the `users` table doesn't exist.
display_all_users()
```

**Output**

```text
[(1, 'djs', 'mypa$$word'), (2, 'django', 'w0ff'), (3, 'alecg', 'c0de')]
Traceback (most recent call last):
  File "/home/daniel/documentation-examples/main.py", line 27, in <module>
    display_all_users()
  File "/home/daniel/documentation-examples/main.py", line 12, in display_all_users
    result = sql.execute(query)
sqlite3.OperationalError: no such table: users
```

**Further Reading**

-   [SQLBolt - Dropping tables](https://sqlbolt.com/lesson/dropping_tables)
-   [SQLite Tutorial - SQLite Drop Table](https://www.sqlitetutorial.net/sqlite-drop-table/)

## GROUP BY

If you need to "flatten" the results of a `SELECT` query, the `GROUP BY` clause is helpful. It let's you group the resulting rows by a particular column, effectively filtering out duplicate rows that have the same column value. You almost always use `GROUP BY` with an _Aggregate Function_ to perform some sort of calculation on a group of rows with similar column values, but you can also use it to filter a column by unique values (as we do to get the unique product categories below):

**Raw SQL**

```sql
SELECT * FROM products;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

-- Get the unique product categories
SELECT product_category FROM products GROUP BY product_category;
┌──────────────────┐
│ product_category │
├──────────────────┤
│ Accessories      │
│ Computers        │
│ Microphones      │
└──────────────────┘

-- Get the number of products in each `product_category`
SELECT product_category, COUNT(*) AS num_products_per_category
FROM products
GROUP BY product_category;
┌──────────────────┬───────────────────────────┐
│ product_category │ num_products_per_category │
├──────────────────┼───────────────────────────┤
│ Accessories      │ 2                         │
│ Computers        │ 4                         │
│ Microphones      │ 2                         │
└──────────────────┴───────────────────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("products-database.db")
sql = con.cursor()

def execute_query_and_display_rows(query):
    result = sql.execute(query)
    rows = result.fetchall()

    for row in rows:
        print(row)

query = """
    SELECT * FROM products;
"""

print("All products:")
execute_query_and_display_rows(query)

query = """
    SELECT product_category FROM products GROUP BY product_category;
"""

print("\nUnique `product_categories`:")
execute_query_and_display_rows(query)

query = """
    SELECT product_category, COUNT(*) AS num_products_per_category
    FROM products
    GROUP BY product_category;
"""

print("\nNumber of products per category:")
execute_query_and_display_rows(query)
```

**Output**

```text
All products:
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(6, 'MacBook Pro 16', 2100.5, 'Computers')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')

Unique `product_categories`:
('Accessories',)
('Computers',)
('Microphones',)

Number of products per category:
('Accessories', 2)
('Computers', 4)
('Microphones', 2)
```

**Further Reading**

-   [SQLBolt - Queries with aggregates - Pt. 1](https://sqlbolt.com/lesson/select_queries_with_aggregates)
-   [SQLite Tutorial - SQLite Group By](https://www.sqlitetutorial.net/sqlite-group-by/)

## INSERT

Once you've created a table, you'll want to put data in it. The `INSERT` statement is used to add data to a SQL table. You list the column names in the `()` after the table name.

Consider this `users` table definition:

```sql
CREATE TABLE IF NOT EXISTS users (
    user_id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT UNIQUE NOT NULL,
    password TEXT NOT NULL
);
```

If we wanted to fill this table with a few users, we would leave out the `user_id` in the `()` as this table has the `user_id` set to `AUTOINCREMENT`. We would need to add the other two column names in whatever order we wished, though.

**Raw SQL**

```sql
INSERT INTO users (username, password) VALUES ("djs", "mypa$$word");
INSERT INTO users (username, password) VALUES ("django", "w0ff");
INSERT INTO users (username, password) VALUES ("alecg", "c0de");

SELECT * FROM users;
┌─────────┬──────────┬────────────┐
│ user_id │ username │  password  │
├─────────┼──────────┼────────────┤
│ 1       │ djs      │ mypa$$word │
│ 2       │ django   │ w0ff       │
│ 3       │ alecg    │ c0de       │
└─────────┴──────────┴────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("users-database.db")
sql = con.cursor()

query = """
    INSERT INTO users (username, password) VALUES ("djs", "mypa$$word");
"""
sql.execute(query)

query = """
    INSERT INTO users (username, password) VALUES ("django", "w0ff");
"""
sql.execute(query)

query = """
    INSERT INTO users (username, password) VALUES ("alecg", "c0de");
"""
sql.execute(query)

# Make sure the changes are saved to the DB.
con.commit()

query = """
    SELECT * FROM users;
"""

result = sql.execute(query)
rows = result.fetchall()

print(rows)
```

**Output**

```text
[(1, 'djs', 'mypa$$word'), (2, 'django', 'w0ff'), (3, 'alecg', 'c0de')]
```

### Inserting multiple rows into a table

If you want to insert multiple rows into a database table, you can use a single `INSERT` statement and group each row in `()`.

**Raw SQL**

```sql
INSERT INTO users (username, password)
VALUES
    ("djs", "mypa$$word"),
    ("django", "w0ff"),
    ("alecg", "c0de");


SELECT * FROM users;
┌─────────┬──────────┬────────────┐
│ user_id │ username │  password  │
├─────────┼──────────┼────────────┤
│ 1       │ djs      │ mypa$$word │
│ 2       │ django   │ w0ff       │
│ 3       │ alecg    │ c0de       │
└─────────┴──────────┴────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("users-database.db")
sql = con.cursor()

query = """
    INSERT INTO users (username, password)
    VALUES
        ("djs", "mypa$$word"),
        ("django", "w0ff"),
        ("alecg", "c0de");
"""

sql.execute(query)
con.commit()

query = """
    SELECT * FROM users;
"""

result = sql.execute(query)
rows = result.fetchall()

print(rows)
```

**Output**

```text
[(1, 'djs', 'mypa$$word'), (2, 'django', 'w0ff'), (3, 'alecg', 'c0de')]
```

**Further Reading**

-   [SQLBolt - Inserting rows](https://sqlbolt.com/lesson/inserting_rows)
-   [SQLite Tutorial - SQLite Insert](https://www.sqlitetutorial.net/sqlite-insert/)

## JOIN

Being able to combine data from related tables is one of the things that makes a relational database like SQLite so powerful.

### Defining Table Relationships

Before you can `JOIN` two tables, they must share a common key. Consider the following two table schemas, which represent data about authors and books:

```sql
CREATE TABLE authors (
    author_id INTEGER PRIMARY KEY AUTOINCREMENT,
    author_name TEXT NOT NULL
);

CREATE TABLE books (
    book_id INTEGER PRIMARY KEY AUTOINCREMENT,
    author_id INTEGER NOT NULL REFERENCES authors (author_id), -- the Foreign Key relationship
    book_title TEXT UNIQUE NOT NULL
);
```

We can relate the two tables with the `REFERENCES` keyword. The `author_id` is known as a _Foreign Key_ in the `books` table because it's merely pointing to the `PRIMARY KEY` of the `authors` table. It's the `author_id` shared between the `authors` and `books` tables that allows us to `JOIN` them together.

### JOINING Tables Together

Now that we have an established relationship between our `authors` and `books` tables, we can `JOIN` them together. We'll preface each column name with the table it references since we'll be referring to multiple tables like this `table_name.column_name`. This isn't always strictly required, but it makes it easier to understand which table each column references in the query.

**Raw SQL**

```sql
SELECT * FROM authors;
┌───────────┬───────────────┐
│ author_id │  author_name  │
├───────────┼───────────────┤
│ 1         │ J.D. Salinger │
│ 2         │ Harper Lee    │
│ 3         │ Truman Capote │
└───────────┴───────────────┘

SELECT * FROM books;
┌─────────┬───────────┬────────────────────────┐
│ book_id │ author_id │       book_title       │
├─────────┼───────────┼────────────────────────┤
│ 1       │ 2         │ To Kill a Mockingbird  │
│ 2       │ 3         │ In Cold Blood          │
│ 3       │ 1         │ The Catcher in the Rye │
│ 4       │ 3         │ Breakfast at Tiffanys  │
│ 5       │ 1         │ Franny and Zooey       │
│ 6       │ 3         │ Summer Crossing        │
│ 7       │ 2         │ Go Set a Watchman      │
└─────────┴───────────┴────────────────────────┘

-- Join the `authors` and `books` tables together
SELECT authors.author_name, books.book_title
FROM authors
JOIN books ON authors.author_id = books.author_id;
┌───────────────┬────────────────────────┐
│  author_name  │       book_title       │
├───────────────┼────────────────────────┤
│ Harper Lee    │ To Kill a Mockingbird  │
│ Truman Capote │ In Cold Blood          │
│ J.D. Salinger │ The Catcher in the Rye │
│ Truman Capote │ Breakfast at Tiffanys │
│ J.D. Salinger │ Franny and Zooey       │
│ Truman Capote │ Summer Crossing        │
│ Harper Lee    │ Go Set a Watchman      │
└───────────────┴────────────────────────┘

-- Getting a bit fancier by ordering by `author_name`
SELECT authors.author_name, books.book_title
FROM authors
JOIN books ON authors.author_id = books.author_id
ORDER BY authors.author_name;
┌───────────────┬────────────────────────┐
│  author_name  │       book_title       │
├───────────────┼────────────────────────┤
│ Harper Lee    │ To Kill a Mockingbird  │
│ Harper Lee    │ Go Set a Watchman      │
│ J.D. Salinger │ The Catcher in the Rye │
│ J.D. Salinger │ Franny and Zooey       │
│ Truman Capote │ In Cold Blood          │
│ Truman Capote │ Breakfast at Tiffanys │
│ Truman Capote │ Summer Crossing        │
└───────────────┴────────────────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("library-database.db")
sql = con.cursor()

def execute_query_and_display_rows(query):
    result = sql.execute(query)
    rows = result.fetchall()

    for row in rows:
        print(row)


query = """
    SELECT * FROM authors;
"""

print("All rows in the `authors` table:")
execute_query_and_display_rows(query)

query = """
    SELECT * FROM books;
"""

print("\nAll rows in the `books` table:")
execute_query_and_display_rows(query)


query = """
    SELECT authors.author_name, books.book_title
    FROM authors
    JOIN books ON authors.author_id = books.author_id;
"""

print("\nJoining the `authors` and `books` tables:")
execute_query_and_display_rows(query)

query = """
    SELECT authors.author_name, books.book_title
    FROM authors
    JOIN books ON authors.author_id = books.author_id
    ORDER BY authors.author_name;
"""

print("\nJoining and sorting the `authors` and `books` tables:")
execute_query_and_display_rows(query)
```

**Output**

```text
All rows in the `authors` table:
(1, 'J.D. Salinger')
(2, 'Harper Lee')
(3, 'Truman Capote')

All rows in the `books` table:
(1, 2, 'To Kill a Mockingbird')
(2, 3, 'In Cold Blood')
(3, 1, 'The Catcher in the Rye')
(4, 3, "Breakfast at Tiffany's")
(5, 1, 'Franny and Zooey')
(6, 3, 'Summer Crossing')
(7, 2, 'Go Set a Watchman')

Joining the `authors` and `books` tables:
('Harper Lee', 'To Kill a Mockingbird')
('Truman Capote', 'In Cold Blood')
('J.D. Salinger', 'The Catcher in the Rye')
('Truman Capote', "Breakfast at Tiffany's")
('J.D. Salinger', 'Franny and Zooey')
('Truman Capote', 'Summer Crossing')
('Harper Lee', 'Go Set a Watchman')

Joining and sorting the `authors` and `books` tables:
('Harper Lee', 'To Kill a Mockingbird')
('Harper Lee', 'Go Set a Watchman')
('J.D. Salinger', 'The Catcher in the Rye')
('J.D. Salinger', 'Franny and Zooey')
('Truman Capote', 'In Cold Blood')
('Truman Capote', "Breakfast at Tiffany's")
('Truman Capote', 'Summer Crossing')
```

#### The `USING()` shorthand

When using a `JOIN`, you don't have to use the `ON table.column_name = other_table.column_name` syntax if the column names are the same in both tables. We could rewrite the last `JOIN` from the previous example in a shorter way with `USING()` like so:

```sql
SELECT authors.author_name, books.book_title
FROM authors
JOIN books USING (author_id)  -- This is a nice shorthand
ORDER BY authors.author_name;
┌───────────────┬────────────────────────┐
│  author_name  │       book_title       │
├───────────────┼────────────────────────┤
│ Harper Lee    │ To Kill a Mockingbird  │
│ Harper Lee    │ Go Set a Watchman      │
│ J.D. Salinger │ The Catcher in the Rye │
│ J.D. Salinger │ Franny and Zooey       │
│ Truman Capote │ In Cold Blood          │
│ Truman Capote │ Breakfast at Tiffanys │
│ Truman Capote │ Summer Crossing        │
└───────────────┴────────────────────────┘
```

**Further Reading**

-   [SQLBolt - Multi-table queries with JOINs](https://sqlbolt.com/lesson/select_queries_with_joins)
-   [SQLite Tutorial - SQLite Join](https://www.sqlitetutorial.net/sqlite-join/)

## LIMIT

Sometimes, you may want to get a limited number of rows back from a `SELECT` query. The `LIMIT` clause allows you to do this:

**Raw SQL**

```sql
SELECT * FROM products;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

-- Only get the first 3 products in the table (by `product_id`)
SELECT * FROM products LIMIT 3;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("products-database.db")
sql = con.cursor()

# We'll use this a few times so it makes sense for it to be a function
def fetch_and_display_rows(query):
    result = sql.execute(query)
    rows = result.fetchall()

    for row in rows:
        print(row)


query = """
    SELECT * FROM products;
"""

fetch_and_display_rows(query)

query = """
    SELECT * FROM products LIMIT 3;
"""

print("\nThe first three products in the table:")
fetch_and_display_rows(query)
```

**Output**

```text
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(6, 'MacBook Pro 16', 2100.5, 'Computers')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')

The first three products in the table:
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
```

**Further Reading**

-   [SQLBolt - Filtering and sorting Query results](https://sqlbolt.com/lesson/filtering_sorting_query_results)
-   [SQLite Tutorial - SQLite Limit](https://www.sqlitetutorial.net/sqlite-limit/)

## NULL

The `NULL` datatype allows you to express a missing or unknown value.

### Avoiding NULL Values In CREATE TABLE Statements

Generally, `NULL` values should be avoided by adding a `NOT NULL` constraint to your `CREATE TABLE` definitions like so:

```sql
CREATE TABLE products (
    product_id INTEGER PRIMARY KEY AUTOINCREMENT,
    product_name TEXT UNIQUE NOT NULL,
    product_price REAL NOT NULL,
    product_category TEXT NOT NULL
);
```

If a column has a `NOT NULL` constraint and you try to enter a `NULL` value for that column, you'll get an error:

**Raw SQL**

```sql
SELECT * FROM products;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

INSERT INTO products (product_name, product_price, product_category)
VALUES ("mousepad", NULL, "Accessories");
-- Error: NOT NULL constraint failed: products.product_price
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("products-database.db")
sql = con.cursor()

query = """
    SELECT * FROM products;
"""

print("All products:")
result = sql.execute(query)
rows = result.fetchall()

for row in rows:
    print(row)


query = """
    INSERT INTO products (product_name, product_price, product_category)
    VALUES ("mousepad", NULL, "Accessories");
"""

# This will throw an error
sql.execute(query)
con.commit()
```

**Output**

```text
All products:
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(6, 'MacBook Pro 16', 2100.5, 'Computers')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')
Traceback (most recent call last):
  File "/home/daniel/documentation-examples/main.py", line 24, in <module>
    sql.execute(query)
sqlite3.IntegrityError: NOT NULL constraint failed: products.product_price
```

### Filtering NULL Values In SELECT Statements

You can use `IS NULL` and `IS NOT NULL` to filter `SELECT` statements by columns with or without `NULL` values. This can be valuable to find rows with missing information or to only display rows with no missing information.

Note that in Python, `NULL` translates to the `None` datatype.

**Raw SQL**

```sql
/*
*   We can see that the "Lenovo ThinkPad" doesn't have a `product_price`.
*   That's because it's `NULL`!
*/
SELECT * FROM products;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │               │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

/*
*   We can filter our results to find products with missing
*   `product_price` data.
*/
SELECT * FROM products WHERE product_price IS NULL;
┌────────────┬─────────────────┬───────────────┬──────────────────┐
│ product_id │  product_name   │ product_price │ product_category │
├────────────┼─────────────────┼───────────────┼──────────────────┤
│ 8          │ Lenovo ThinkPad │               │ Computers        │
└────────────┴─────────────────┴───────────────┴──────────────────┘

/*
*   We can also filter out rows that have a `NULL` value for
*   `product_price`.
*/
SELECT * FROM products WHERE product_price IS NOT NULL;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("products-database.db")
sql = con.cursor()

def execute_query_and_display_rows(query):
    result = sql.execute(query)
    rows = result.fetchall()

    for row in rows:
        print(row)


query = """
    SELECT * FROM products;
"""

print("All products:")
execute_query_and_display_rows(query)

query = """
    SELECT * FROM products WHERE product_price IS NULL;
"""

print("\nProducts with `NULL` values for their price:")
execute_query_and_display_rows(query)

query = """
    SELECT * FROM products WHERE product_price IS NOT NULL;
"""

print("\nProducts __without__ `NULL` values for their price:")
execute_query_and_display_rows(query)
```

**Output**

```text
All products:
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(6, 'MacBook Pro 16', 2100.5, 'Computers')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', None, 'Computers')

Products with `NULL` values for their price:
(8, 'Lenovo ThinkPad', None, 'Computers')

Products __without__ `NULL` values for their price:
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(6, 'MacBook Pro 16', 2100.5, 'Computers')
(7, 'Rode Z28', 275.99, 'Microphones')
```

**Further Reading**

-   [SQLBolt - A short note on NULLs](https://sqlbolt.com/lesson/select_queries_with_nulls)
-   [SQLite Tutorial - SQLite IS NULL](https://www.sqlitetutorial.net/sqlite-is-null/)

## OFFSET

If you've ever visited a website like Amazon.com, you know that when you search for a particular product, there are multiple pages of results. The `OFFSET` clause allows you to move the starting point of the returned rows from a query. It's usually used in conjunction with a `LIMIT` clause for things like pagination (as in the Amazon example).

**Raw SQL**

```sql
SELECT * FROM products;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

-- Only get the first 3 products in the table (by `product_id`)
SELECT * FROM products LIMIT 3;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

-- Get the next 3 products in the table
SELECT * FROM products LIMIT 3 OFFSET 3;
┌────────────┬────────────────┬───────────────┬──────────────────┐
│ product_id │  product_name  │ product_price │ product_category │
├────────────┼────────────────┼───────────────┼──────────────────┤
│ 4          │ Logitech M1    │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD │ 88.75         │ Accessories      │
│ 6          │ MacBook Pro 16 │ 2100.5        │ Computers        │
└────────────┴────────────────┴───────────────┴──────────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("products-database.db")
sql = con.cursor()

# We'll use this a few times so it makes sense for it to be a function
def fetch_and_display_rows(query):
    result = sql.execute(query)
    rows = result.fetchall()

    for row in rows:
        print(row)


query = """
    SELECT * FROM products;
"""

fetch_and_display_rows(query)

query = """
    SELECT * FROM products LIMIT 3;
"""

print("\nThe first three products in the table:")
fetch_and_display_rows(query)

query = """
    SELECT * FROM products LIMIT 3 OFFSET 3;
"""

print("\nThe second group of three products in the table:")
fetch_and_display_rows(query)
```

**Output**

```text
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(6, 'MacBook Pro 16', 2100.5, 'Computers')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')

The first three products in the table:
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')

The second group of three products in the table:
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(6, 'MacBook Pro 16', 2100.5, 'Computers')
```

**Further Reading**

-   [SQLBolt - Filtering and sorting Query results](https://sqlbolt.com/lesson/filtering_sorting_query_results)
-   [SQLite Tutorial - SQLite Limit](https://www.sqlitetutorial.net/sqlite-limit/)

## ORDER BY

The `ORDER BY` clause allows you to order rows in ascending (`ASC`) or descending (`DESC`) order alphanumerically. You use it with a `SELECT` query to order the output.

**Raw SQL**

```sql
SELECT * FROM products;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

-- Ordering products from lowest price to highest price
SELECT * FROM products ORDER BY product_price;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

-- ASC is the default, so it's the the same as doing nothing after ORDER BY
SELECT * FROM products ORDER BY product_price ASC;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

-- Ordering products from highest price to lowest price
SELECT * FROM products ORDER BY product_price DESC;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("products-database.db")
sql = con.cursor()

# We'll use this a few times so it makes sense for it to be a function
def fetch_and_display_all_rows(query):
    result = sql.execute(query)
    rows = result.fetchall()

    for row in rows:
        print(row)


query = """
    SELECT * FROM products;
"""

fetch_and_display_all_rows(query)

query = """
    SELECT * FROM products ORDER BY product_price;
"""

print("\nProducts ordered from price lowest to highest price:")
fetch_and_display_all_rows(query)

query = """
    SELECT * FROM products ORDER BY product_price DESC;
"""

print("\nProducts ordered from price highest to lowest price:")
fetch_and_display_all_rows(query)
```

**Output**

```text
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(6, 'MacBook Pro 16', 2100.5, 'Computers')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')

Products ordered from price lowest to highest price:
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(1, 'Dell XPS 17', 1599.99, 'Computers')
(6, 'MacBook Pro 16', 2100.5, 'Computers')

Products ordered from price highest to lowest price:
(6, 'MacBook Pro 16', 2100.5, 'Computers')
(1, 'Dell XPS 17', 1599.99, 'Computers')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')
(7, 'Rode Z28', 275.99, 'Microphones')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(4, 'Logitech M1', 34.99, 'Accessories')
```

**Further Reading**

-   [SQLBolt - Filtering and sorting Query results](https://sqlbolt.com/lesson/filtering_sorting_query_results)
-   [SQLite Tutorial - SQLite Order By](https://www.sqlitetutorial.net/sqlite-order-by/)

## SELECT

To see what data is in a SQL table, you use the `SELECT` statement.

### Selecting all of the rows and columns from a table

You can `SELECT *` from a table and that'll give you all of the rows in that table along with all the columns. Be aware that the `*` means "Give me all the columns" not "Give me all the rows". All rows are returned from a `SELECT` query unless you begin using filters like `WHERE`, `LIMIT`, or `DISTINCT`.

**Raw SQL**

```sql
SELECT * FROM users;
┌─────────┬──────────┬────────────┐
│ user_id │ username │  password  │
├─────────┼──────────┼────────────┤
│ 1       │ djs      │ mypa$$word │
│ 2       │ django   │ w0ff       │
│ 3       │ alecg    │ c0de       │
└─────────┴──────────┴────────────┘
```

When selecting data from Python, you can fetch all of the rows by using the `fetchall()` method of the query result. Note that `fetchall()` returns a `list` of `tuples`, so you would need to do further processing from Python to get the individual rows from this `list`, such as looping through the rows.

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("users-database.db")
sql = con.cursor()

query = """
    SELECT * FROM users;
"""

result = sql.execute(query)
rows = result.fetchall()

print(rows)

for row in rows:
    # Using multiple assignment to get the values from each row
    user_id, username, password = row
    print(f"User ID: {user_id}")
    print(f"Username: {username}")
    print(f"Password: {password}")

```

**Output**

```text
[(1, 'djs', 'mypa$$word'), (2, 'django', 'w0ff'), (3, 'alecg', 'c0de')]
User ID: 1
Username: djs
Password: mypa$$word
User ID: 2
Username: django
Password: w0ff
User ID: 3
Username: alecg
Password: c0de
```

### Selecting specific columns from a table

If you only want certain columns returned, you can list them separated by commas after the `SELECT` keyword. Notice how the `user_id` column is not present in the result set in the query below.

**Raw SQL**

```sql
SELECT username, password FROM users;
┌──────────┬────────────┐
│ username │  password  │
├──────────┼────────────┤
│ djs      │ mypa$$word │
│ django   │ w0ff       │
│ alecg    │ c0de       │
└──────────┴────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("users-database.db")
sql = con.cursor()

query = """
    SELECT username, password FROM users;
"""

result = sql.execute(query)
rows = result.fetchall()

print(rows)
```

**Output**

```text
[('djs', 'mypa$$word'), ('django', 'w0ff'), ('alecg', 'c0de')]
```

**Further Reading**

-   [SQLBolt - SELECT queries 101](https://sqlbolt.com/lesson/select_queries_introduction)
-   [SQLite Tutorial - SQLite Select](https://www.sqlitetutorial.net/sqlite-select/)

## UPDATE

If you need to change data in a SQL table, the `UPDATE` statement is used. Make sure to use a `WHERE` clause so that you only update the rows you intend to change.

**Raw SQL**

```sql
SELECT * FROM users;
┌─────────┬──────────┬────────────┐
│ user_id │ username │  password  │
├─────────┼──────────┼────────────┤
│ 1       │ djs      │ mypa$$word │
│ 2       │ django   │ w0ff       │
│ 3       │ alecg    │ c0de       │
└─────────┴──────────┴────────────┘

-- The `djs` user will now have `danielj` as their username.
UPDATE users SET username = "danielj" WHERE user_id = 1;

SELECT * FROM users;
┌─────────┬──────────┬────────────┐
│ user_id │ username │  password  │
├─────────┼──────────┼────────────┤
│ 1       │ danielj  │ mypa$$word │
│ 2       │ django   │ w0ff       │
│ 3       │ alecg    │ c0de       │
└─────────┴──────────┴────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("users-database.db")
sql = con.cursor()

# We'll use this twice, so it makes sense to be a function
def display_all_users():
    query = """
        SELECT * FROM users;
    """

    result = sql.execute(query)
    rows = result.fetchall()

    print(rows)


display_all_users()

query = """
    UPDATE users SET username = "danielj" WHERE id = 1;
"""

sql.execute(query)

# Make sure to commit the changes to the DB
con.commit()

display_all_users()
```

**Output**

```text
[(1, 'djs', 'mypa$$word'), (2, 'django', 'w0ff'), (3, 'alecg', 'c0de')]
[(1, 'danielj', 'mypa$$word'), (2, 'django', 'w0ff'), (3, 'alecg', 'c0de')]
```

### Updating multiple columns

If you need to update multiple columns, you can separate the `SET` clauses with commas. We've also put each new SQL command on a new line and added some indentation to make this longer query easier to read.

**Raw SQL**

```sql
SELECT * FROM users;
┌─────────┬──────────┬────────────┐
│ user_id │ username │  password  │
├─────────┼──────────┼────────────┤
│ 1       │ djs      │ mypa$$word │
│ 2       │ django   │ w0ff       │
│ 3       │ alecg    │ c0de       │
└─────────┴──────────┴────────────┘

UPDATE users
SET
    username = "danielj", -- note the comma here
    password = "b3tTerpa$$w0rd"
WHERE user_id = 1;

SELECT * FROM users;
┌─────────┬──────────┬────────────────┐
│ user_id │ username │    password    │
├─────────┼──────────┼────────────────┤
│ 1       │ danielj  │ b3tTerpa$$w0rd │
│ 2       │ django   │ w0ff           │
│ 3       │ alecg    │ c0de           │
└─────────┴──────────┴────────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("users-database.db")
sql = con.cursor()

# We'll use this twice, so it makes sense to be a function
def display_all_users():
    query = """
        SELECT * FROM users;
    """

    result = sql.execute(query)
    rows = result.fetchall()

    print(rows)


display_all_users()

query = """
    UPDATE users
    SET
        username = "danielj",
        password = "b3tTerpa$$w0rd"
    WHERE user_id = 1;
"""

sql.execute(query)

# Make sure to commit the changes to the DB
con.commit()

display_all_users()
```

**Output**

```text
[(1, 'djs', 'mypa$$word'), (2, 'django', 'w0ff'), (3, 'alecg', 'c0de')]
[(1, 'danielj', 'b3tTerpa$$w0rd'), (2, 'django', 'w0ff'), (3, 'alecg', 'c0de')]
```

**Further Reading**

-   [SQLBolt - Updating rows](https://sqlbolt.com/lesson/updating_rows)
-   [SQLite Tutorial - SQLite Update](https://www.sqlitetutorial.net/sqlite-update/)

## WHERE

To filter the results from a SQL query, use the `WHERE` clause.

**Raw SQL**

```sql
SELECT * FROM users;
┌─────────┬──────────┬────────────┐
│ user_id │ username │  password  │
├─────────┼──────────┼────────────┤
│ 1       │ djs      │ mypa$$word │
│ 2       │ django   │ w0ff       │
│ 3       │ alecg    │ c0de       │
└─────────┴──────────┴────────────┘


SELECT * FROM users WHERE username = "djs";
┌─────────┬──────────┬────────────┐
│ user_id │ username │  password  │
├─────────┼──────────┼────────────┤
│ 1       │ djs      │ mypa$$word │
└─────────┴──────────┴────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("users-database.db")
sql = con.cursor()

def run_query_and_display_results(query):
    result = sql.execute(query)
    rows = result.fetchall()

    print(rows)


query = """
    SELECT * FROM users;
"""

run_query_and_display_results(query)

query = """
    SELECT * FROM users WHERE username = "djs";
"""

run_query_and_display_results(query)
```

**Output**

```text
[(1, 'djs', 'mypa$$word'), (2, 'django', 'w0ff'), (3, 'alecg', 'c0de')]
[(1, 'djs', 'mypa$$word')]
```

#### Getting a single row from Python when using `WHERE`

If you only need a single row from a `SELECT` statement using a `WHERE` clause in your Python programs, use `fetchone()`. This returns a `tuple` of the data in each column, and you can use techniques like tuple unpacking or indexing to pull the individual values from the `tuple`.

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("users-database.db")
sql = con.cursor()

query = """
    SELECT * FROM users WHERE username = "djs";
"""

result = sql.execute(query)
row = result.fetchone()

# This will be a tuple
print(row)

# Getting the values from the row with tuple unpacking
user_id, username, password = row

print(f"User ID: {user_id}")
print(f"Username: {username}")
print(f"Password: {password}")
```

**Output**

```text
(1, 'djs', 'mypa$$word')
User ID: 1
Username: djs
Password: mypa$$word
```

#### Using conditional logic with `WHERE` clauses

There are many operators available to use in a `WHERE` clause. The ones that you can use with numerical data are shown below (`=`, `IN`, and `NOT IN` can also be used with `TEXT` data):

| Operator          | Description                           |
| ----------------- | ------------------------------------- |
| =                 | Equality (works for numbers and TEXT) |
| >                 | Greater-than                          |
| <                 | Less-than                             |
| >=                | Greater-than or equal-to              |
| <=                | Less-than or equal-to                 |
| BETWEEN...AND     | Number is between two values          |
| NOT BETWEEN...AND | Number is not between two values      |
| IN (...)          | Number/Text exists in a list          |
| NOT IN (...)      | Number/Text does not exist in a list  |

Here are examples of a few of the operators on a table of `products`:

**Raw SQL**

```sql
SELECT * FROM products;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

-- Get the product where the `product_name` is "Lenovo ThinkPad".
SELECT * FROM products WHERE product_name = "Lenovo ThinkPad";
┌────────────┬─────────────────┬───────────────┬──────────────────┐
│ product_id │  product_name   │ product_price │ product_category │
├────────────┼─────────────────┼───────────────┼──────────────────┤
│ 8          │ Lenovo ThinkPad │ 950.75        │ Computers        │
└────────────┴─────────────────┴───────────────┴──────────────────┘

-- Get the products that cost less than $1000.
SELECT * FROM products WHERE product_price < 1000;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

-- Get the products that cost more than $1000.
SELECT * FROM products WHERE product_price > 1000;
┌────────────┬────────────────────┬───────────────┬──────────────────┐
│ product_id │    product_name    │ product_price │ product_category │
├────────────┼────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17        │ 1599.99       │ Computers        │
│ 3          │ System76 Thelio B1 │ 1255.55       │ Computers        │
│ 6          │ MacBook Pro 16     │ 2100.5        │ Computers        │
└────────────┴────────────────────┴───────────────┴──────────────────┘

-- Get the products whose prices are between $50 and $300 (inclusive).
SELECT * FROM products WHERE product_price BETWEEN 50 AND 300;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

-- Get the products that are in the "Microphones" and "Computers" categories.
SELECT * FROM products WHERE product_category IN ("Microphones", "Computers");
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘
```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("products-database.db")
sql = con.cursor()

# We'll use this a few times so it makes sense for it to be a function
def fetch_and_display_all_rows(query):
    result = sql.execute(query)
    rows = result.fetchall()

    for row in rows:
        print(row)


query = """
    SELECT * FROM products;
"""

fetch_and_display_all_rows(query)

query = """
    SELECT * FROM products WHERE product_name = "Lenovo ThinkPad";
"""

print("\nLooking for the 'Lenovo ThinkPad':")
fetch_and_display_all_rows(query)

query = """
    SELECT * FROM products WHERE product_price < 1000;
"""

print("\nProducts cheaper than $1000:")
fetch_and_display_all_rows(query)

query = """
    SELECT * FROM products WHERE product_price > 1000;
"""

print("\nProducts more expensive than $1000:")
fetch_and_display_all_rows(query)

query = """
    SELECT * FROM products WHERE product_price BETWEEN 50 AND 300;
"""

print("\nProducts between $50 and $300 (inclusive):")
fetch_and_display_all_rows(query)

query = """
    SELECT * FROM products WHERE product_category IN ("Microphones", "Computers");
"""

print("\nProducts in the 'Microphones' and 'Computers' categories:")
fetch_and_display_all_rows(query)
```

**Output**

```text
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(6, 'MacBook Pro 16', 2100.5, 'Computers')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')

Looking for the 'Lenovo ThinkPad':
(8, 'Lenovo ThinkPad', 950.75, 'Computers')

Products cheaper than $1000:
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')

Products more expensive than $1000:
(1, 'Dell XPS 17', 1599.99, 'Computers')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(6, 'MacBook Pro 16', 2100.5, 'Computers')

Products between $50 and $300 (inclusive):
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(7, 'Rode Z28', 275.99, 'Microphones')

Products in the 'Microphones' and 'Computers' categories:
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(6, 'MacBook Pro 16', 2100.5, 'Computers')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')
```

#### Complex conditional logic with `WHERE` clauses

You can join multiple `WHERE` clauses with the logical `AND` and `OR` operators to make complex conditional statements, just like in a programming language like Python or JavaScript.

**Raw SQL**

```sql
SELECT * FROM products;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 1          │ Dell XPS 17              │ 1599.99       │ Computers        │
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 3          │ System76 Thelio B1       │ 1255.55       │ Computers        │
│ 4          │ Logitech M1              │ 34.99         │ Accessories      │
│ 5          │ Seagate S1 SSD           │ 88.75         │ Accessories      │
│ 6          │ MacBook Pro 16           │ 2100.5        │ Computers        │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

-- Get all microphones less than $200.
SELECT * FROM products
WHERE product_category = "Microphones" AND product_price < 200;
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

-- Get any microphones or computers less than $1000.
SELECT * FROM products
WHERE product_price < 1000 AND product_category IN ("Computers", "Microphones");
┌────────────┬──────────────────────────┬───────────────┬──────────────────┐
│ product_id │       product_name       │ product_price │ product_category │
├────────────┼──────────────────────────┼───────────────┼──────────────────┤
│ 2          │ Blue Snowball Microphone │ 99.5          │ Microphones      │
│ 7          │ Rode Z28                 │ 275.99        │ Microphones      │
│ 8          │ Lenovo ThinkPad          │ 950.75        │ Computers        │
└────────────┴──────────────────────────┴───────────────┴──────────────────┘

```

**Python + SQL**

```python
import sqlite3

con = sqlite3.connect("products-database.db")
sql = con.cursor()

# We'll use this a few times so it makes sense for it to be a function
def fetch_and_display_all_rows(query):
    result = sql.execute(query)
    rows = result.fetchall()

    for row in rows:
        print(row)


query = """
    SELECT * FROM products;
"""

fetch_and_display_all_rows(query)

query = """
    SELECT * FROM products
    WHERE product_category = "Microphones" AND product_price < 200;
"""

print("\nGetting microphones less than $200:")
fetch_and_display_all_rows(query)

query = """
    SELECT * FROM products
    WHERE product_price < 1000 AND product_category IN ("Computers", "Microphones");
"""

print("\nComputers and Microphones cheaper than $1000:")
fetch_and_display_all_rows(query)
```

**Output**

```text
(1, 'Dell XPS 17', 1599.99, 'Computers')
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(3, 'System76 Thelio B1', 1255.55, 'Computers')
(4, 'Logitech M1', 34.99, 'Accessories')
(5, 'Seagate S1 SSD', 88.75, 'Accessories')
(6, 'MacBook Pro 16', 2100.5, 'Computers')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')

Getting microphones less than $200:
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')

Computers and Microphones cheaper than $1000:
(2, 'Blue Snowball Microphone', 99.5, 'Microphones')
(7, 'Rode Z28', 275.99, 'Microphones')
(8, 'Lenovo ThinkPad', 950.75, 'Computers')
```

**Further Reading**

-   [SQLBolt - Queries with constraints - Pt. 1](https://sqlbolt.com/lesson/select_queries_with_constraints)
-   [SQLBolt - Queries with constraints - Pt. 2](https://sqlbolt.com/lesson/select_queries_with_constraints_pt_2)
-   [SQLite Tutorial - SQLite Where](https://www.sqlitetutorial.net/sqlite-where/)
