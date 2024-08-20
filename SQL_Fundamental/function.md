Joins : combines data from two tables.

---

1. LEFT JOIN : LEFT JOIN returns all rows from the left table with matching rows from the right table. Rows without a match are filled
   with NULLs. LEFT JOIN is also called LEFT OUTER JOIN.
2. RIGHT JOIN: RIGHT JOIN returns all rows from the right table with matching rows from the left table. Rows without a match are
   filled with NULLs. RIGHT JOIN is also called RIGHT OUTER JOIN.
3. FULL JOIN: FULL JOIN returns all rows from the left table and all rows from the right table. It fills the non-matching rows with
   NULLs. FULL JOIN is also called FULL OUTER JOIN.
4. CROSS JOIN: CROSS JOIN returns all possible combinations of rows from the left and right tables.cartesian product of the two tables included in the join.
5. SELF JOIN: You can join a table to itself.
6. NATURAL JOIN: If the tables have columns with the same name, you can use NATURAL JOIN instead of JOIN.

Difference:

| **INNER JOIN**                                    | **LEFT JOIN**                                                                          | **RIGHT JOIN**                                                                        | **FULL JOIN**                                            | **SELF JOIN**                                                                                                                    | CARTESIAN JOIN                                                                                      |
| ------------------------------------------------------- | -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| returns rows when there<br />is a match in both tables. | returns all rows from the left table, even<br /> if there are no matches in the right table. | returns all rows from the right table,<br />even if there are no matches in the left table. | combines the results of both<br /> left and right outer joins. | joins a table to itself as<br />if the table were two tables,<br />temporarily renaming at least <br />one table in the SQL statement. | returns the Cartesian product of the<br />sets of records from the two or more<br /> joined tables. |

---

SUBQUERIES: A subquery is a query that is nested inside another query, or inside another subquery. There are different types of subqueries.

* SINGLE VALUE: The simplest subquery returns exactly one column and exactly one row. It can be used with comparison operators =, <, <=, >, or >=. Appear in SELECT statements, clause like where and having or from.

  ```sql
  SELECT name FROM city
  WHERE rating = (
  SELECT rating
  FROM city
  WHERE name = 'Paris'
  ```
* MULTIPLE VALUES: A subquery can also return multiple columns or multiple rows. Such subqueries can be used with operators IN, EXISTS, ALL, or ANY.Appear in SELECT statements, clause like where and having or from.

  ```sql
  SELECT name
  FROM city
  WHERE country_id IN (
  SELECT country_id
  FROM country
  WHERE population > 20000000
  );
  ```
* CORRELATED: A correlated subquery refers to the tables introduced in the outer query. A correlated subquery depends on the outer query. It cannot be run independently from the outer query.

  ```sql
  SELECT *
  FROM city main_city
  WHERE population > (
  SELECT AVG(population)
  FROM city average_city
  WHERE average_city.country_id = main_city.country_id
  );
  ```

Key differences

* Execution: Non-correlated runs once, correlated runs for each row in the outer query.
* Dependency: Non-correlated is independent, correlated needs data from the outer query.
* Performance: Non-correlated can be faster due to fewer executions.
* Complexity: Correlated queries can be more complex and harder to read.

**Best Practices:**

* Prefer non-correlated subqueries whenever possible: If the required information can be obtained independently of the outer query, use a non-correlated subquery for potential performance benefits.
* Optimize correlated subqueries carefully: If correlated subqueries are necessary, consider techniques like using indexes and optimizing the subquery logic to minimize execution time.
* Test and measure: Always test and measure the performance of different query approaches with your specific data and workload to determine the most efficient solution for your use case.

---

Window Functions: SQL function where the input values are taken from a "window" of one or more rows in the results set of a SELECT statement.

AGGREGATE FUNCTIONS VS. WINDOW FUNCTIONS: unlike aggregate functions, window functions do not collapse rows.

PARTITION BY: divides rows into multiple groups, called partitions, to which the window function is applied.

1. Aggregate Functions
   * avg() - average value for rows within the window frame
   * count() - count of values for rows within the window frame
   * max() - maximum value within the window frame
   * min() - minimum value within the window frame
   * sum() - sum of values within the window frame
2. Ranking Functions
   * row_number() - unique number for each row within partition, with different numbers for tied values (give unique value for duplicates values also)
   * rank() - ranking within partition, with gaps and same ranking for tied values - (give samevalue for duplicates values and skip next digits)
   * dense_rank() - ranking within partition, with no gaps and same ranking for tied values - (give samevalue for duplicates values and not skip digits)
3. Distribution Functions
   * percent_rank() - he percentile ranking number of a row—a value in [0, 1] interval: (rank - 1) / (total number of rows - 1)
   * cume_dist()  - the cumulative distribution of a value within a group of values, i.e., the number of rows with values less than or equal to the current row’s value divided by the total number of rows; a value in (0, 1] interval
4. Analytic Functions
   * lead(expr, offset, default)
   * lag(expr, offset, default)
   * ntile(n) - divide rows within a partition as equally as possible into n groups, and assign each row its group number.
   * first_value(expr) - the value for the first row within the window frame
   * last_value(expr) - the value for the last row within the window frame
   * nth_value(expr,n) - the value for the n-th row within the window frame; n must be an integer

---

CTE: SQL CTEs or Common Table Expressions are nothing but temporary tables that you can use within a query.They can be referenced within a SELECT, INSERT, UPDATE, or DELETE statement.

Recursive CTEs: CTEs can be used for recursive queries, which are queries that refer to themselves to generate a result. For example, you can use a recursive CTE to generate a list of numbers or dates.

```sql
WITH recursive numbers (n) AS (
    SELECT 1
    UNION ALL
    SELECT n + 1
    FROM numbers
    WHERE n < 10
)
SELECT n
FROM numbers;
```

When to Use:

* CTE can help you to avoid repeated sub queries.
* A CTE can be used multiple times within your statement, e.g. within a `JOIN` with a dynamic behavior depending on the actual row-count.
* You can use multiple CTEs within one statement and you can use the result of one CTE within a later CTE.
* There are recursive (or better  *iterative* ) CTEs.

Advantages:

* useable in  *ad-hoc* -queries (functions, views)
* no unexpected side effects (most narrow scope)

Disadvantages:

* You cannot use the CTE's result in different statements
* You cannot use indexes, statistics to optimize your CTE's set (although it will implicitly use existing indexes and statistics of the targeted objects - if appropriate).

difference between Subquery and CTE:

* **CTE can be reusable:** One advantage of using CTE is CTE is reusable by design. Instead of having to declare the same subquery in every place you need to use it, you can use CTE to define a temporary table once, then refer to it whenever you need it.
* **CTE can be more readable:** Another advantage of CTE is CTE is more readable than Subqueries. Since CTE can be reusable, you can write less code using CTE than using a subquery. Also, **people tend to follow logic and ideas easier in sequence than in a nested fashion. **When you write a query, it is easier to break down a complex query into smaller pieces using CTE.
* **CTEs can be recursive:** A CTE can run recursively, which a subquery cannot. This makes it especially well suited to tree structures, in which information in a given row is based on the information from the previous row(s). The recursion feature can be implemented with `RECURSIVE` and `UNION ALL`.
