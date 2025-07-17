# 03-MySQL-DDL

# MySQL DDL 操作笔记

## 1. 数据库操作

### 1.1. 创建数据库

```sql
CREATE DATABASE 数据库名;
```

- **解释**：创建一个新的数据库。

### 1.2. 删除数据库

```sql
DROP DATABASE 数据库名;
```

- **解释**：删除指定的数据库及其所有内容。

### 1.3. 选择数据库

```sql
USE 数据库名;
```

- **解释**：选择要操作的数据库。

---

## 2. 表操作

### 2.1. 创建表

```sql
CREATE TABLE 表名 (
    列名1 数据类型 [约束条件],
    列名2 数据类型 [约束条件],
    ...
);
```

- **解释**：创建一个新表，定义列名、数据类型及约束条件（如主键、非空等）。

#### 2.1.1. 示例

```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 2.2. 删除表

```sql
DROP TABLE 表名;
```

- **解释**：删除指定的表及其所有数据。

### 2.3. 清空表

```sql
TRUNCATE TABLE 表名;
```

- **解释**：清空表中的所有数据，但保留表结构。

### 2.4. 修改表结构

#### 2.4.1. 添加列

```sql
ALTER TABLE 表名 ADD 列名 数据类型 [约束条件];
```

- **解释**：向表中添加新列。

#### 2.4.2. 示例

```sql
ALTER TABLE users ADD age INT;
```

#### 2.4.3. 删除列

```sql
ALTER TABLE 表名 DROP COLUMN 列名;
```

- **解释**：删除表中的指定列。

#### 2.4.4. 示例

```sql
ALTER TABLE users DROP COLUMN age;
```

#### 2.4.5. 修改列数据类型

```sql
ALTER TABLE 表名 MODIFY 列名 新数据类型;
```

- **解释**：修改表中某列的数据类型。

#### 2.4.6. 示例

```sql
ALTER TABLE users MODIFY email VARCHAR(150);
```

#### 2.4.7. 重命名列

```sql
ALTER TABLE 表名 CHANGE 旧列名 新列名 数据类型;
```

- **解释**：重命名表中的列，并可以修改数据类型。

#### 2.4.8. 示例

```sql
ALTER TABLE users CHANGE email user_email VARCHAR(100);
```

#### 2.4.9. 重命名表

```sql
ALTER TABLE 旧表名 RENAME TO 新表名;
```

- **解释**：重命名表。

#### 2.4.10. 示例

```sql
ALTER TABLE users RENAME TO customers;
```

---

## 3. 索引操作

### 3.1. 创建索引

```sql
CREATE INDEX 索引名 ON 表名 (列名);
```

- **解释**：为表中的某列创建索引，提高查询效率。

#### 3.1.1. 示例

```sql
CREATE INDEX idx_username ON users (username);
```

### 3.2. 删除索引

```sql
DROP INDEX 索引名 ON 表名;
```

- **解释**：删除表中的指定索引。

#### 3.2.1. 示例

```sql
DROP INDEX idx_username ON users;
```

---

## 4. 约束操作

### 4.1. 添加主键

```sql
ALTER TABLE 表名 ADD PRIMARY KEY (列名);
```

- **解释**：将某列设置为主键。

#### 4.1.1. 示例

```sql
ALTER TABLE users ADD PRIMARY KEY (id);
```

### 4.2. 添加外键

```sql
ALTER TABLE 表名 ADD CONSTRAINT 外键名 FOREIGN KEY (列名) REFERENCES 另一表名 (列名);
```

- **解释**：为某列添加外键约束，关联另一张表的列。

#### 4.2.1. 示例

```sql
ALTER TABLE orders ADD CONSTRAINT fk_user_id FOREIGN KEY (user_id) REFERENCES users (id);
```

### 4.3. 删除约束

```sql
ALTER TABLE 表名 DROP CONSTRAINT 约束名;
```

- **解释**：删除表中的指定约束。

#### 4.3.1. 示例

```sql
ALTER TABLE orders DROP CONSTRAINT fk_user_id;
```

---

## 5. 视图操作

### 5.1. 创建视图

```sql
CREATE VIEW 视图名 AS SELECT 列名 FROM 表名 [WHERE 条件];
```

- **解释**：创建一个虚拟表（视图），基于查询结果。

#### 5.1.1. 示例

```sql
CREATE VIEW active_users AS SELECT username, email FROM users WHERE status = 'active';
```

### 5.2. 删除视图

```sql
DROP VIEW 视图名;
```

- **解释**：删除指定的视图。

#### 5.2.1. 示例

```sql
DROP VIEW active_users;
```

---
