
## 1 下载 HBuilder X

点击下方链接下载 HBuilder X：  
👉 [HBuilder X 下载地址](https://www.dcloud.io/hbuilderx.html)

---

## 2 创建项目

1. 打开 HBuilder X，点击 **文件 > 新建 > 项目**
    
2. 在模板选择中，建议使用 **默认模板**  
	
3. 如果开发 **跨平台应用**，记得勾选 **uni-app x**
    
4. Vue 版本请选择 **Vue 3**
    

---

## 3 项目目录结构说明

```plaintext
├─uniCloud              云空间目录，按云服务商划分子目录
├─components            Vue 组件目录（复用组件）
│  └─comp-a.vue         示例组件
├─utssdk                UTS 文件目录（已废弃）
├─pages                 业务页面存放位置
│  ├─index/index.vue    首页
│  └─list/list.vue      列表页
├─static                静态资源（如图片、视频）
├─uni_modules           存放 uni 模块
├─platforms             各平台专属页面
├─nativeplugins         App 原生语言插件
├─nativeResources       App 原生资源目录
│  ├─android            Android 原生资源
│  └─ios                iOS 原生资源
├─hybrid                App 本地 html 文件
├─wxcomponents          微信/QQ 小程序组件
├─mycomponents          支付宝小程序组件
├─swancomponents        百度小程序组件
├─ttcomponents          抖音/飞书小程序组件
├─kscomponents          快手小程序组件
├─jdcomponents          京东小程序组件
├─unpackage             编译结果文件夹
├─main.js               Vue 初始化入口
├─App.vue               应用全局配置与生命周期
├─pages.json            页面路由与导航配置
├─manifest.json         App 信息与打包配置
├─AndroidManifest.xml   Android 应用清单
├─Info.plist            iOS 配置文件
└─uni.scss              常用样式变量
```

---

## 4 配置外部浏览器与小程序模拟器

### 4.1 外部浏览器配置

如果点击“运行到浏览器”无反应，可按以下步骤操作：

1. 点击菜单栏的 **工具 > 设置**
    
2. 找到 **运行配置 > 浏览器路径**
    
3. 添加你的浏览器执行路径  
    

---

### 4.2 微信小程序模拟器配置

如果要在 **微信小程序端**运行项目，需要安装微信小程序开发者工具。

1. 👉 [微信开发者工具下载（Windows）](https://servicewechat.com/wxa-dev-logic/download_redirect?type=win32_x64&from=mpwiki&download_version=1062503290&version_type=1)
2. 在 `HBuilder X` **工具 > 设置 > 微信开发者工具路径**中配置微信开发者工具安装路径
	![[Pasted image 20250506230527.png]]
3. 运行到微信开发者工具**运行 > 运行到小程序模拟器 > 微信开发者工具 

>  如果你出现 **下载基础库版本 2.31.0 失败** 
>  尝试访问[连接](https://blog.csdn.net/qq_244060631/article/details/132118730) 来解决问题
