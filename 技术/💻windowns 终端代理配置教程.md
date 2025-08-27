# 💻windowns 终端代理配置教程

###通过 PowerShell 配置文件设置

1. **打开 PowerShell 配置文件**：
   - 打开 PowerShell，运行以下命令：

 ```powershell
	 	if (!(Test-Path -Path $PROFILE )) { New-Item -Type File -Path $PROFILE -Force }
		notepad $PROFILE
 ```

   - 这将打开 PowerShell 的配置文件。

2. **添加代理设置**：
   - 在打开的配置文件中，添加以下内容：

```powershell
$Env:http_proxy="http://127.0.0.1:10808"
$Env:https_proxy="http://127.0.0.1:10808"
```

   - 保存并关闭文件。

3. **重新加载配置文件**：
   - 在 PowerShell 中运行以下命令以重新加载配置文件：

```powershell
   . $PROFILE
 ```

## 1 验证代理是否生效

- 使用 `curl` 命令测试代理是否生效：

```bash
  		curl https://www.google.com
```

- 如果代理设置正确，响应应该会经过代理服务器。

通过以上方法，你可以实现 Windows 终端的永久代理设置。

## 2 安全代理

```cmd
ssh -L 20000:127.0.0.1:20000 root@1.1.1.1 -p 22
```