# MYSQL配置

## 修改root用户可以远程访问

1. 修改配置文件监听所有端口
2. 将root用户权限监听切换远程访问

    ```sql
    USE mysql;
    UPDATE user SET host = '%' WHERE user = 'root';
    ```

好的，以下是补全后的笔记，包含修改 MySQL 配置文件和授权 root 用户远程访问的详细步骤：

### 修改 Root 用户可以远程访问

1. **修改 MySQL 配置文件监听所有端口**

    * 找到 MySQL 配置文件，通常位于 `/etc/mysql/my.cnf`​ 或 `C:\ProgramData\MySQL\MySQL Server 8.0\my.ini`​（Windows）。
    * 修改 `bind-address`​ 设置，使其监听所有 IP 地址：

    ```ini
    [mysqld]
    bind-address = 0.0.0.0
    ```

2. **重启 MySQL 服务**

    * 修改配置文件后，重启 MySQL 服务使配置生效：

    ```bash
    sudo systemctl restart mysql
    ```

3. **将 root 用户权限切换为远程访问**

    * 登录 MySQL：

    ```bash
    mysql -u root -p
    ```

    * 选择 MySQL 数据库：

    ```sql
    USE mysql;
    ```

    * 修改 root 用户的访问权限，将 `host`​ 字段改为 `%`​，表示允许从任意 IP 地址进行连接：

    ```sql
    UPDATE user SET host = '%' WHERE user = 'root';
    ```

    * 刷新权限：

    ```sql
    FLUSH PRIVILEGES;
    ```
