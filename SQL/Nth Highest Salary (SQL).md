# LeetCode 177: Nth Highest Salary

## 📌 Problem Description

**Difficulty:** Medium  
**Topic:** SQL (Window Functions / CTEs)

### Table: Employee
| Column Name | Type |
| :--- | :--- |
| id | int |
| salary | int |

`id` is the primary key for this table. Each row contains information about the salary of an employee.

Write a solution to find the $n^{\text{th}}$ highest distinct salary from the `Employee` table. If there are fewer than $n$ distinct salaries, return `null`.

## 🛠️ My Solution

```sql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  RETURN (
      WITH ranked_salary AS (
          SELECT 
              salary, 
              DENSE_RANK() OVER (ORDER BY salary DESC) AS pos 
          FROM Employee
      )
      SELECT MAX(salary) 
      FROM ranked_salary
      WHERE pos = N
  );
END