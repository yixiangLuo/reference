https://www.w3school.com.cn/sql/index.asp
## Basics

### operations
1. select: `SELECT column FROM table`
3. delete: `DELETE FROM table WHERE column = value`
4. insert: `INSERT INTO table (col1, col2) VALUES (val1, val2)`
5. update: `UPDATE table SET column = value WHERE col = val`

### conditioning
1. `AND`, `OR`, `NOT condition`, used with `()`
2. equal `=`     not equal `<>`    lt `<`    leq `<=`
3. `col BETWEEN num1 AND num2` is equal to `col >= num1 AND col <= num2`
4. `col IN (val1, val2)`
5. text pattern searching: `col LIKE _pattern%`   
    - `_` wildcard for one char
    - `%` wildcard for 0+ chars
    - `[abc]` any one of a b c
    - `[!abc]` any one except a b c
6. `NULL` value must be checked by `IS NULL` and `IS NOT NULL`
7. `WHERE` should be used before `GROUP BY` without aggregate functions;
   `HAVING` should be used after `GROUP BY` with aggregate functions. e.g.
   `SELECT * FROM table WHERE col > 0 GROUP BY c HAVING count(*) > 5`

### prefix
1. `TOP`
  - `SELECT TOP 2 * FROM table`
  - `SELECT TOP 50 PERCENT * FROM table`
2. distinct: `SELECT DISTINCT column FROM table`

### table manipulate
1. order `SELECT col1, col2 FROM table ORDER BY col1 DESC, col2 ASC`
2. Join
```
SELECT table1.col1, table2.col2
FROM
(table1 INNER/LEFT/RIGHT/FULL JOIN table2)
ON table1.col=table2.col
```
4. `UNION ALL` union rows, `UNION` union rows and unique
   `SELECT * FROM table1 UNION (ALL) SELECT * FROM table2
6. `GROUP`: aggregate functions apply to each group; selected columns must either be a group key or a aggregated result
   `SELECT col1, SUM(col2) FROM table GROUP BY col1
8. alias
  - table `SELECT * FROM table AS alias`; every derived table must have its alias
  - column `SELECT col AS alias FROM table`
  - cannot use the alias name in the table where it is defined: cannot do 
    `SELECT count(*) AS c FROM table WHERE c > 5`, should do
    ``SELECT count(*) AS c FROM table WHERE count(*) > 5``
### functions
1. aggregate functions: `AVG` `COUNT` `MAX` `MIN` `SUM` `FIRST` `LAST` 
   `SELECT FUN(column) FROM table GROUP BY col`
2. elementwise functions
   - string: `UCASE` `LCASE` `LEN` `MID(col, start[, length])` get substring
   - number: `ROUND` arithmetic operations `(col1+col2)*col3`
   - `ISNULL(col, default)`
3. datetime  `FORMAT` `NOW`    `FORMAT(Now(),'YYYY-MM-DD')`

## Advanced

1. `WITH AS` gives a sub-query block a name, which can be referenced in several places within the main SQL query.
```
WITH query_name AS [sql_subquery_statement]
[do things]
```
2. Use [Jinja template](https://docs.getdbt.com/guides/using-jinja)

## Examples
1. [570. Managers with at Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/)
2. 


