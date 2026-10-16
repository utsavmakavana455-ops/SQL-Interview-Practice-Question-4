# SQL Interview Practice — Question 4

**Level:** Intermediate  
**Topic:** Date Filtering, Aggregation, GROUP BY

## Interview Question: Find Monthly Sales

### Real-World Scenario

You are a Data Analyst at an e-commerce company. Your manager wants to understand how sales are performing month by month.

Use your existing `sql_practice` database and `orders` table.

Assume the `orders` table contains:

- `order_id`
- `customer_name`
- `amount`
- `order_date`

### Your Task

Write a SQL query that displays:

1. The month
2. Total number of orders in that month
3. Total sales amount in that month
4. Average order value for that month

### Requirements

- Group the results by month.
- Round the average order value to **2 decimal places**.
- Sort the results chronologically, from the earliest month to the latest.

### Expected Output

| month | total_orders | total_sales | avg_order_value |
|---|---:|---:|---:|
| 2026-01 | 5 | 1250.00 | 250.00 |
| 2026-02 | 8 | 2100.00 | 262.50 |

## Solution — MySQL

```sql id="z3ps0v"
SELECT
    DATE_FORMAT(order_date, '%Y-%m') AS month,
    COUNT(*) AS total_orders,
    SUM(amount) AS total_sales,
    ROUND(AVG(amount), 2) AS avg_order_value
FROM orders
GROUP BY DATE_FORMAT(order_date, '%Y-%m')
ORDER BY month ASC;
```

## Interview Explanation

`DATE_FORMAT(order_date, '%Y-%m')` converts each order date into a year-month value such as `2026-01`.

`COUNT(*)` calculates the number of orders placed during each month.

`SUM(amount)` calculates the total revenue generated during each month.

`AVG(amount)` calculates the average order value, and `ROUND(..., 2)` limits it to two decimal places.

`GROUP BY` creates one result for each month.

Finally, `ORDER BY month ASC` displays the months from earliest to latest.

## Interview Follow-Up

An interviewer might now ask:

> "Modify your query to show only months where total sales were greater than 1,000."

Think about whether you would use **`WHERE` or `HAVING`** for this condition.
