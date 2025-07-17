# Ubuntu Ufw防火墙使用指南

## 1 安装 `ufw`

```shell
sudo apt-get install ufw
```

## 2 开启防火墙

```shell
sudo ufw enable
```

## 3 开放端口

```shell
ufw allow 22
```

## 4 重载防火墙

```shell
sudo ufw reload
```

## 5 查看防火墙状态

```shell
sudo ufw status
```

## 6 Netstat 查看系统监听端口

```shell
netstat -tunlp
```

## 7 关闭防火墙

```shell
sudo ufw disable
```

## 8 关闭端口

```shell
sudo ufw delete allow 21
```

## 9 开放规定协议的端口

```shell
 sudo ufw allow 8001/tcp
```

## 10 关闭规定协议的端口

```shell
ufw delete allow 8001/tcp
```
