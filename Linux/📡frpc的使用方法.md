# Frpc的使用方法

## 1 `frps` 服务端配置（`frps.toml`）

```toml
[common]
bind_port = 7000
# 使用安全的认证令牌
token = "your_secure_token"
```

**解释：** 

- `bind_port = 7000`: `frps` 服务端的监听端口。
- `token`: 用于认证客户端，确保客户端能够与服务端建立连接。你需要确保客户端使用相同的令牌。

## 2 `frpc` 客户端配置（`frpc.toml`）

```toml
[common]
server_addr = "your_frps_server_ip"
server_port = 7000
# 与服务端相同的认证令牌
token = "your_secure_token"

# 安全代理配置示例（映射 SSH）
[[proxies]]
name = "ssh"
type = "tcp"
local_ip = "127.0.0.1"
local_port = 22
remote_port = 6000
```

## 3 启动命令

- 启动 `frps` 服务端：

```sh
./frps -c frps.toml
```

- 启动 `frpc` 客户端：

```sh
./frpc -c frpc.toml
```

这样你就可以通过安全的配置确保 `frpc` 和 `frps` 之间的通信安全且简单。

 