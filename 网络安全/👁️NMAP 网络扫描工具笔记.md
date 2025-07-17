---
number headings: first-level 1, max 6, _.1.1
tags:
  - nmap
  - 渗透
  - 扫描
---

# 👁️NMAP 网络扫描工具笔记

## 1 基础概念

NMAP（Network Mapper）是一款开源的网络探测和安全审计工具，被网络管理员和安全专业人员广泛使用。它可以：

- 发现网络上的主机 
- 识别开放的端口
- 检测运行的服务及其版本
- 推断操作系统信息
- 探测网络安全状况

## 2 基础命令

### 2.1 基本扫描

```bash
# 基本扫描单个目标
nmap 192.168.1.1

# 扫描多个目标
nmap 192.168.1.1 192.168.1.2

# 扫描整个网段
nmap 192.168.1.0/24

# 从文件中读取目标
nmap -iL targets.txt
```

### 2.2 端口扫描选项

```bash
# 扫描特定端口
nmap -p 80,443 192.168.1.1

# 扫描端口范围
nmap -p 1-1000 192.168.1.1

# 扫描所有端口
nmap -p- 192.168.1.1

# 扫描常用端口
nmap --top-ports 100 192.168.1.1
```

### 2.3 扫描类型

```bash
# TCP SYN 扫描（半开放扫描，默认）
nmap -sS 192.168.1.1

# TCP 连接扫描
nmap -sT 192.168.1.1

# UDP 扫描
nmap -sU 192.168.1.1

# PING 扫描
nmap -sP 192.168.1.0/24

# 不进行 PING 检测
nmap -Pn 192.168.1.1
```

## 3 进阶技巧

### 3.1 版本检测

```bash
# 服务和版本检测
nmap -sV 192.168.1.1

# 积极的版本检测
nmap -sV --version-intensity 9 192.168.1.1
```

### 3.2 操作系统检测

```bash
# 操作系统检测
nmap -O 192.168.1.1

# 更多操作系统检测细节
nmap -O --osscan-guess 192.168.1.1
```

### 3.3 脚本扫描

```bash
# 默认脚本扫描
nmap -sC 192.168.1.1

# 指定脚本
nmap --script=http-title 192.168.1.1

# 脚本类别
nmap --script=vuln 192.168.1.1

# 多个脚本
nmap --script=http-headers,http-title 192.168.1.1
```

### 3.4 输出选项

```bash
# 详细输出
nmap -v 192.168.1.1

# 更详细输出
nmap -vv 192.168.1.1

# 保存为普通文本
nmap -oN output.txt 192.168.1.1

# 保存为 XML
nmap -oX output.xml 192.168.1.1

# 保存为所有格式
nmap -oA output 192.168.1.1
```

### 3.5 隐蔽扫描

```bash
# 慢速扫描
nmap --scan-delay 1s 192.168.1.1

# 伪装源 IP
nmap -S 10.0.0.1 192.168.1.1

# 分散速度
nmap -T0 192.168.1.1  # 偏执级别
nmap -T1 192.168.1.1  # 猥琐级别
nmap -T2 192.168.1.1  # 礼貌级别
nmap -T3 192.168.1.1  # 默认级别
nmap -T4 192.168.1.1  # 激进级别
nmap -T5 192.168.1.1  # 疯狂级别
```

### 3.6 防火墙/IDS 绕过

```bash
# 碎片扫描
nmap -f 192.168.1.1

# 指定 MTU
nmap --mtu 8 192.168.1.1

# 使用诱饵
nmap -D RND:10 192.168.1.1

# 自定义源端口
nmap --source-port 53 192.168.1.1
```

## 4 高级应用

### 4.1 综合扫描

```bash
# 全面扫描（慢但完整）
nmap -sS -sV -sC -A -O -p- 192.168.1.1

# 快速但有效的扫描
nmap -sV -sC -T4 --top-ports 1000 192.168.1.1
```

### 4.2 漏洞扫描

```bash
# 使用漏洞检测脚本
nmap --script vuln 192.168.1.1

# 针对特定服务的漏洞
nmap --script http-vuln* 192.168.1.1
```

### 4.3 NSE 脚本引擎

```bash
# 列出可用脚本
nmap --script-help "*"

# 列出特定类别脚本
nmap --script-help "http*"

# 使用脚本参数
nmap --script http-brute --script-args userdb=users.txt,passdb=pass.txt 192.168.1.1
```

### 4.4 网络发现

```bash
# 网络拓扑发现
nmap --traceroute 192.168.1.1

# 主机发现
nmap -sL 192.168.1.0/24
```

## 5 实战案例

1. **网络资产发现**:

    ```bash
    nmap -sP 192.168.1.0/24
    ```

2. **全面端口服务扫描**:

    ```bash
    nmap -sV -sC -p- -oA full_scan 192.168.1.1
    ```

3. **定期安全审计**:

    ```bash
    nmap --script vuln -oA security_audit 192.168.1.0/24
    ```

4. **Web 服务器扫描**:

    ```bash
    nmap -sV -p 80,443 --script http-enum,http-headers,http-title 192.168.1.1
    ```

5. **防火墙规则测试**:

    ```bash
    nmap -sA -p 1-1000 192.168.1.1
    ```

## 6 使用注意事项

1. **合法使用**: 仅在获得授权的网络上执行扫描
2. **流量控制**: 使用 `-T` 选项限制速度避免网络拥塞
3. **结果解读**: 准确理解扫描结果，避免误判
4. **保密性**: 妥善保管扫描结果，防止信息泄露
5. **更新维护**: 定期更新 NMAP 和脚本库

## 7 进阶学习资源

- 官方文档: https://nmap.org/book/
- NMAP 脚本库: https://nmap.org/nsedoc/
- 实战指南: https://nmap.org/docs/discovery.pdf

希望这份笔记对你学习 NMAP 从基础到进阶有所帮助！