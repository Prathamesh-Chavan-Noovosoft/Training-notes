# PostgreSQL basics

## Basic commands

### SELECT

One of the most common tasks, when you work with the database, is to retrieve data from tables
using the SELECT statement.

The SELECT statement is one of the most complex statements in PostgreSQL.
It has many clauses that you can use to form a flexible query.

Due to its complexity, we will break it down into many shorter and easy-to-understand tutorials so
that you can learn about each clause faster.

The SELECT statement has the following clauses:

- Select distinct rows using DISTINCT operator.
- Sort rows using ORDER BY clause.
- Filter rows using WHERE clause.
- Select a subset of rows from a table using LIMIT or FETCH clause.
- Group rows into groups using GROUP BY clause.
- Filter groups using HAVING clause.
- Join with other tables using joins such as INNER JOIN, LEFT JOIN, FULL OUTER JOIN, CROSS JOIN clauses.
- Perform set operations using UNION, INTERSECT, and EXCEPT.

### Syntax

```PostgreSQL
SELECT
   select_list
FROM
   table_name;
```

In this syntax:

First, specify a select list that can be a column or a list of columns in a table from
which you want to retrieve data. If you specify a list of columns,
you need to place a comma (,) between two columns to separate them.
If you want to select data from all the columns of the table, you can use an asterisk (\*) shorthand instead of specifying all the column names. The select list may also contain expressions or literal values.

Second, provide the name of the table from which you want to query data after the FROM keyword.
The FROM clause is optional. If you are not querying data from any table, you can omit the FROM
clause in the SELECT statement.

PostgreSQL evaluates the FROM clause before the SELECT clause in the SELECT statement:
