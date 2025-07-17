# Debian 配置 Systemd 开机自启动服务

## 1 ### 📌 什么是 systemd？

`systemd` 是 Linux 系统中用于管理服务的工具。我们可以通过它让程序在系统启动时自动运行。

---

# 2 ## 🧱 前提条件

你的文件结构如下：

- 可执行文件路径：`/opt/frp/frpc`
    
- 配置文件路径：`/etc/frp/frpc.toml`

---

# 3 ## 🛠 第一步：编写服务文件

服务文件就是告诉系统：

> “启动哪个程序、怎么启动、什么时候启动”。

我们将创建一个服务文件 `frpc.service`，位置放在 `/etc/systemd/system/` 目录。

## 1 创建文件

在终端中输入以下命令：

```bash
sudo nano /etc/systemd/system/frpc.service
```

## 2 填入以下内容

```ini
[Unit]
Description=FRP Client Service (frpc)   # 服务的描述信息
After=network.target                    # 表示网络服务启动之后再启动 frpc

[Service]
Type=simple                             # 简单的启动方式（适用于大多数程序）
ExecStart=/opt/frp/frpc -c /etc/frp/frpc.toml   # 启动时执行的命令
Restart=on-failure                      # 如果 frpc 出错退出，自动重启

[Install]
WantedBy=multi-user.target              # 表示系统正常启动时启用这个服务
```

按下 `Ctrl + O` 保存文件，然后按 `Ctrl + X` 退出编辑器。

---

# 4 ## ✅ 第二步：设置服务生效并启用

## 1 重新加载配置文件

```bash
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
```

## 2 设置为“开机自动启动”

```bash
sudo systemctl enable frpc
```

## 3 立即启动 Frpc

```bash
sudo systemctl start frpc
```

---

# 5 ## 🧪 第三步：检查是否运行成功

你可以用以下命令查看服务状态：

```bash
sudo systemctl status frpc
```

看到 `Active: active (running)` 就说明运行成功了。

---

# 6 ## 🧹 常用命令汇总

|命令|作用|
|---|---|
|`sudo systemctl start frpc`|启动 frpc 服务|
|`sudo systemctl stop frpc`|停止 frpc 服务|
|`sudo systemctl restart frpc`|重启 frpc 服务|
|`sudo systemctl status frpc`|查看服务状态|
|`sudo systemctl enable frpc`|设置开机自动启动|
|`sudo systemctl disable frpc`|取消开机自动启动|
|`journalctl -u frpc -b`|查看 frpc 的运行日志|

---

如果你希望我继续扩展这份文档（比如加上如何调试失败、如何卸载 frpc 服务等），可以告诉我，我可以做成更完整的一份 PDF 学习资料。你需要吗？