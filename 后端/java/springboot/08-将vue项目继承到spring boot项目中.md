若你不想前后端分离部署，你可以将 vue 项目打包到 springboot 项目中
1. 打包前配置
```json
build: {
    outDir: 'dist',  // 输出目录名
    rollupOptions: {
      output: {
        assetFileNames: (assetInfo) => {
          // 根据文件类型放到不同目录
          if (/\.(css)$/.test(assetInfo.name)) {
            return 'css/[name].[hash].[ext]';
          }
          if (/\.(png|jpe?g|svg|gif|ico)$/.test(assetInfo.name)) {
            return 'img/[name].[hash].[ext]';
          }
          return 'assets/[name].[hash].[ext]';
        },
        chunkFileNames: 'js/[name].[hash].js',
        entryFileNames: 'js/[name].[hash].js',
      }
    }
  }
```
2. 打包 vue 前端项目
```shell
pnpm run build
```
3. 将打包的文件放入到 springboot 项目的 static
4. 配置 springboot 来处理前端路由
在 Controoler 中来创建一个控制器来处理请求
```java
package com.example.spark.controller;  
import org.springframework.stereotype.Controller;  
import org.springframework.web.bind.annotation.GetMapping;  
@Controller  
public class WebController {  
    @GetMapping("/{path:^[^\\.]*}/**")  
    public String forward() {  
        return "forward:/index.html";  
    }  
}
```
