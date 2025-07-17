# 安装与卸载

## 1 包管理器安装

> **包管理器（Package Manager）** 是一种用于管理操作系统中软件包的工具，特别是 Linux 系统。它能自动处理软件的安装、更新、配置和卸载。

### 1.1 `apt` 的安装与卸载

1. **更新软件包列表**

   ```sh
   sudo apt update
   ```

   这条命令会更新本地的包列表，使得系统知道最新的软件包版本。

2. **搜索软件包**

   ```sh
   apt search <package_name>
   ```

   你可以使用这条命令来查找是否有你需要的软件包。例如，查找 `vim` 编辑器：

   ```sh
   apt search vim
   ```

3. **安装软件包**

   ```sh
   sudo apt install <package_name>
   ```

   这条命令会安装指定的软件包。如果想安装多个软件包，可以一次性指定：

   ```sh
   sudo apt install <package_name1> <package_name2>
   ```

4. **更新所有软件包**

   ```sh
   sudo apt upgrade
   ```

   这个命令会升级系统中已安装的所有包到最新版本。

5. **卸载软件包**

   ```sh
   sudo apt remove <package_name>
   ```

   这会卸载指定的软件包，但保留其配置文件。如果你想完全删除软件包，包括配置文件，可以使用：

   ```sh
   sudo apt purge <package_name>
   ```

6. **自动清除不再需要的软件包**

   ```sh
   sudo apt autoremove
   ```

   这个命令会删除不再需要的依赖包，这些依赖是曾经安装的软件包的一部分，但现在已经不再使用。

7. **查看包信息**

   ```sh
   apt show <package_name>
   ```

   这会显示有关某个包的详细信息，比如版本、描述、依赖关系等。

8. **清理本地缓存**

   ```sh
   sudo apt clean
   ```

   清理下载的包缓存，以释放硬盘空间。

---

如果有其他具体命令或功能不清楚，可以告诉我，我帮你进一步解答！
