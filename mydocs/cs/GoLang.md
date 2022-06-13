# 摘要

Go 是一个开源的编程语言，显著的特色是简洁快速和高并发性，常用在后端开发领域。Go 语言最初是 Google 为了代替 C/C++ 而开发的系统级语言，目前看来，Go 与 C/C++ 一样执行效率高、简单而强大且编译速度更快。与 Java 相比，Go 的体量更为简洁，且编译过程不需要借助虚拟机，故而效率更高，于此同时 Go 在并发编程上具有强大的实力。

# 基础

## Go 语言概述

Go 语言可以在 Linux、MacOS(Dariwn)、FreeBSD 和 Windows 操作系统上运行。

Windows Go 环境配置：

Linux Go 环境配置：

MacOS、FreeBSD 是类 UNIX 系统，我没用过，但应该与 Linux 的配置方法类似。

Go 语言的基本结构：

* 包声明
* 包导入
* 函数
* 变量
* 表达式
* 语句
* 注释

```go
package main //包声明

import "fmt" //包导入

/*主函数*/
func main() {
    var s = "hello world!" //Go 不用写分号
    fmt.Println(s)
}
```

## 数据类型和常变量

Go 中有四大类数据类型：

1. 布尔型(bool)：true 或 false
2. 数字类型：
    * 整数型
        * int(8 | 16 | 32 | 64)
        * uint(8 | 16 | 32 | 64)
    * 浮点型 
        * float(32 | 64)
        * complex(64 | 128)
3. 字符串类型(string)
4. 派生类型
    * 指针(pointer)
    * 数组
    * 结构体(struct)
    * Channel
    * 函数(func)
    * 切片
    * 接口(interface)
    * map

Go 变量的声明和初始化：

```go
/*声明时初始化*/
var identifier type = value

/*声明后初始化*/
var identifier type
identifier = value
```



# 进阶

# 数据结构