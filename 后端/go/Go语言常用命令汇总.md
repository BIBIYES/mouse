# Go语言常用命令汇总

Go语言提供了一系列命令行工具，用于代码编译、运行、测试、依赖管理等多种开发任务。本文档列出了Go语言及Go Modules的主要命令及其简要说明。

## 1 Go语言基本命令

| 命令           | 说明           | 示例                      |
| ------------ | ------------ | ----------------------- |
| `go build`   | 编译包和依赖项      | `go build myapp`        |
| `go clean`   | 移除对象文件和缓存文件  | `go clean`              |
| `go doc`     | 显示包或符号的文档    | `go doc fmt`            |
| `go env`     | 打印Go环境信息     | `go env`                |
| `go fmt`     | 格式化包源代码      | `go fmt ./...`          |
| `go get`     | 添加依赖到当前模块并安装 | `go get github.com/pkg` |
| `go install` | 编译并安装包和依赖    | `go install myapp`      |
| `go list`    | 列出包或模块       | `go list ./...`         |
| `go run`     | 编译并运行Go程序    | `go run main.go`        |
| `go test`    | 测试包          | `go test ./...`         |
| `go version` | 打印Go版本       | `go version`            |

## 2 辅助命令

|命令|说明|示例|
|---|---|---|
|`go bug`|开始一个错误报告|`go bug`|
|`go fix`|更新包以使用新的API|`go fix oldpackage`|
|`go generate`|通过处理源代码生成Go文件|`go generate ./...`|
|`go tool`|运行指定的Go工具|`go tool vet .`|
|`go vet`|报告包中可能的错误|`go vet ./...`|

## 3 Go Modules命令

|命令|说明|示例|
|---|---|---|
|`go mod download`|下载模块到本地缓存|`go mod download`|
|`go mod edit`|编辑`go.mod`文件|`go mod edit -fmt`|
|`go mod graph`|打印模块依赖图|`go mod graph`|
|`go mod init`|在当前目录初始化新模块|`go mod init mymodule`|
|`go mod tidy`|添加缺失模块并移除未使用模块|`go mod tidy`|
|`go mod vendor`|制作依赖的vendored副本|`go mod vendor`|
|`go mod verify`|验证依赖具有预期内容|`go mod verify`|
|`go mod why`|解释为什么需要某个包或模块|`go mod why github.com/pkg`|

## 4 使用示例

- **添加依赖**

    bash

    `go get github.com/some/dependency`

- **初始化模块**

    bash

    `go mod init myproject`

- **格式化代码**

    bash

    `go fmt ./...`

- **运行测试**

    bash

    `go test ./...`

---

下面是关于在Windows上使用Go语言打包的补充说明及示例命令，采用Markdown格式：

---

# Windows平台Go语言打包命令

在Windows上编译Go程序时，默认生成的是控制台程序，运行时会弹出命令提示符窗口。如果你的程序是GUI应用，通常希望避免弹出命令行窗口。Go提供了`-ldflags -H=windowsgui`选项，可以让生成的可执行文件以Windows GUI程序的形式运行，从而不显示命令行窗口。

## 1 常用命令示例

```go
go build -ldflags "-H=windowsgui" -o mouse.exe
```

- `-ldflags "-H=windowsgui"`：告诉Go编译器生成Windows GUI程序，避免弹出命令行窗口。
    
- `-o mouse.exe`：指定输出的可执行文件名。

## 2 其他常用优化参数

为了减小生成的可执行文件体积，可以配合使用以下参数：

bash

`go build -ldflags "-s -w -H=windowsgui" -o mouse.exe`

- `-s`：去除符号表。
    
- `-w`：去除调试信息。

## 3 脚本示例（Windows批处理）

你可以写一个简单的`build.bat`脚本，方便每次构建：

text

`go build -ldflags "-s -w -H=windowsgui" -o mouse.exe`

然后在命令行执行：

text

`build.bat`

即可生成无命令行窗口的GUI程序。

## 4 跨平台编译示例

如果你在非Windows系统上开发，需要交叉编译Windows可执行文件，可以设置环境变量：

bash

`GOOS=windows GOARCH=amd64 go build -ldflags "-H=windowsgui" -o mouse.exe`

这条命令会生成Windows 64位的GUI程序。

---
