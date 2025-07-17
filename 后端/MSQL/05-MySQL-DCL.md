# 05-MySQL-DCL

# MySQL DCL 常用操作总结

DCL（Data Control Language，数据控制语言）主要用于管理数据库的用户权限和事务控制。以下是 **常用** 的 DCL 操作及其命令和简单解释。

---

## 1. 用户管理

### 1.1. 创建用户

```sql
CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';
```

- **解释**：创建一个新用户，并设置密码。
- **示例**：
  ```sql
  CREATE USER 'john'@'localhost' IDENTIFIED BY 'password123';
  ```

### 1.2. 修改用户密码

```sql
ALTER USER '用户名'@'主机名' IDENTIFIED BY '新密码';
```

- **解释**：修改用户的密码。
- **示例**：
  ```sql
  ALTER USER 'john'@'localhost' IDENTIFIED BY 'newpassword123';
  ```

### 1.3. 删除用户

```sql
DROP USER '用户名'@'主机名';
```

- **解释**：删除指定用户。
- **示例**：
  ```sql
  DROP USER 'john'@'localhost';
  ```

### 1.4. 查看所有用户

```sql
SELECT user, host FROM mysql.user;
```

- **解释**：查看数据库中的所有用户及其主机信息。
- **示例**：
  ```sql
  SELECT user, host FROM mysql.user;
  ```

---

## 2. 权限管理

### 2.1. 授予权限

```sql
GRANT 权限 ON 数据库名.表名 TO '用户名'@'主机名';
```

- **解释**：授予用户对指定数据库或表的操作权限。
- **常用权限**：
  - `SELECT`：查询
  - `INSERT`：插入
  - `UPDATE`：更新
  - `DELETE`：删除
  - `ALL`：所有权限
- **示例**：
  ```sql
  GRANT SELECT, INSERT ON mydb.* TO 'john'@'localhost';
  ```

### 2.2. 撤销权限

```sql
REVOKE 权限 ON 数据库名.表名 FROM '用户名'@'主机名';
```

- **解释**：撤销用户对指定数据库或表的操作权限。
- **示例**：
  ```sql
  REVOKE INSERT ON mydb.* FROM 'john'@'localhost';
  ```

### 2.3. 查看用户权限

```sql
SHOW GRANTS FOR '用户名'@'主机名';
```

- **解释**：查看指定用户的权限详情。
- **示例**：
  ```sql
  SHOW GRANTS FOR 'john'@'localhost';
  ```

---

## 3. 事务控制

### 3.1. 开启事务

```sql
START TRANSACTION;
```

- **解释**：开启一个新事务。

### 3.2. 提交事务

```sql
COMMIT;
```

- **解释**：提交当前事务，使所有更改生效。

### 3.3. 回滚事务

```sql
ROLLBACK;
```

- **解释**：回滚当前事务，撤销所有未提交的更改。

### 3.4. 设置自动提交

```sql
SET autocommit = 0; -- 关闭自动提交
SET autocommit = 1; -- 开启自动提交
```

- **解释**：设置是否自动提交事务。`0` 表示关闭，`1` 表示开启。

---

## 4. 其他常用操作

### 4.1. 刷新权限

```sql
FLUSH PRIVILEGES;
```

- **解释**：刷新权限表，使权限更改立即生效。

### 4.2. 查看当前用户

```sql
SELECT CURRENT_USER();
```

- **解释**：查看当前登录的用户。
- **示例**：
  ```sql
  SELECT CURRENT_USER();
  ```

---

## 5. 常用命令速查表

|操作|命令示例|
| ------------| --------|
|创建用户|`CREATE USER 'john'@'localhost' IDENTIFIED BY 'password123';`|
|修改密码|`ALTER USER 'john'@'localhost' IDENTIFIED BY 'newpassword123';`|
|删除用户|`DROP USER 'john'@'localhost';`|
|查看所有用户|`SELECT user, host FROM mysql.user;`|
|授予权限|`GRANT SELECT, INSERT ON mydb.* TO 'john'@'localhost';`|
|撤销权限|`REVOKE INSERT ON mydb.* FROM 'john'@'localhost';`|
|查看用户权限|`SHOW GRANTS FOR 'john'@'localhost';`|
|开启事务|`START TRANSACTION;`|
|提交事务|`COMMIT;`|
|回滚事务|`ROLLBACK;`|
|刷新权限|`FLUSH PRIVILEGES;`|
|查看当前用户|`SELECT CURRENT_USER();`|

---

## 6. 总结

DCL 操作用于管理数据库的用户权限和事务控制，常用的操作包括：

1. **用户管理**：创建、修改、删除用户。
2. **权限管理**：授予、撤销权限，查看用户权限。
3. **事务控制**：开启、提交、回滚事务。
4. **其他操作**：刷新权限、查看当前用户。

掌握这些常用命令可以帮助你更好地管理数据库的安全性和一致性！
