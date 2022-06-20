[TOC]

# Pure C

## 宏定义和预处理

```c
#include 

#define

#if

#ifdef

#ifndef

#endif

#error

#progma
```

## 基本数据类型

C 语言有 8 种基本数据类型：

* int：整数型
* unsigned int：无符号整数型
* short int：
* long int：
* float：单精度浮点数型
* double：双精度浮点数型
* long double：
* char：字符型
* long char：

```c
int a = 100;   //十进制 100
int b1 = 100u; //
int b2 = 100U; //
int b3 = 100l; //
int b4 = 100L; //
int c1 = 077;  //八进制 77
int c2 = 0xFF; //十六进制 FF
int c3 = 0XFF; //十六进制 FF

```

## 变量和常量

## 运算符和表达式

## 语句结构

### 选择结构

```c
if () {

} else if () {

} else {

}

switch() {
    case
    break;
    default
}
```

### 循环结构

```c
while () {

}

do {

} while ()

for ( ; ; ) {

}
```

## 函数

```c
<返回类型> <函数名称>([形式参数列表]) {
    /*函数体*/
}

/*for instance*/
void func(int a) {
    printf("%d\n", a);
}
```

### 函数传参


### 函数调用栈帧


## 数组

### 一维数组

```c
<数据类型> <数组名>[<元素个数>]
```

### 多维数组

```c

```

## 指针


## 自定义数据类型

### 枚举类型

```c

```

### 结构体类型

```c

```

### 共用体类型

```c

```

## 内存管理

### 

### 函数栈帧

### 栈溢出

### 堆溢出


# C++

## 内联函数

## 异常处理

## 引用数据类型

## 命名空间

```cpp
namespace {

}
```

## 类和对象

```cpp
class <类名> {
    /*成员*/
    
    /*成员函数*/

    /*构造函数*/

    /*析构函数*/
}

/*for instance*/
class Student {
    private int age;
    private int age;
    private int age;
    
    Student() {
    
    }
    
    ~Student() {
    
    }
}
```

## 继承和派生

## 多态

## 运算符重载

## 输入输出流

## 内存管理

## String 类


# STL

## 容器

## 算法


# 开发工具

## GCC

## GDB

## make