### LeetCode 176: Second Highest Salary

#### Problem Description

**Table:** `Employee`

| Column Name | Type |
| :--- | :--- |
| `id` | int |
| `salary` | int |

* `id` is the primary key (column with unique values) for this table.
* Each row of this table contains information about the salary of an employee.

Write a solution to find the second highest distinct salary from the `Employee` table. If there is no second highest salary, return `null` (or `None` in Pandas).

---

#### Solution (SQL)

```sql
WITH ranked_salary AS (
    SELECT 
        salary, 
        DENSE_RANK() OVER (ORDER BY salary DESC) AS pos
    FROM 
        Employee
)
SELECT 
    MAX(salary) AS SecondHighestSalary 
FROM 
    ranked_salary
WHERE 
    pos = 2;
