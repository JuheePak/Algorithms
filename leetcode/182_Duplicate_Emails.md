### 182. Duplicate Emails

---

Write a SQL query to find all duplicate emails in a table named `Person`.

``` mysql
+----+---------+
| Id | Email   |
+----+---------+
| 1  | a@b.com |
| 2  | c@d.com |
| 3  | a@b.com |
+----+---------+
```

For example, your query should return the following for the above table:

```mysql
+---------+
| Email   |
+---------+
| a@b.com |
+---------+
```

A. 

``` mysql
# Write your MySQL query statement below
SELECT Email
FROM Person
GROUP BY Email
HAVING COUNT(Email)>1;
```

