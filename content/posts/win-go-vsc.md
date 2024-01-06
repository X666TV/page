---
title : 'win-go-vscode环境配置'
slug : win-go-vsc
date : 2022-08-13T12:00:00+08:00
draft : false
tags : ['备忘']
toc : false
---

{{< admonition warning "Warning" >}}
该文章年久失修，可能已不适用
{{< /admonition >}}

_记录自己配置go开发环境的过程，以免以后又踩坑_
1.  下载zip或msi文件，解压或安装 
2.  改环境变量：zip安装：添加PATH，GOPATH，GOROOT（可选）；msi：调整GOPATH位置（默认为用户目录的文件夹），添加GOROOT（可选）,此时在任意位置运行go命令是没问题的
_GOROOT为 go的安装路径,即根目录,PATH下添加根目录的bin文件夹,GOPATH会作为go的包的安装位置_ 
3.  调整go env:用`go env -w xxx=xxx`，或者直接去GOENV所指的文件改（直接加） 
   - GO111MODULE：默认为空，即auto，可以不管他，也可以设为on,
   - GOPROXY：go get 使用的国内代理，有两个，自己上网查，永久改要用go env
   - 如果用msi安装在非默认路径，GOPATH可以改，但GOCACHE和GOENV不太好改，就暂时不要改了
   - 懒人专用：
```powershell
go env -w GOPROXY=https://goproxy.io,direct
```

4.  创建文件夹，创建go代码文件main.go,
懒人专用:  
```go
package main
import "fmt"
func main(){
    fmt.Println("hello go")
}
```

5.  当前文件夹执行 `go mod init` 或 `go mod tidy` 生成go.mod文件,如果用不了,去检查go安装,如果go安装没问题,看看是不是版本太旧了 
6.  配置VS Code:打开vscode,安装插件:Code Runner,Go;除此之外,打开main.go文件时会有弹窗,点击安装,安装所有go工具,这里很可能会出现安装失败的情况,可以尝试以下方法: 
   - 检查网络连接,一般有国内网就行了,无需翻墙
   - 检查GOPATH环境变量是否配置正确,以及对应目录下是否有bin,pkg,src三个文件夹,没有则添加
   - 检查步骤1-3是否有问题,可尝试把GO111MODULE设为on,以及设置GOROOT环境变量
   - 实在不行可以手动下载,这里有两个参考:[知乎](https://zhuanlan.zhihu.com/p/56567884),[博客园](https://www.cnblogs.com/feiquan/p/11433461.html)
   - 正常情况下下载完后会发现GOPATH路径下bin,pkg文件夹下多了东西
