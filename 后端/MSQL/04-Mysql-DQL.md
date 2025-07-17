# 04-Mysql-DQL

## 1. 基本查询

### 1.1. 查询所有列

```sql
SELECT * FROM 表名;
```

- **解释**：查询表中所有列的数据。

#### 1.1.1. 示例

```sql
SELECT * FROM users;
```

### 1.2. 查询指定列

```sql
SELECT 列名1, 列名2 FROM 表名;
```

- **解释**：查询表中指定列的数据。

#### 1.2.1. 示例

```sql
SELECT username, email FROM users;
```

### 1.3. 查询时使用别名

```sql
SELECT 列名 AS 别名 FROM 表名;
```

- **解释**：为查询结果的列设置别名。

#### 1.3.1. 示例

```sql
SELECT username AS name, email AS user_email FROM users;
```

---

## 2. 条件查询

### 2.1. 使用 `WHERE` 子句

```sql
SELECT 列名 FROM 表名 WHERE 条件;
```

- **解释**：根据条件筛选数据。

#### 2.1.1. 示例

```sql
SELECT * FROM users WHERE age > 18;
```

### 2.2. 比较运算符

- `=`：等于
- `!=` 或 `<>`：不等于
- `>`：大于
- `<`：小于
- `>=`：大于等于
- `<=`：小于等于

#### 2.2.1. 示例

```sql
SELECT * FROM users WHERE age >= 20 AND age <= 30;
```

### 2.3. 逻辑运算符

- `AND`：与
- `OR`：或
- `NOT`：非

#### 2.3.1. 示例

```sql
SELECT * FROM users WHERE age > 18 AND status = 'active';
```

### 2.4. 模糊查询 (`LIKE`)

```sql
SELECT 列名 FROM 表名 WHERE 列名 LIKE '模式';
```

- **解释**：使用通配符 `%`（任意字符）和 `_`（单个字符）进行模糊查询。

#### 2.4.1. 示例

```sql
SELECT * FROM users WHERE username LIKE 'j%'; -- 查询以 'j' 开头的用户名
SELECT * FROM users WHERE email LIKE '%@gmail.com'; -- 查询 Gmail 邮箱
```

### 2.5. 范围查询 (`BETWEEN`)

```sql
SELECT 列名 FROM 表名 WHERE 列名 BETWEEN 值1 AND 值2;
```

- **解释**：查询某列值在指定范围内的数据。

#### 2.5.1. 示例

```sql
SELECT * FROM users WHERE age BETWEEN 18 AND 25;
```

### 2.6. 集合查询 (`IN`)

```sql
SELECT 列名 FROM 表名 WHERE 列名 IN (值1, 值2, ...);
```

- **解释**：查询某列值在指定集合中的数据。

#### 2.6.1. 示例

```sql
SELECT * FROM users WHERE id IN (1, 2, 3);
```

---

## 3. 排序查询

### 3.1. 使用 `ORDER BY` 子句

```sql
SELECT 列名 FROM 表名 ORDER BY 列名 [ASC|DESC];
```

- **解释**：按某列的值排序，`ASC` 为升序（默认），`DESC` 为降序。

#### 3.1.1. 示例

```sql
SELECT * FROM users ORDER BY age DESC; -- 按年龄降序排列
SELECT * FROM users ORDER BY created_at ASC; -- 按创建时间升序排列
```

### 3.2. 多列排序

```sql
SELECT 列名 FROM 表名 ORDER BY 列名1 [ASC|DESC], 列名2 [ASC|DESC];
```

- **解释**：先按列名 1 排序，再按列名 2 排序。

#### 3.2.1. 示例

```sql
SELECT * FROM users ORDER BY age DESC, username ASC;
```

---

## 4. 分组查询

### 4.1. 使用 `GROUP BY` 子句

```sql
SELECT 列名, 聚合函数 FROM 表名 GROUP BY 列名;
```

- **解释**：按某列的值分组，通常与聚合函数一起使用。

#### 4.1.1. 示例

```sql
SELECT age, COUNT(*) FROM users GROUP BY age; -- 按年龄分组并统计每组的数量
```

### 4.2. 聚合函数

- `COUNT()`：统计行数
- `SUM()`：求和
- `AVG()`：求平均值
- `MAX()`：求最大值
- `MIN()`：求最小值

#### 4.2.1. 示例

```sql
SELECT age, AVG(salary) FROM users GROUP BY age; -- 按年龄分组并计算每组的平均工资
```

### 4.3. 使用 `HAVING` 子句

```sql
SELECT 列名, 聚合函数 FROM 表名 GROUP BY 列名 HAVING 条件;
```

- **解释**：对分组后的结果进行筛选。

#### 4.3.1. 示例

```sql
SELECT age, COUNT(*) FROM users GROUP BY age HAVING COUNT(*) > 10; -- 查询数量大于 10 的年龄组
```

---

## 5. 分页查询

### 5.1. 使用 `LIMIT` 子句

```sql
SELECT 列名 FROM 表名 LIMIT 数量;
```

- **解释**：限制查询结果的数量。

#### 5.1.1. 示例

```sql
SELECT * FROM users LIMIT 10; -- 查询前 10 条数据
```

### 5.2. 使用 `LIMIT` 和 `OFFSET`

```sql
SELECT 列名 FROM 表名 LIMIT 数量 OFFSET 偏移量;
```

- **解释**：从指定偏移量开始查询指定数量的数据。

#### 5.2.1. 示例

```sql
SELECT * FROM users LIMIT 10 OFFSET 20; -- 查询第 21 到 30 条数据
```

---

## 6. 连接查询

### 6.1. 内连接 (`INNER JOIN`)

```sql
SELECT 列名 FROM 表1 INNER JOIN 表2 ON 表1.列名 = 表2.列名;
```

- **解释**：查询两个表中满足条件的交集数据。

#### 6.1.1. 示例

```sql
SELECT users.username, orders.order_id 
FROM users 
INNER JOIN orders ON users.id = orders.user_id;
```

### 6.2. 左连接 (`LEFT JOIN`)

```sql
SELECT 列名 FROM 表1 LEFT JOIN 表2 ON 表1.列名 = 表2.列名;
```

- **解释**：查询左表的所有数据，以及右表中满足条件的数据（不满足条件的右表数据为 `NULL`）。

#### 6.2.1. 示例

```sql
SELECT users.username, orders.order_id 
FROM users 
LEFT JOIN orders ON users.id = orders.user_id;
```

### 6.3. 右连接 (`RIGHT JOIN`)

```sql
SELECT 列名 FROM 表1 RIGHT JOIN 表2 ON 表1.列名 = 表2.列名;
```

- **解释**：查询右表的所有数据，以及左表中满足条件的数据（不满足条件的左表数据为 `NULL`）。

#### 6.3.1. 示例

```sql
SELECT users.username, orders.order_id 
FROM users 
RIGHT JOIN orders ON users.id = orders.user_id;
```

---

## 7. 子查询

### 7.1. 子查询作为条件

```sql
SELECT 列名 FROM 表名 WHERE 列名 = (SELECT 列名 FROM 表名 WHERE 条件);
```

- **解释**：将一个查询的结果作为另一个查询的条件。

#### 7.1.1. 示例

```sql
SELECT * FROM users WHERE age = (SELECT MAX(age) FROM users); -- 查询年龄最大的用户
```

### 7.2. 子查询作为表

```sql
SELECT 列名 FROM (SELECT 列名 FROM 表名 WHERE 条件) AS 别名;
```

- **解释**：将一个查询的结果作为临时表。

#### 7.2.1. 示例

```sql
SELECT * FROM (SELECT * FROM users WHERE age > 18) AS adult_users;
```

---
