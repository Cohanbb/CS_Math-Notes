<p align="center">
	<font size="6" >
	<strong>
	PHP__A Basic Start
	</strong>
	</font>
</p>

# 摘要

PHP(Hypertext Preprocessor)超文本预处理器，一种开源的、常运行在服务器上的开源脚本语言，它跨平台、与几乎所有 Web 服务器兼容、与大量的数据库兼容。  
PHP 文件可以包含 PHP 代码、HTML 和 JavaScript 代码，在服务端执行，与数据库进行交互后生成 HTML 文件通过 Web 服务器返回给浏览器。

<hr>

**本文索引**

- [摘要](#摘要)
- [基本形式](#基本形式)
- [PHP 基础语法](#php-基础语法)
  - [常变量和数据类型](#常变量和数据类型)
    - [PHP 数据类型](#php-数据类型)
    - [PHP 常量](#php-常量)
    - [PHP 变量及全局变量](#php-变量及全局变量)
    - [PHP 字符串](#php-字符串)
    - [PHP 数组](#php-数组)
  - [语句](#语句)
    - [选择语句](#选择语句)
    - [循环语句](#循环语句)
  - [函数](#函数)
- [PHP 进阶](#php-进阶)
  - [PHP 面向对象](#php-面向对象)
  - [PHP HTTP](#php-http)
    - [HTTP](#http)
    - [GET 和 POST](#get-和-post)
    - [Cookie 和 Session](#cookie-和-session)
  - [PHP 操作数据库](#php-操作数据库)
  - [PHP 文件包含](#php-文件包含)
  - [PHP 文件读写](#php-文件读写)
  - [PHP 文件上传](#php-文件上传)
  - [PHP 命令执行](#php-命令执行)
  - [PHP 过滤器](#php-过滤器)

<hr>

# 基本形式

一个 PHP 文件通常包含 HTML 和 PHP 脚本，基本形式为：

```php
<!DOCTYPE html>
<html>
<body>
    <?php
        echo "Hello World!";
    ?>
</body>
</html>
```

# PHP 基础语法

## 常变量和数据类型

### PHP 数据类型

与 C/C++、Java、C#、Go 这些强类型语言不同，PHP 是一种弱类型语言，PHP 有 8 种数据类型：

* Integer：整数型
* Float：浮点数型
* String：字符串型 
* Boolean：布尔型
* Array：数组
* Object：对象
* Null：空
* Resource：资源型

各种变量的定义方式：

```php
<?php
    /* 整型 */
    $a = 1;
    
    /* 浮点型 */
    $b1 = 1.1;
    $b2 = 9.9e-10;
    $b3 = 5E-10;
    
    /* 字符串 */
    $c = "PHP";
    
    /* bool 型 */
    $d1 = TRUE;
    $d2 = FALSE;
    
    /* 数组 */
    $e = array("I", "LOVE", "YOU"); 
    
    /* 类与对象 */
    class F {
        ......
    }
    $f = new F;
    
    /* Null */
    $g = null;
    
    /* resource 型 */
    $h1 = mysqli_connect(...);
    $h2 = fopen(...);
?>
```

由于 PHP 是弱类型语言，故 PHP 有两种比较方式：

* 松散比较：使用两个等号 `==` 进行比较，只比较值，不比较数据类型。
* 严格比较：使用三个等号 `===` 进行比较，既比较值，又比较数据类型。

```php
<?php
    if (TRUE == "TRUE") {
        echo "相等1";
    } else if (TRUE === "TRUE") {
        echo "相等2";
    }
    // 将输出：相等1
?>
```

### PHP 常量

PHP 常量的定义需要使用 `define()` 函数，函数用法为：

```php
<?php
    bool define(string $name, mixed $value [, bool $case_insensitive = false])
    /* $name 为常量名，$value 为常量值，$case_insensitive 表示常量名是否大小写不敏感 */

    define("A", "123", TRUE);
    echo a;
    echo A; 
    /* 将输出两次 123
     * 若没有设置为大小写不敏感，则 echo a 将报错
     */
?>
```

### PHP 变量及全局变量

PHP 一个变量需要在变量名前加上符号 `$`，变量名是区分大小写的，例如：

```php
<?php
    $x = 7;
    $y = 7.7;
    $zz = "Hello PHP!";
    $ZZ = "Hi PHP!"
?>
```

PHP 在局部使用全局变量：

1. 使用 global 关键字声明全局变量，如：
    
    ```php
    <?php
        $a = 5;
        $b = 10;
        
        function Maxab() {
            global $a, $b; // 声明使用全局变量 a 和 b
            if ($a >= $b) {
                return $a;
            } else { 
                return $b;
            }
        }
    ?>
    ``` 
    
2.  使用 `$GLOBALS` 超级全局变量数组直接调用变量，如：
    
    ```php
    <?php
        $a = 5;
        $b = 10;
        
        function Maxab() {
            if ($GLOBALS["a"] >= $GLOBALS["b"]) {
                return $GLOBALS["a"];
            } else { 
                return $GLOBALS["b"];
            }
        }
    ?>
    ```

`$GLOBALS` 是包含了全部变量的数组，除了 `$GLOBALS` 之外，PHP 还有几个超级全局变量：

1. `$_SERVER`：存储服务器信息和执行环境。
2. `$_REQUEST`：收集 HTML 表单提交的数据，包括 get 和 post 方式提交的数据以及 cookie。
3. `$_POST`：收集 HTML 表单使用 post 方式提交的数据。
4. `$_GET`：收集 HTML 表单使用 get 方式提交的数据，或 URL 提交的数据。
5. `$_FILES`：存储上传文件的信息。
6. `$_ENV`：存储服务器的环境变量。
7. `$_COOKIE`：存储 cookie 信息。
8. `$_SESSION`：存储 session 信息。

### PHP 字符串

PHP 中需掌握三种字符串操作：

1. 并置运算符 `.` 用于连接两个字符串，如： 
  
    ```php
    <?php
        $str1 = "Hel";
        $str2 = "leo";
        echo $str1 . $str2; // 将输出 Hello
    ?>
    ```
    
2.  `strlen()` 函数，同 C 语言，返回字符串的长度。
3.  `strpos()` 函数，在字符串内查找一段文本，若查找到会返回该文本第一次出现的位置，若未查找到则返回 `FALSE`，如：
    ```php
    <?php
        echo strpos("Hello Hello", "Hello");
    ?>
    ```

字符串既可以用单引号也可以用双引号，二者的主要区别：

1. 双引号可以解释变量，单引号不解释变量。
2. 单引号的解析速度更快。

### PHP 数组

PHP 中数组类型：

1. 数值数组：带有数字键值的数组，键值为从 0 开始的数字。
2. 关联数组：自定义键值的数组。
3. 多维数组：多维度的数组。

定义方式如下：

 ```php
 <?php
     /* 数值数组 */
     $a = array("1", "2", "3");
     echo a[0];
     echo a[1];
     echo a[2];
     foreach ($a as $value) {
         echo $value;
     }

    /* 关联数组 */
    $b = array("a" => "1", "b" => "2", "c" => "3");
    echo b['a'];
    echo b['b'];
    echo b['c'];
    foreach ($b as $x => $x_value) {
        echo $x;
        echo "<br />";
        echo $x_value;
    }

    /* 多维数组 */
    $c = array(
        "c1" => array(
            array("1", "2", "3"),
            array("4", "5", "6")
        ),
        "c2" => array(
            array("7", "8", "9"),
            array("10", "11", "12")
        )
    )
?>
 ```

常用函数：

* `count()`：可以返回数组的长度。
* `sort()`：进行升序排序。
* `rsort()`：进行降序排序。
* `asort()`：根据关联值进行升序排序。
* `ksort()`：根据关联键值进行升序排序。
* `arsort()`：根据关联值进行降序排序。
* `krsort()`：根据关联键值进行降序排序。

## 语句

###  选择语句

PHP 中的选择语句与 C 语言完全相同，使用 `if-else` 语句或 `switch-case` 语句。

```php
<?php
    /* if-else 语句 */
    if (/* condition1 */) {
        /* operation */
    } else if (/* condition2 */) {
        /* operation */
    } else {
        /* operation */
    }

    /* switch-case 语句 */
    switch (/* identifier or expression */) {
        case /* value1 */: 
            /* operation */
        case /* value2*/: 
            /* operation */
        /* 
         * ...... 
         */
        break;
        default:
            /* operation */
    }
?>
```


### 循环语句

PHP 中的循环语句在 C 语言提供的 `while`、`do while`、`for` 的基础上又提供了一种 `foreach`。

```php
<?php
    /* while 型 */
    while (/* condition */) {
        /* operation */
    }

    /* do-while 型 */
    do {
        /* operation */
    } while (/* condition */)

    /* for 型 */
    for (/* initializing */; /* condition */; /* addition */) {
        /* operation */
    }

    /* foreach 型用于遍历数组 */
    $a = array ("1", "2", "3");
    foreach ($a as $value) {
        echo $value;
    } // 将输出 123
?>
```

## 函数

PHP 内建了大量的函数，功能强大，在下文会列举几个关键函数。  

PHP 是脚本语言，直接由 PHP 解释器解释执行，不需要进行编译，故函数可以在代码中的任意位置定义，不需要在调用前进行声明，函数的定义方法：

```php
<?php
    function function_name(parameter_list) {
        /* operation */
        return ... ; // 返回值    
    }
?>
```

# PHP 进阶

## PHP 面向对象

PHP 面向对象的使用方法与 C++ 类似：

```php
<?php
class php_class {
    /* 成员变量 */
    public $var1;
    // var $var1;
    protected $var2;
    private $var3;
    
    /* 构造函数 */
    function __construct($par1, $par2) {
        $this->var1 = $par1;
        $this->var2 = $par2;
    }
    
    /* 析构函数 */
    function __destruct() {
        echo "销毁对象" . this->name;
    }
    
    /* 成员函数 */
    function fun($par) {
        echo $par;   
    }
}

/* 声明对象 */
$obj = new php_class(1, 2);

/* 调用成员函数 */
$obj -> fun(1);

/* 继承 */
class child_class extends php_class {
    /* 代码 */
}

/* 接口 */
// 声明接口
interface A {
    public function fun(parameter_list);
}

// 实现接口
class a implements A {
    public function fun(parameter_list) {
        /* operation */
    } 
}

/* 抽象类 */
// 定义抽象类
abstract class B {
    abstract protected function fun1(parameter_list);
    public function fun2();
}

class b extends B {
    protected function fun1(parameter_list) {
        /* operation */
    }
}
?>
```

## PHP HTTP

### HTTP

使用 `header()` 函数向浏览器发送 HTTP 报头，函数原型为：

```php
<?php
    header(string, replace, http_response_code)
    /* string 表示要发送的报头字符串
     * replace 表示是否代替原来的报头，默认 TRUE
     * http_response_code 可选，表示把 HTTP 响应强制为指定的值
     */
?>
```

例如想要在新的页面定向到某个 URL：

```php
<?php
    header("Location: https://cohanbb.github.io/", FALSE);
?>
```

### GET 和 POST

`$_GET[]` 和 `$_POST[]` 两个数组分别用来收集 HTML 使用 get 和 post 方式提交的数据。

例如想要收集 get 方式提交的数据 DEMO:

```php
/* demo.php */
<html>
    <form action="demo.php" method="get">
        <input type="text" name="DEMO"/>
        <input type="submit" name="submit" value="submit"/>
    </form>
</html>
<?php
    $demo = $_GET["DEMO"];
    echo $demo;
?>
```

### Cookie 和 Session

何谓 Cookie？

> cookie 常用于识别用户，cookie 是一种服务器留在用户计算机上的小文件。每当同一台计算机通过浏览器请求页面时，这台计算机将会发送 cookie。

PHP 使用 `setcookie()` 函数设置 cookie：

```php
<?php
    /* 函数原型 */
    setcookie(name, value, expire, path, domain);
    
    /* 设置 cookie 并于 3600 秒后过期 */
    setcookie("user", "Cohanbb", time() + 3600);
?>
```

`$_COOKIE_` 存储设置的 cookie 值：

```php
<?php
    echo $_COOKIE["user"];
?>
```

删除 cookie：

```php
<?php
    /* 将时间设为过去的时间即可删除 cookie */
    setcookie("user", "", time() - 1); 
?>
```

何谓 Session？

> 在计算机上操作某个应用程序时，打开它、做些更改、关闭它，这很像一次对话。你所操作的计算机知道你是谁，它清楚你在何时打开和关闭应用程序。然而由于 HTTP 地址无法保持状态，Web 服务器并不知道你是谁以及你做了什么。  
> session 解决了这个问题，它通过在服务器上存储用户信息以便随后使用（比如用户名称、购买商品等）。会话信息是临时的，在用户离开网站后将被删除。如果需要永久存储信息，可以把数据存储在数据库中。  
> session 的工作机制是：为每个访客创建一个唯一的 id (UID)，并基于这个 UID 来存储变量。UID 存储在 cookie 中，或者通过 URL 进行传导。

PHP 操作 session：

```php
<?php
    session_start();

    /* 设置 session */
    $_SESSION["name"] = "Cohanbb";
    
    /* 获取 session */
    $name = $_SESSION["name"];
    
    /* 清空 session */
    session_unset();
    
    /* 销毁 session */
    session_destroy();
?>
```

## PHP 操作数据库

PHP 通过 `MySQLi` 或 `PDO` 连接和操作数据库，`PDO` 可以应用在12种不同的数据库，`MySQLi` 只能应用在 MySQL 数据库，在此仅演示 `MySQLi`。

`MySQLi` 可以面向过程也可以面向对象，写法上有一些差异。   

**连接数据库**  
使用 `mysqli_connect()` 函数连接数据库，或面向对象：

```php
<?php
    /* 面向过程*/
    $conn = my sqli_connect("localhost", "root", "123456");
    if (!$conn) {
        die("数据库连接失败：" . mysqli_connect_error()));
    }
    echo "数据库连接成功";
    mysqli_close($conn);
    
    /* 面向对象 */
    $conn = new mysqli("localhost", "root", "123456");
    if ($conn->connect_error) {
        die("数据库连接失败：" . $conn->connect_error);
    }
    echo "数据库连接成功";
    $conn->close();
?>
```

**使用 SQL 语句**    
使用 `mysqli_query()` 函数连接 SQL 语句，或面向对象：

```php
<?php
    /* 面向过程 */
    $sql = "SELECT * FROM users";
    if (!mysqli_query($conn, $sql)) {
        die("查询失败");
    }

    /* 面向对象 */
    $sql = "SELECT * FROM users";
    if (!($conn->query($sql))) {
        die("查询失败");
    }
?>
```

**其他常用函数**   

* 使用 `mysqli_error()` 函数返回最近调用函数的最后一个错误的描述。
* 使用 `mysqli_errno()` 函数返回最近调用函数的最后一个错误代码。
* 使用 `mysqli_affected_rows()` 函数返回上一个 SQL 语句影响的行。  
* 使用 `mysqli_real_escape_string()` 函数转义 SQL 语句中的特殊字符，可用于防注入。  
* 使用 `mysqli_fetch_xxx()` 函数从查询结构中返回一些数据：

    - `mysqli_fetch_all()` 从结果集中取得所有行作为关联/数值数组  
    - `mysqli_fetch_array()` 从结果集中取得一行作为关联/数值数组  
    - `mysqli_fetch_assoc()` 从结果中取得一行作为关联数组  
    - `mysqli_fetch_object()` 从结果中取得一行作为对象  

## PHP 文件包含

PHP 有四种文件包含方式：

* `include`
* `include_once`
* `require`
* `require_once`

其中 `include` 和 `require` 的区别是，二者处理错误的方式不同，前者生成一个警告，出错后脚本继续执行，后者生成一个致命错误，脚本停止执行。  
后面带上 `_once` 的作用是如果之前已经包含了该文件，则不会再次包含，即防止多次包含同一个文件。
  
常用文件包含语句：

```php
<?php
    /* 普通方式包含 */
    include "file.php";
    require "file.php";
    include_once "file.php";
    require_once "file.php"; 

    /* get 方式传参包含 */
    $file = $_GET["FILE"];
    include($file);
    require($file);
?>
```

## PHP 文件读写

PHP 中使用 `fopen()` 函数打开文件，`fwrite()` 函数写入文件，`fclose()` 函数关闭文件，用法如下：

```php
<?php
    $file = fopen("test.txt", "r"); // 以只读方式打开 test.txt 文件
    $str = "123";
    fwrite($file, "str");
    fclose($file);
?>
```

`fopen()` 函数第二个参数表示打开文件的模式：

|Patterns|Descriptions|
|--|--|
|r|只读，从文件开头开始。|
|r+|读写，从文件开头开始。|
|w|只写，且清空文件内容，若文件不存在则新建。|
|w+|读写，且清空文件内容，若文件不存在则新建。|
|a|只写，从文件末尾进行追加，若文件不存在则新建。|
|a+|读写，从文件末尾进行追加，若文件不存在则新建。|
|x|只写，创建一个新文件，若文件已存在则返回 FALSE 并报错。|
|x+|读写，创建一个新文件，若文件已存在则返回 FALSE 并报错。|

## PHP 文件上传

PHP 使用 `$_FILES` 超级全局变量进行文件上传，`$_FILES` 是一个二维数组，结构如下：

```php
$_FILES = array(
    /* 假设 filename 为 HTML 表单中 <input "name" /> 的值 */
    "filename" => array(
        "name" => 被上传的文件名称
        "type" => 被上传的文件类型
        "tmp_name" => 被上传的文件在服务器中暂时的路径和名称
        "error" => 上传过程有无错误
        "size" => 被上传文件的大小
        )
);
```

在此我给出一个简单的文件上传程序：

```html
<html>
    <body>
        <form action="upload.php" method="post">
            <label>请上传文件：</label>
            <input type="file" name="filename" />
            <br />
            <input type="submit" name="submit" value="确认上传" />
        </form>
    </body>
<html>
```
```php
upload.php
<?php
    /* 限制上传文件的类型和大小 */
    if ((($_FILES["filename"]["type"] == "image/gif") 
      || ($_FILES["filename"]["type"] == "image/jpeg") 
      || ($_FILES["filename"]["type"] =="image/pjpeg")) 
      && ($_FILES["filename"]["size"] < 20000)) {
        if ($_FILES["filename"]["error"]) {
            echo "错误：" . $_FILES["filename"]["error"] . "<br />";
        } else {
            /* 输出上传的文件信息 */
            echo "文件名：" . $_FILES["filename"]["name"] . "<br />";
            echo "文件类型：" . $_FILES["filename"]["type"] . "<br />";
            echo "文件大小" . ($_FILES["filename"]["size"] / 1024) . "Kb<br />";
            echo "文件副本：" . $_FILES["filename"]["tmp_name"] . "<br />";
            /* 将文件存储在服务器 */
            if (file_exists("upload/" . $_FILES["filename"]["name"])) {
                echo $_FILES["filename"]["name"] . "已经存在";
            } else {
                move_uploaded_file($_FILES["filename"]["tmp_name"], "upload/" . $_FILES["filename"]["name"]);
                echo "文件存储在" . "upload/" . $_FILES["filename"]["name"];
            }
        }
    } else {
        echo "无法上传该文件";
    }
?>
```

## PHP 命令执行

PHP 调用系统命令函数：

* `system()`：执行系统命令，输出执行结果。
* `passthru()`：与 `system()`函数相似。
* `exec()`：执行系统命令，无回显，返回最后一行结果。
* `shell_exec()`：执行系统命令，返回完整的输出结果。
* `popen(command, mode)`：command 为执行的命令，mode 规定连接模式，可以是 r（只读）、w（只写）等。
* `proc_open()`：不直接返回执行结果，返回一个文件指针。
* `pcntl_exec()`：执行发生错误返回 FALSE，无错误不返回。

命令执行的例子：

```php
<?php
    $ip = $_GET["ip"];
    $command = "ping -c 3 $ip";
    system("$command");
?>
```

## PHP 过滤器

以网络安全为目的，常在 PHP 程序中使用 `Filter` 函数对外部数据进行过滤，外部数据指表单提交的数据、cookie、Web 服务器信息、数据库查询结果等。   

常用的过滤函数：

* `filter_var()`：对单一的变量使用指定过滤器过滤。
* `filter_var_array()`：对多个变量使用多个过滤器过滤。
* `filter_input()`：获取一个表单输入的内容，并指定过滤器进行过滤。
* `filter_input_array()`：获取多个表单输入的内容，并通过多个过滤器进行过滤。

下面的例子使用 `filter_var()` 进行过滤：

```php
<?php
    $int = 777;
    if (!filter_var($int, FILTER_VALIDATE_INT)) {
        echo "不是合法的整数";
    } else {
        echo "是合法整数";
    }
?>
```
