# Problem Description

Write a solution to report the **first name**, **last name**, **city**, and **state** of each person in the `Person` table. If the address of a `personId` is not present in the `Address` table, report `null` instead.

### Database Schema

#### `Person` Table
| personId | lastName | firstName |
| :--- | :--- | :--- |
| 1 | Wang | Allen |
| 2 | Alice | Bob |

#### `Address` Table
| addressId | personId | city | state |
| :--- | :--- | :--- | :--- |
| 1 | 2 | New York City | New York |
| 2 | 3 | Leetcode | California |

### Expected Output
| firstName | lastName | city | state |
| :--- | :--- | :--- | :--- |
| Allen | Wang | *Null* | *Null* |
| Bob | Alice | New York City | New York |

---

## Solution

A `LEFT JOIN` is used here to ensure that all records from the `Person` table are included in the result, even if there is no matching `personId` in the `Address` table.

```sql
SELECT 
    p.firstName, 
    p.lastName, 
    a.city, 
    a.state 
FROM Person p
LEFT JOIN Address a
    ON p.personId = a.personId;