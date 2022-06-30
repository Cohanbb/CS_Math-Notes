# C++11/14/17/20 新特性

## C++11

### long long int 类型

C++11 中引入了 long long int（简称 long long）数据类型，规定该数据类型至少不小于 long int 数据类型。

### nullptr 空指针

>在 C 语言中 `NULL` 被定义为 `((void *)0)`，而在 C++ 中 `NULL` 仅仅被定义为 `0`，所以当一个空指针作为函数参数时会被认为是一个 int 型参数。

`nullptr` 用来表示一个不指向任何内容的空指针 `(void *)`，且不会被转换成整数类型，而是被视作一个基础类型 `std::nullptr_t`。

### auto & decltype 类型指示符 

C++11 允许声明一个变量或对象而不需要声明数据类型，只需要在前面声明 `auto`，并进行初始化，其类型会根据初始值被自动推导出来。

```cpp
/*
 * auto identifier = value;
 * 根据 value 自动推导数据类型
 */
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
/*
 * decltype(statement) identifier = value; 
 * 根据 statement 来设置数据类型
 * statement 可以是变量、常量、表达式、函数名
 */
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
/*
 * for (declare : range) {
 *     operation
 * }
 */
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



## C++14

## C++17

## C++20
