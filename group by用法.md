`GROUP BY`语句用于将数据表中的数据按照指定的列进行分组，以便对每个分组执行聚合函数，如求和、平均值、计数等。

用法示例：

假设我们有一个名为`orders`的表，包含以下字段：`id`（订单ID）、`customer_id`（客户ID）、`product_id`（产品ID）和`quantity`（数量）。

# 1.按客户ID分组，计算每个客户的订单总数：

```sql
SELECT customer_id, COUNT(id) as order_count
FROM orders
GROUP BY customer_id;
```

# 2.按产品ID分组，计算每个产品的销售总量：

```sql
SELECT product_id, SUM(quantity) as total_quantity
FROM orders
GROUP BY product_id;
```

# 3.按客户ID分组，计算每个客户的平均订单数量：

```sql
SELECT customer_id, AVG(quantity) as average_quantity
FROM orders
GROUP BY customer_id;
```

1. 注意：在使用`GROUP BY`时，`SELECT`语句中列出的非聚合列必须出现在`GROUP BY`子句中。