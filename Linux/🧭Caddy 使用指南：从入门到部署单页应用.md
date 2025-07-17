# 🧭Caddy 使用指南：从入门到部署单页应用

## 1 部署单页应用（SPA）

一个常见的部署单页应用的配置

```json
:8080 {
    root * /var/website/xcamp-blog/dist
    file_server
    try_files {path} /index.html
}
```

它们分别是

* 静态资源目录
* 文件服务器
* 如果路径不存在尝试转发到 `index.html`

## 2 请求转发

若要将部分请求转发到指定端口进行处理

```json
:8080 {
    root * /var/website/xcamp-blog/dist
    file_server
    try_files {path} /index.html
    reverse_proxy /api/* localhost:5000
}
```

你可以可以转发所有请求到指定端口**反向代理**

```json
bibiyes.xyz {
    reverse_proxy /api/* localhost:5000
}
```

```json
:9085 {
    # 启用gzip压缩
    encode gzip

    # 指向Vue应用的构建目录 - 使用Windows路径格式
    root * ./dist

    # 处理API请求的反向代理
    handle /api/* {
        uri strip_prefix /api
        reverse_proxy http://127.0.0.1:9086
    }

    # 处理publicapi请求的反向代理
    handle /publicapi/* {
        reverse_proxy http://127.0.0.1:9086
    }

    # 处理上传图片的代理规则
    handle /uploads/* {
        reverse_proxy http://127.0.0.1:9086
    }
    
    # 处理上传图片的代理规则
    handle /empeExportExcel/* {
        reverse_proxy http://127.0.0.1:9086
    }
    
    # 处理上传图片的代理规则
    handle /template/* {
        reverse_proxy http://127.0.0.1:9086
    }


    # 处理其他所有请求 - 单页应用需要将所有路由重定向到index.html
    handle {
        try_files {path} /index.html
        file_server
    }

    # Windows下的日志配置
    log {
        output file C:/logs/caddy/vue-app.log {
            roll_size 10MB
            roll_keep 5
            roll_keep_for 720h
        }
    }
}

:9084 {
    # 启用gzip压缩
    encode gzip

    # 指向Vue应用的构建目录 - 使用Windows路径格式
    root * ./dist2

    # 处理API请求的反向代理
    handle /api/* {
        uri strip_prefix /api
        reverse_proxy http://112.124.23.138:81 
    }

    # 处理publicapi请求的反向代理
    handle /publicapi/* {
        reverse_proxy http://112.124.23.138:81 
    }

    # 处理上传图片的代理规则
    handle /uploads/* {
        reverse_proxy http://112.124.23.138:81 
    }


    # 处理其他所有请求 - 单页应用需要将所有路由重定向到index.html
    handle {
        try_files {path} /index.html
        file_server
    }

    # Windows下的日志配置
    log {
        output file C:/logs/caddy/vue-app.log {
            roll_size 10MB
            roll_keep 5
            roll_keep_for 720h
        }
    }
}
```