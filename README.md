# SQL Table Relations Lab: Joins and Subqueries

A lab on writing SQL queries that combine data from multiple tables, using the Northwind-style CRM database (customers, employees, offices, orders, products, payments). The queries run from a Jupyter notebook using `sqlite3` and `pandas`.

## Files

| File | Description |
|---|---|
| `SQLJoinsSubQueriesLab.ipynb` | The completed lab notebook (Steps 1-10) |
| `data.sqlite` | SQLite database used by the notebook |
| `ERD.png` | Entity relationship diagram of the database |

## Skills practiced

- `INNER JOIN` and `LEFT JOIN`, including joins across 3 to 5 tables
- Filtering with `WHERE` and with `HAVING` on aggregates
- `GROUP BY` with `COUNT`, `SUM`, `AVG` and `COUNT(DISTINCT ...)`
- `CAST` to fix a column stored with the wrong datatype
- Subqueries used inside a `WHERE ... IN (...)` clause

## How to run

1. Clone the repo and open a terminal in its folder.
2. Install the dependencies if needed: `pip install pandas jupyter`
3. Start Jupyter: `jupyter notebook`
4. Open `SQLJoinsSubQueriesLab.ipynb` and run all cells. `data.sqlite` must be in the same folder as the notebook.

## Summary of the queries

| Step | Question | Technique | Result |
|---|---|---|---|
| 1 | Names and job titles of Boston employees | `JOIN` + `WHERE` | 2 employees |
| 2 | Any offices with zero employees? | `LEFT JOIN` + `HAVING COUNT(...) = 0` | None |
| 3 | All employees with their office city and state | `LEFT JOIN` + `ORDER BY` | 23 employees |
| 4 | Customers who have never placed an order | `LEFT JOIN` + `IS NULL` | 24 customers |
| 5 | Customer contacts with payment amounts, largest first | `JOIN` + `CAST(amount AS REAL)` | 273 payments |
| 6 | Employees whose customers average over 90k credit limit | `GROUP BY` + `HAVING AVG(...)` | 4 employees |
| 7 | Orders and units sold per product | `GROUP BY` + `COUNT` / `SUM` | 109 products |
| 8 | Distinct customers per product | 3-table join + `COUNT(DISTINCT ...)` | 109 products |
| 9 | Customers per office | 3-table join + `GROUP BY` | 7 offices |
| 10 | Employees who sold products ordered by fewer than 20 customers | 5-table join + subquery in `WHERE` | 15 employees |

## Notes

- **Payment amounts are stored as text** in `payments.amount`. Sorting them directly gives an alphabetical order, so Step 5 casts them to `REAL` first.
- **Customers per office (Step 9)** are linked to an office through their sales rep, so customers without a sales rep are not counted in any office.
- **Step 10** uses `DISTINCT` so an employee who sold several low-performing products appears only once.
