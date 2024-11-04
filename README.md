# Gomall

## Goroutine

协程：用户态，轻量级线程，栈KB级别

线程：内核态，线程跑多个协程，栈MB级别

## CSP(Communicating Sequential Processes)

提倡通过**通信共享内存**而不是通过共享内存而通信

## Channel

make(chan 元素类型, [缓存大小])

+ 无缓存通道(同步通道)  make(chan int)
+ 有缓存通道  make(chan int,2)

## 并发安全Lock

## WaitGroup

Add

Done

Wait

## 依赖管理

### GOPATH

+ bin 项目编译的二进制文件

+ pkg 项目编译的中间产物，加速编译

+ src 项目源码

项目代码直接依赖src下的代码

go get下载最新版本的包到src目录下

弊端：

场景：A和B依赖某一package的不同版本

问题：无法实现package的多版本控制

## Go Vender

项目目录增加vendor文件夹

依赖寻址方式：vendor => GOPATH

问题：

无法控制依赖版本

更新项目又可能出现依赖冲突，导致编译出错

## Go Module

通过go.mod文件管理依赖包版本

通过go get/go mod指令工具管理依赖包

## 依赖管理三要素

1.配置文件，描述依赖  go.mod

2.中心仓库管理依赖库 Proxy

3.本地工具  go get/mod

## 单元测试

规则：

+ 所有测试文件以_test.go结尾

+ func TestXxx(*testing.T)

+ 初始化逻辑放到了TestMain中

运行：

go test \[flags][packages]

assert

--cover计算单元测试覆盖率

Tips：

+ 一般覆盖率：50%~60%，较高覆盖率80%+
+ 测试分支相互独立、全面覆盖
+ 测试单元粒度足够小，函数单一职责

Mock：https://github.com/bouk/monkey

+ 为一个函数打桩
+ 为一个方法打桩
+ 不依赖本地文件

基准测试：

+ 优化代码，需要对当前代码分析
+ 内置的测试框架提供了基准测试的能力

优化：

https://github.com/bytedance/gopkg