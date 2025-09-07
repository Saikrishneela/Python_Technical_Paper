
# SQL Joins: A Technical Overview

## Introduction
Joins in SQL are used to combine rows from two or more tables based on a related column. They are fundamental for relational database queries and allow us to retrieve meaningful results from normalized data structures.

This paper explores the main types of joins: **INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL JOIN (also called FULLER JOIN), and CROSS JOIN**.

---

## 1. INNER JOIN
An **INNER JOIN** returns only the rows where there is a match in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

**Example:**
Retrieve customers who have placed an order:
```sql
SELECT Customers.CustomerID, Customers.Name, Orders.OrderID
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

---

## 2. LEFT JOIN
A **LEFT JOIN** returns all rows from the left table and the matching rows from the right table. If no match exists, NULL is returned for columns from the right table.

**Syntax:**
```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```

**Example:**
Retrieve all customers and their orders, including those with no orders:
```sql
SELECT Customers.CustomerID, Customers.Name, Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

---

## 3. RIGHT JOIN
A **RIGHT JOIN** returns all rows from the right table and the matching rows from the left table. If no match exists, NULL is returned for columns from the left table.

**Syntax:**
```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```

**Example:**
Retrieve all orders and their associated customers, even if some orders don’t have matching customer data:
```sql
SELECT Customers.CustomerID, Customers.Name, Orders.OrderID
FROM Customers
RIGHT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

---

## 4. FULL JOIN / FULLER JOIN
A **FULL JOIN** (also called **FULL OUTER JOIN** or informally referred to as **FULLER JOIN**) returns all rows when there is a match in either table. Rows without a match are filled with NULLs.

**Syntax:**
```sql
SELECT columns
FROM table1
FULL JOIN table2
ON table1.column = table2.column;
```

**Example:**
Retrieve all customers and all orders, showing NULLs where no match exists:
```sql
SELECT Customers.CustomerID, Customers.Name, Orders.OrderID
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

**Note:** Some databases may not support `FULL JOIN` directly (e.g., MySQL). In such cases, it can be simulated using a combination of `LEFT JOIN` and `RIGHT JOIN` with `UNION`.

---

## 5. CROSS JOIN
A **CROSS JOIN** returns the Cartesian product of both tables, combining every row from the first table with every row from the second.

**Syntax:**
```sql
SELECT columns
FROM table1
CROSS JOIN table2;
```

**Example:**
Generate all possible customer–order pairs:
```sql
SELECT Customers.CustomerID, Orders.OrderID
FROM Customers
CROSS JOIN Orders;
```


## Conclusion
- **INNER JOIN** → only matching rows.  
- **LEFT JOIN** → all left rows + matches.  
- **RIGHT JOIN** → all right rows + matches.  
- **FULL JOIN / FULLER JOIN** → all rows from both sides.  
- **CROSS JOIN** → Cartesian product.

Understanding these concepts is crucial for effective SQL querying in relational databases.



🔸 Key Differences Between Joins

-Join Type	What It Returns.

-INNER JOIN	Only rows with matching values in both tables.

-LEFT JOIN	All rows from left table + matches from right (NULL if no match).

-RIGHT JOIN	All rows from right table + matches from left (NULL if no match).

-FULL OUTER JOIN	All rows from both tables (NULLs where no match).

-SELF JOIN	A table joined with itself, often used for hierarchy or comparison within same table.

-CROSS JOIN	Cartesian product (all possible combinations).