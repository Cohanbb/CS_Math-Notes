# Pure C

C 语言是一个系统级的高级程序设计语言，与 Java 一样是需要编译执行的语言，Java 虚拟机、CPython 解释器以及 GNU/Linux Kernel 的大部分内容都由 C 语言编写，故 C 语言是最接近底层的高级语言。

C 语言编译执行的过程：

1. 预处理

对源程序进行预处理替换，呈现出完整的程序。

**.c file** $\longrightarrow$ **.i file**

2. 编译

将预处理后的程序编译成汇编程序。

**.i file** $\longrightarrow$ **.s file**

3. 汇编

将汇编程序转换为机器指令。

**.s file** $\longrightarrow$ **.o file**

4. 链接

链接库文件并生成可执行文件。


## 预处理和宏定义

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

C 语言的基本数据类型，在 32 位或 64 位编译器下：

|类型|存储字节|范围|
|--|--|--|
| int | 4 | [-2<sup>31</sup>, 2<sup>31</sup> - 1] |
| unsigned int | 4 | [0, 2<sup>32</sup> - 1] |
| short int | 2 | [-2<sup>15</sup>, 2<sup>15</sup> - 1] |
| unsigned short | 2 | [0, 2<sup>16</sup> - 1] |
| long int | 4 或 8 | [-2<sup>31</sup>, 2<sup>31</sup> - 1] 或 [-2<sup>63</sup>, 2<sup>63</sup> - 1] |
| unsigned long | 4 或 8| [0, 2<sup>32</sup> - 1] 或 [0, 2<sup>64</sup> - 1] |
| char | 1 | [-128, 127] 或 [0, 255] |
| unsigned char | 1 | [0, 255] |
| signed char | 1 | [-128, 127] |
| float | 4 | [1.2E-38, 3.4E+38] 精度 6 或 7|
| double | 8 | [2.3E-308, 1.7E+308] 精度 15 或 16|
| long double | 8 或 12 或 16| 略|

这些数据类型是如何存储的？为什么不同数据类型的存储字节数不同？学习 [组成原理_数据的表示与运算]()

```c
int a = 100; // 十进制 100
int b1 = 100u; // 无符号 100
int b2 = 100U; // 无符号 100
int b3 = 100l; // 长整数 100
int b4 = 100L; // 长整数 100
int b5 = 100ul; // 无符号长整数 100
int c1 = 077; // 八进制 77
int c2 = 0xFF; // 十六进制 FF
int c3 = 0XFF; // 十六进制 FF

float d1 = 3.1415;
float d2 = 31415E-5;
float d3 = 31415e-5; 

char e1 = 'a'; // 字符 a
char e2 = 97; // 字符 a 的 ASCII 码
```

## 变量和常量

* 变量的作用域：变量可以被使用的范围，如果在外部定义，则作用域为全局，如果在局部代码块内定义，则作用域为块作用域。

* 变量的生存期：变量在程序执行过程中的存留时间。

四种存储类型：

* `auto` 类型，局部变量的默认类型，存储在内存中的栈区，作用域和生存期都在局部代码块内。

* `register` 类型，存储在 CPU 寄存器而不是内存中的局部变量，一般用于存储使用频率高的变量。
  
  > 要注意的是由于机器字长的限制，只推荐将一些存储位数少的类型声明为 register 类型，如 char、short、int。

* `static` 类型，存储在内存中的静态存储区，如果修饰局部变量，则该局部变量变为静态局部变量，在整个程序的生命周期保持存在，不会因进出作用域而创建和销毁。如果修饰全局变量，则会将变量的作用域限制在文件内。

* `extern` 类型，可以理解为在其他文件中声明了一个全局变量或函数，要在本文件中使用这个全局变量或函数，一般用于多个文件共享一个全局变量或函数。

变量的声明和定义：

```c
/*
 * 变量的声明：
 * (store_type) data_type indentifier;
 */
int a;
auto int b;

/*
 * 变量的初始化：
 * 1.(store_type) data_type indentifier = value;
 * 2.(store_type) data_type indentifier(value);
 */
 auto int c = 1；
 auto int d(2);
```

常量的定义：

```c
/*
 * 1.使用 #define
 * #define identifier value
 */
#define LENGTH 100

/*
 * 2.使用 const
 * const data_type identifier = value;
 */
 const int WIDTH = 50;
```

## 运算符和表达式

## 语句结构

### 选择结构

```c
/* if-else 型 */
if (/* condition1 */) {
    /* operation */
} else if (/* condition2 */) {
    /* operation */
} else {
    /* operation */
}

/* switch-case 型 */
switch (/* identifier or expression */) {
    case /* value */:
        /* operation */
    case /* value */:  
        /* operation */
    /*
     * ......
     */
    break;
    default:
        /* operation */
}
```

除此之外还可以使用三目运算符 `?:` 来表示选择结构：

```c
/* condition */ ? /* operation1 */ : /* operation2 */;
```

若 condition 为真，则执行 operation1，否则执行 operation2。

### 迭代结构

```c
/* while 型 */
while (/* condition */) {
    /* operation */
}

/* do-while 型 */
do {
    /* operation */
} while (/* condition */)

/* for 型 */
for (/* init_expression */; /* condition */; /* end_operation */) {
    /* mid_operation */
}
```

## 函数

C 语言是需要编译的语言，程序中函数在被调用之前必须声明。

```c
/*
 * 函数的声明
 * (extern) return_type func_identifier(parameter_list);
 * 函数在声明时候参数列表可以只写数据类型
 */
 int Add(int);


/*
 * 函数的定义：
 * return_type func_identifier (parameter_list) {
 *     operation
 * }
 */
int Add(int a) {
    return ++a;
}
```

### 函数传参

函数的参数列表中的参数叫做形式参数，形式参数可以使用：

1. 变量
2. 指针

### 函数调用栈帧




## 数组

### 一维数组

```c
/*
 * 数组的声明
 * data_type identifier[array_length];
 */
 int a[10];
 
 /*
  * 数组的初始化
  * data_type identifier[] = {value_list};
  */
  int b[5] = {1, 2, 3, 4, 5};
```

### 多维数组

### C_Style String

## 指针

## 自定义数据类型

### 枚举类型

```c
/*
 * 枚举的定义：
 * enum identifier {
 *     element1,
 *     element2,
 *     ......
 * };
 */
enum week {
    Monday=1,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday,
    Sunday
};
```

### 结构体类型

```c
/* 
 * 结构体的定义：
 * struct identifier {
 *     member_list
 * };
 */
struct Students {
    char sex;
    int age;
    char name[10];
};

/*
 * 也可以不定义结构体标识符的直接定义结构体变量
 * struct {
 *     member_list
 * } identifier;
 */
struct {
    char sex;
    int age;
    char name[10];
} Allen, Bob;
```

### 共用体类型

共用体是特殊的结构体，允许在相同的内存位置存储不同的数据类型，只有一个成员是带有值的。

## IO


## 内存管理

