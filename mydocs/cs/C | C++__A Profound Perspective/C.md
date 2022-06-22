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
