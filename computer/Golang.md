# Golang

[TOC]

## Introduction

## 数据类型

数组（Array）

切片（Slice）

字符串（String）

Map（哈希表）

结构体（Struct）

指针（Pointer）

## 函数

函数的定义与调用
变量作用域
多返回值
匿名函数与闭包
Defer 关键字

## Interface & reflect

## 并发编程

Goroutine

Channel

sync 包（WaitGroup、Mutex、Once、Cond）

Context 控制并发

### Goroutine 调度

调度策略（G-P-M 模型）
G（Goroutine）：代表一个 Goroutine，是 Go 语言中的轻量级协程，每个 Goroutine 都有自己的栈空间、程序计数器等上下文信息。
P（Processor）：处理器，它负责管理和执行 Goroutine。每个 P 都有一个本地的 Goroutine 队列，P 会从自己的本地队列或全局队列中获取 Goroutine 来执行，同时 P 还与一个操作系统线程绑定，在该线程上执行 Goroutine。
M（Machine）：代表操作系统线程，M 负责执行 P 分配给它的 Goroutine。M 与 P 是多对多的关系，一个 M 可以绑定到不同的 P 上，一个 P 也可以在不同的 M 上运行。
调度策略就是在 G、P、M 之间进行合理的资源分配和任务调度。例如，当一个 P 的本地队列空了，它会尝试从其他 P 的本地队列中窃取一半的 Goroutine 到自己的队列，以实现负载均衡。



## 错误处理

error 接口

自定义错误类型

panic 和 recover

## 数据库操作

## Web 开发

HTTP 服务器（net/http）

RESTful API 设计

Gin/Gorm 框架

中间件

WebSocket

## Go 语言测试

单元测试（testing 包）

性能测试（benchmark）

Mock 测试

## 配置管理
读取 JSON/YAML 配置
使用 Viper 进行配置管理

## 部署与运维

Go 代码编译和交叉编译

使用 Docker 部署

Kubernetes（K8s）管理 Go 服务

CI/CD 集成（GitHub Actions、Jenkins）