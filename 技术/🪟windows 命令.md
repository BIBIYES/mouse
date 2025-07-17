# Windows 常用命令参考文档

## 1 文件和目录操作

|命令|参数|功能描述|示例|
|---|---|---|---|
|`dir`|`/a` `/s` `/b` `/p`|列出目录内容<br>`/a` 显示所有文件<br>`/s` 包括子目录<br>`/b` 简洁格式<br>`/p` 分页显示|`dir /a /s`|
|`cd`|`..` `/d`|更改目录<br>`..` 返回上级<br>`/d` 跨驱动器|`cd /d D:\folder`|
|`md` / `mkdir`|-|创建目录|`mkdir newfolder`|
|`rd` / `rmdir`|`/s` `/q`|删除目录<br>`/s` 删除子目录<br>`/q` 静默模式|`rmdir /s /q folder`|
|`copy`|`/y` `/v` `/s`|复制文件<br>`/y` 不确认覆盖<br>`/v` 验证复制<br>`/s` 复制子目录|`copy /s source dest`|
|`xcopy`|`/e` `/h` `/k` `/y`|增强复制<br>`/e` 复制空目录<br>`/h` 复制隐藏文件<br>`/k` 保留属性<br>`/y` 不确认|`xcopy /e /h source dest`|
|`move`|`/y`|移动/重命名文件|`move oldname newname`|
|`del` / `erase`|`/f` `/s` `/q`|删除文件<br>`/f` 强制删除<br>`/s` 删除子目录中文件<br>`/q` 静默模式|`del /f /s *.tmp`|
|`ren` / `rename`|-|重命名文件|`ren old.txt new.txt`|

## 2 系统信息和管理

|命令|参数|功能描述|示例|
|---|---|---|---|
|`systeminfo`|`/s` `/u` `/p`|显示系统信息<br>`/s` 远程系统<br>`/u` 用户名<br>`/p` 密码|`systeminfo`|
|`tasklist`|`/svc` `/m` `/v`|显示进程列表<br>`/svc` 显示服务<br>`/m` 显示模块<br>`/v` 详细信息|`tasklist /svc`|
|`taskkill`|`/f` `/im` `/pid`|结束进程<br>`/f` 强制结束<br>`/im` 按映像名<br>`/pid` 按进程ID|`taskkill /f /im notepad.exe`|
|`services.msc`|-|打开服务管理器|`services.msc`|
|`msconfig`|-|系统配置实用程序|`msconfig`|
|`dxdiag`|-|DirectX 诊断工具|`dxdiag`|
|`msinfo32`|-|系统信息工具|`msinfo32`|

## 3 网络命令

|命令|参数|功能描述|示例|
|---|---|---|---|
|`ping`|`-t` `-n` `-l`|测试网络连通性<br>`-t` 持续ping<br>`-n` 指定次数<br>`-l` 数据包大小|`ping -n 10 google.com`|
|`ipconfig`|`/all` `/release` `/renew` `/flushdns`|IP配置<br>`/all` 详细信息<br>`/release` 释放IP<br>`/renew` 更新IP<br>`/flushdns` 刷新DNS|`ipconfig /all`|
|`netstat`|`-a` `-n` `-o` `-r`|网络连接状态<br>`-a` 所有连接<br>`-n` 数字格式<br>`-o` 显示PID<br>`-r` 路由表|`netstat -ano`|
|`nslookup`|-|DNS查询|`nslookup google.com`|
|`tracert`|`-h` `-w`|路由跟踪<br>`-h` 最大跳数<br>`-w` 超时时间|`tracert google.com`|
|`telnet`|-|远程连接|`telnet 192.168.1.1 80`|
|`netsh`|-|网络配置工具|`netsh wlan show profiles`|

## 4 磁盘管理

|命令|参数|功能描述|示例|
|---|---|---|---|
|`diskpart`|-|磁盘分区工具|`diskpart`|
|`chkdsk`|`/f` `/r` `/x`|检查磁盘<br>`/f` 修复错误<br>`/r` 恢复坏扇区<br>`/x` 强制卸载|`chkdsk C: /f`|
|`sfc`|`/scannow` `/verifyonly`|系统文件检查<br>`/scannow` 扫描修复<br>`/verifyonly` 仅验证|`sfc /scannow`|
|`defrag`|`/a` `/v` `/x`|磁盘碎片整理<br>`/a` 分析<br>`/v` 详细输出<br>`/x` 自由空间整理|`defrag C: /a`|
|`format`|`/fs` `/q` `/v`|格式化磁盘<br>`/fs` 文件系统<br>`/q` 快速格式化<br>`/v` 卷标|`format D: /fs:NTFS /q`|

## 5 文本处理

|命令|参数|功能描述|示例|
|---|---|---|---|
|`type`|-|显示文件内容|`type readme.txt`|
|`more`|-|分页显示文本|`more file.txt`|
|`find`|`/i` `/c` `/n`|搜索文本<br>`/i` 忽略大小写<br>`/c` 统计行数<br>`/n` 显示行号|`find /i "error" log.txt`|
|`findstr`|`/i` `/r` `/c`|高级搜索<br>`/i` 忽略大小写<br>`/r` 正则表达式<br>`/c` 字面字符串|`findstr /i /r "error.*" *.log`|
|`sort`|`/r` `/+n`|排序文本<br>`/r` 逆序<br>`/+n` 从第n列开始|`sort /r data.txt`|
|`fc`|`/a` `/c` `/n`|文件比较<br>`/a` 简化输出<br>`/c` 忽略大小写<br>`/n` 显示行号|`fc /c file1.txt file2.txt`|

## 6 用户和权限管理

|命令|参数|功能描述|示例|
|---|---|---|---|
|`net user`|`/add` `/delete` `/active`|用户管理<br>`/add` 添加用户<br>`/delete` 删除用户<br>`/active` 激活状态|`net user newuser /add`|
|`net localgroup`|`/add` `/delete`|本地组管理|`net localgroup administrators`|
|`whoami`|`/all` `/groups` `/priv`|当前用户信息<br>`/all` 所有信息<br>`/groups` 组信息<br>`/priv` 权限信息|`whoami /all`|
|`runas`|`/user` `/noprofile`|以其他用户身份运行<br>`/user` 指定用户<br>`/noprofile` 不加载配置文件|`runas /user:admin cmd`|
|`cacls`|`/p` `/g` `/r`|文件权限<br>`/p` 替换权限<br>`/g` 授予权限<br>`/r` 撤销权限|`cacls file.txt /g user:F`|

## 7 注册表操作

|命令|参数|功能描述|示例|
|---|---|---|---|
|`reg query`|`/s` `/v` `/f`|查询注册表<br>`/s` 递归查询<br>`/v` 指定值<br>`/f` 过滤条件|`reg query HKLM\Software`|
|`reg add`|`/v` `/t` `/d` `/f`|添加注册表项<br>`/v` 值名<br>`/t` 数据类型<br>`/d` 数据<br>`/f` 强制覆盖|`reg add HKCU\Test /v Name /d Value`|
|`reg delete`|`/v` `/f`|删除注册表项<br>`/v` 值名<br>`/f` 强制删除|`reg delete HKCU\Test /f`|
|`regedit`|`/s` `/e`|注册表编辑器<br>`/s` 静默导入<br>`/e` 导出|`regedit /s backup.reg`|

## 8 环境变量和批处理

|命令|参数|功能描述|示例|
|---|---|---|---|
|`set`|-|显示/设置环境变量|`set PATH`|
|`setx`|`/m` `/k`|永久设置环境变量<br>`/m` 系统变量<br>`/k` 注册表路径|`setx PATH "%PATH%;C:\tools"`|
|`echo`|`off` `on`|显示文本/控制回显|`echo Hello World`|
|`pause`|-|暂停批处理|`pause`|
|`call`|-|调用另一个批处理|`call script.bat`|
|`goto`|-|跳转到标签|`goto :label`|
|`if`|`/i` `exist` `not`|条件判断<br>`/i` 忽略大小写<br>`exist` 文件存在<br>`not` 取反|`if exist file.txt echo Found`|
|`for`|`/l` `/f` `/d` `/r`|循环结构<br>`/l` 数值循环<br>`/f` 文件处理<br>`/d` 目录<br>`/r` 递归|`for /l %%i in (1,1,10) do echo %%i`|

## 9 其他实用命令

|命令|参数|功能描述|示例|
|---|---|---|---|
|`cls`|-|清屏|`cls`|
|`date`|`/t`|显示/设置日期<br>`/t` 仅显示|`date /t`|
|`time`|`/t`|显示/设置时间<br>`/t` 仅显示|`time /t`|
|`ver`|-|显示Windows版本|`ver`|
|`title`|-|设置窗口标题|`title My Command Window`|
|`color`|-|设置控制台颜色|`color 0A`|
|`mode`|-|配置系统设备|`mode con cols=80 lines=25`|
|`shutdown`|`/s` `/r` `/l` `/t`|关机命令<br>`/s` 关机<br>`/r` 重启<br>`/l` 注销<br>`/t` 延时|`shutdown /s /t 60`|
|`gpupdate`|`/force` `/target`|更新组策略<br>`/force` 强制更新<br>`/target` 目标|`gpupdate /force`|
|`powercfg`|`/list` `/query` `/h`|电源配置<br>`/list` 列出方案<br>`/query` 查询<br>`/h` 休眠设置|`powercfg /list`|

## 10 快捷键组合

|组合键|功能描述|
|---|---|
|`Ctrl + C`|中断当前命令|
|`Ctrl + Z`|暂停当前命令|
|`Tab`|自动完成文件名/命令|
|`F1`|逐字符重复上一命令|
|`F3`|重复上一命令|
|`F7`|显示命令历史|
|`F8`|搜索命令历史|
|`F9`|按编号选择历史命令|
|`Alt + F7`|清除命令历史|

## 11 重定向和管道

|符号|功能描述|示例|
|---|---|---|
|`>`|重定向输出到文件|`dir > list.txt`|
|`>>`|追加输出到文件|`echo text >> file.txt`|
|`<`|从文件输入|`sort < data.txt`|
|`\|`|管道传递|`dir \| find "txt"`|
|`&`|连接命令|`echo A & echo B`|
|`&&`|条件执行(成功)|`dir && echo Success`|
|`\|`|条件执行(失败)|`dir missing \| echo Failed`|

---

_此文档涵盖了Windows命令行中最常用的命令和参数。使用时请注意权限要求，某些命令需要管理员权限。_