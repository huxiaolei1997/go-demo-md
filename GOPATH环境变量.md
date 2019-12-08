# GOPATH环境变量

默认在~/go(unix,linux), %USERPROFILE%\go(windows)

官方推荐：所有项目和第三方库都放在同一个GOPATH下

也可以将每个项目放在不同的GOPATH



# 安装gopm

```shell
go get github.com/gpmgo/gopm
go install github.com/gpmgo/gop
```



如果能够科学上网，那么就不需要安装 gopm，可以直接通过go命令来安装 各种包，比如安装goimports，可以帮助我们移除无用的包

> go install golang.org/x/tools/cmd/goimports   



## go build

go build 命令可以将Go语言程序代码编译成二进制的可执行文件，但是需要我们手动运行该二进制文件；但是会在当前目录生成一个与 main 包文件同名的 .exe 可执行文件

* 当参数不为空时

如果 fileName 为同一 main 包下的所有源文件名（可能有一个或者多个），编译器将生成一个与第一个 fileName 同名的可执行文件（如执行`go build abc.go def.go ...`会生成一个 abc.exe 文件）；如果 fileName 为非 main 包下的源文件名，编译器将只对该包进行语法检查，不生成可执行文件。

* 当参数为空时

如果当前目录下存在 main 包，则会生成一个与当前目录名同名的“目录名.exe”可执行文件（如在 hello 目录中执行`go build`命令时，会生成 hello.exe 文件）；如果不存在 main 包，则只对当前目录下的程序源码进行语法检查，不会生成可执行文件。

## go install

go install 产生pkg文件和可执行文件

## go run

go run 命令则更加方便，它会在编译后直接运行Go语言程序，编译过程中会产生一个临时文件，但不会生成可执行文件，这个特点很适合用来调试程序。

`go run`命令的语法格式如下：

> go run fileName

其中 `fileName` 为所需要的参数，参数必须是`同一 main 包`下的所有源文件名，并且不能为空。



#### GOPROXY

proxy 顾名思义就是代理服务器的意思。大家都知道，国内的网络有防火墙的存在，这导致有些Go语言的第三方包我们无法直接通过`go get `命令获取。GOPROXY 是Go语言官方提供的一种通过中间代理商来为用户提供包下载服务的方式。要使用 GOPROXY 只需要设置环境变量 GOPROXY 即可。

目前公开的代理服务器的地址有：

- goproxy.io
- goproxy.cn：（推荐）由国内的七牛云提供。


Windows 下设置 GOPROXY 的命令为：

> go env -w GOPROXY=https://goproxy.cn,direct

MacOS 或 Linux 下设置 GOPROXY 的命令为：

> export GOPROXY=https://goproxy.cn

Go语言在 1.13 版本之后 GOPROXY 默认值为 https://proxy.golang.org，在国内可能会存在下载慢或者无法访问的情况，所以十分建议大家将 GOPROXY 设置为国内的 goproxy.cn。

#### 使用go get命令下载指定版本的依赖包

执行`go get `命令，在下载依赖包的同时还可以指定依赖包的版本。

- 运行`go get -u`命令会将项目中的包升级到最新的次要版本或者修订版本；
- 运行`go get -u=patch`命令会将项目中的包升级到最新的修订版本；
- 运行`go get [包名]@[版本号]`命令会下载对应包的指定版本或者将对应包升级到指定的版本。

提示：`go get [包名]@[版本号]`命令中版本号可以是 x.y.z 的形式，例如 go get foo@v1.2.3，也可以是 git 上的分支或 tag，例如 go get foo@master，还可以是 git 提交时的哈希值，例如 go get foo@e3702bed2。