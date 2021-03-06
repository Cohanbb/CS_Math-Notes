# C++

C++ 同样诞生于贝尔实验室，最初的目的是将 C 改良为“带类的 C”（然而现在远远不仅如此），1983 年正式命名为 C++。1998 年，ANSI/ISO 发布了 C++ 标准以及标准模板库 STL。

于 2003 年对 C++98 进行了漏洞的修复，并于 2011 年、2014 年、2017 年和2020 年相继推出了新的 C++ 标准。

本文的内容基于 C89、C++03 和部分 C++11，其中面向过程部分仅阐述了 C++03 与 C89 的差异和新特性。所有代码均使用 GCC 编译。

## C++ 与 C89 的差异和新特性

### 内联函数

内联函数，在函数定义时前面加上 `inline` 即表明该函数为内联函数。

### new & delete 关键字

C++ 新增了 `new` 和 `delete` 关键词用于动态管理内存，对应的功能就像 C 语言中的 `malloc` 和 `free`。

### 新增基本数据类型

1. bool 型

`bool` 型即布尔数据类型，用来表示 `true` 或 `false`，占一个字节。

* `bool` 型转 `int` 型，`true` 转化为 1，`false` 转化为 0。
* `int` 型转 `bool` 型，0 转化为 `false`，任何非零整数转化为 `true`。 

2. wchat_t 型（C99 标准也加入）

在 C++ 中宽字符型 `wchar_t` 是一种基本数据类型，而 C 语言中是通过 `typedef unsigned int wchar_t` 实现。

3. C++11 引入 long long int 型（C99 标准也加入）

### 变量初始化方式

1. =
2. ()
3. C++11{}

### 强制类型转换

C 语言中强制类型转换的安全性不够高，C++ 对此做出了改进。

### 引用数据类型

C++ 中引入了引用数据类型

引用类型作函数参数

引用类型作函数返回值

### try 语句块和异常处理

```cpp

```

### 函数的改进

C++ 在 C 语言基础上对函数进行了改进和扩展，提高了函数的安全性、便捷性和可扩展性。

1. 函数参数列表

C 语言在声明函数原型时可以不指出参数列表，而 C++ 不可，但可以使用 `...` 省略。

```cpp
void f(...);

void f(int a, int b) {
    std::cout << a + b << std::endl;
}
```

2. 函数参数缺省

C 语言中函数参数不可以设置默认值，C++ 可以设置参数的默认值，如果参数缺省，则使用默认值。

使用默认值的规则是：在函数声明时从右至左逐个设置默认值，如：

```cpp
int f(int a = 1, int b = 2, int c =3);
int f(int a, int b = 2, int c =3);
int f(int a, int b = 2, int c); // Invalid

int f(int a, int b, int c) {
    return a + b + c;
}

int main() {
    int n = f();
}
```

3. 函数返回值缺省

C 语言中函数的返回值可以缺省，默认返回 `int` 型，但在 C++ 中不可以缺省，必须规定返回值类型。

4. 函数重载

C 语言不支持函数的重载，C++ 支持。

5. 引用类型作为函数参数或返回值

## 命名空间

```cpp
namespace {

}
```

## C++ 结构体

## 类和对象

```cpp
// class class_identifier {
//     member_list    
//     member_functions
// };
class Student {
    private int age;
    public int age;
    protected int age;
    
    protected void func();
    
    Student();
    
    ~Student();
};
```

## 继承和派生

## 多态

## 运算符重载

## I/O 类

## String 类

String 是 C++ 风格的字符串。

## 模版

### 函数模版

### 类模版

## 容器

### 序列容器

#### Array

#### String

#### Vector

#### Deque

#### List

#### Forword List

### 关联容器

#### Set & Multiset

#### Map & Multimap

### 容器适配器

#### Stack

#### Queue

#### Priority Queue

## 算法

## 迭代器

## C++11 新特性

### long long int 类型

C++11 中引入了 long long int（简称 long long）数据类型，规定该数据类型至少不小于 long int 数据类型。

### nullptr 空指针

>在 C 语言中 `NULL` 被定义为 `((void *)0)`，而在 C++ 中 `NULL` 仅仅被定义为 `0`，所以当一个空指针作为函数参数时会被认为是一个 int 型参数。

`nullptr` 用来表示一个不指向任何内容的空指针 `(void *)`，且不会被转换成整数类型，而是被视作一个基础类型 `std::nullptr_t`。

### auto & decltype 类型指示符 

C++11 允许声明一个变量或对象而不需要声明数据类型，只需要在前面声明 `auto`，并进行初始化，其类型会根据初始值被自动推导出来。

```cpp
// auto identifier = value;
// 根据 value 自动推导数据类型
auto a = 100; // a 为 int 型
float b;
auto c = b; // b 为 float 型
```

使用 `auto` 的注意事项：

1. 在一个语句中声明多个变量或对象，这些变量或对象的数据类型必须一样。

```cpp
auto a = 1, b = 1.5; // 错误写法
```

2. 无法推导为 `const` 类型

```cpp
const int a = 1;
auto b = a; // b 被推导为 int 型变量，而不是常量
```

3. 无法推导为引用数据类型

```cpp
int a = 1, &b = a;
auto c = b; // c 被推导为 int 类型，而不是 int &
```

由于 `auto` 功能的限制，因此 C++11 又引入了 `decltype` 机制。

```cpp
// decltype(statement) identifier = value; 
// 根据 statement 来设置数据类型
// statement 可以是变量、常量、表达式、函数名
const int a = 1, &b = a, *c = &a;
decltype(a) d = 1; // d 为 const int 型
decltype(b) e = 1; // e 为 const int & 型
decltype(c) f = 1; // f 为 const int * 型

decltype(expr) g = 1; // g 的类型为 expr 的值的类型
decltype(func) h = 1; // h 的类型为 func 返回值的类型
```

### tuple 元组

`tuple` 是一个特殊的数组，里面的元素可以为不同的数据类型。

### 区间 for 循环

C++11 引入了一种新的 `for` 循环，可以逐一迭代某个给定的范围（如数组）内的每一个元素。

```cpp
// for (declare : range) {
//     operation
// }
for (int i : {1, 2, 3, 4, 5}) {
    std::cout << i << std::endl;
}
```

### Lambda

C++11 最重要的特性之一：`lambda`，允许内联函数的定义式被用作一个参数，或一个 local 对象。

### 移动赋值运算符和移动构造函数

移动语义也是 C++11 最重要的特性之一。

### override & final

### defaulted & deleted

### 模版别名

### initializer_list

### 右值引用

### 委托构造和继承构造

### noexpect

C++11 中引入了一个关键词 `noexpect` 用来指明某个函数无法抛出异常。

### constexpr

`constexpr` 关键词可以用来让表达式核定于编译期。

### alignof & alignas

### 带领域的枚举

### 非受限的联合体 union
