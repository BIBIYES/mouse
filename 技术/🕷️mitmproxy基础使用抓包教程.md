## 1 安装 `mitmproxy`
可以现在通过  
* [Microsoft](ms-windows-store://pdp/?ProductId=9NWNDLQMNZD7) 
* [github](https://github.com/mitmproxy/mitmproxy)
* `mitmproxy` [官网](https://mitmproxy.org/)
三种方式来安装

## 2 运行 `mitmproxy`

1. 打开 `cmd` 输入

```bash
mitmweb -p 9000 --set web_port=9001
```
2. 我们打开浏览器输入 `http://127.0.0.1:9001` 来进入到 `mitmproxy` web 界面
	![[Pasted image 20250416204653.png]]
到这样我们就算安装完成了
>  **在命令行中**
>  第一个是 `mitmproxy` 代理的监听端口
>  第二个是 `mitmproxy` web 界面的监听端口
## 3 配置代理

现在我们是**无法抓取**我们电脑的上的数据包的，*因为我们还没有配置代理*
	1. 打开 `windwos ` 网络和 `Internet` 手动设置代理服务器
	2. 配置 ip 地址为 127.0.0.1 端口为 9000 如图
	![[Pasted image 20250416205042.png]]
## 4 安装 `mitmproxy` 根证书

*如果我们没有安装根证书, 是无法抓取到 `https` 流量的*
1. 在浏览器地址栏中输入 `http://mitm.it`
2. 下载当前系统的证书 ![[Pasted image 20250416205554.png]]
3. 下载完成后双击打开根证书, 进入证书导入向导, 我们选择本地计算机 ![[Pasted image 20250416205747.png]]
4. 一直下一步直到**这里**按照图片配置 ![[Pasted image 20250416210002.png]] 确定之后我们的证书就安装完成了