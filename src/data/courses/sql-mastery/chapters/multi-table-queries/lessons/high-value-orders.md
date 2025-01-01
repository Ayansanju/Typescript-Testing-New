---
title: High Value Orders
description: Practice using EXCEPT to identify potential technical book opportunities
order: 110
type: challenge
setup: |
  ```sql
  CREATE TABLE customer (
      id INT PRIMARY KEY,
      name VARCHAR(255),
      email VARCHAR(255)
  );

  CREATE TABLE sale (
      id INT PRIMARY KEY,
      customer_id INT,
      order_date DATE,
      total_amount DECIMAL(10,2)
  );

  INSERT INTO customer (id, name, email)
  VALUES 
      (1, 'John Doe', 'john.doe@example.com'),
      (2, 'Jane Smith', 'jane.smith@example.com'),
      (3, 'Alice Johnson', 'alice.johnson@example.com'),
      (4, 'Bob Brown', 'bob.brown@example.com'),
      (5, 'Charlie Davis', 'charlie.davis@example.com'),
      (6, 'David Lee', 'david.lee@example.com');

  INSERT INTO sale (id, customer_id, order_date, total_amount)
  VALUES 
      (1, 1, '2024-12-02', 100.00),
      (2, 1, '2024-11-15', 150.00),
      (3, 1, '2024-10-20', 550.00),
      (4, 4, '2024-12-26', 250.00),
      (5, 5, '2024-11-12', 300.00),
      (6, 2, '2024-11-23', 300.00),
      (7, 2, '2024-11-11', 600.00);
  ```
---

The bookstore wants to identify the highest value orders i.e. the orders worth more than or equal to $500. Write a query to find order amounts, dates along with the customer names and emails.

We have the `customer` and `sale` tables.

> `customer` table has the list of customers.

| id  | name          | email                     |
| --- | ------------- | ------------------------- |
| 1   | John Doe      | john.doe@example.com      |
| 2   | Jane Smith    | jane.smith@example.com    |
| 3   | Alice Johnson | alice.johnson@example.com |
| 4   | Bob Brown     | bob.brown@example.com     |
| 5   | Charlie Davis | charlie.davis@example.com |
| 6   | David Lee     | david.lee@example.com     |

> `sale` table has the list of sales.

| id  | customer_id | order_date | total_amount |
| --- | ----------- | ---------- | ------------ |
| 1   | 1           | 2024-12-02 | 100.00       |
| 2   | 1           | 2024-11-15 | 150.00       |
| 3   | 1           | 2024-10-20 | 200.00       |
| 4   | 4           | 2024-12-26 | 250.00       |
| 5   | 5           | 2024-11-12 | 300.00       |
| 6   | 2           | 2024-11-23 | 300.00       |
| 7   | 2           | 2024-11-11 | 300.00       |

Write a query to find the orders above $500 along with the information of the customers. Your output should have the following columns:

- `customer_name`
- `customer_email`
- `order_amount`
- `order_date`

The output should be ordered by the `order_amount` in descending order.

## Expected Output

| customer_name | customer_email         | order_amount | order_date        |
| ------------- | ---------------------- | ------------ | ----------------- |
| Jane Smith    | jane.smith@example.com | 600.00       | November 11, 2024 |
| John Doe      | john.doe@example.com   | 550.00       | October 20, 2024  |

## Solution

```sql
SELECT
    c.name,
    c.email,
    s.total_amount,
    TO_CHAR(s.order_date, 'Month DD, YYYY') AS order_date
FROM customer c
JOIN sale s ON c.id = s.customer_id
WHERE s.total_amount >= 500
ORDER BY s.total_amount DESC;
```
