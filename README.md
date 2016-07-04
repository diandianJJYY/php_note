# 7月2日 总结
### 类型

#### 1. 标量类型：

> * boolean（布尔型）
> * integer（整型）
> * float（浮点型，也称作 double)
> * string（字符串）

两种复合类型：
> * array（数组）
> * object（对象）


最后是两种特殊类型：
> * resource（资源）
> * NULL（无类型）

------

#### 2.变量

###### 变量命名
> * 变量名区分大小写 \$var 与 \$Var 不同
> * 变量名不能以数字开头

###### 变量赋值
引用赋值：下列代码片断将输出“My name is Bob”两次：
```php
<?php
$foo = 'Bob';              // 将 'Bob' 赋给 $foo
$bar = &$foo;              // 通过 $bar 引用 $foo
$bar = "My name is $bar";  // 修改 $bar 变量
echo $bar;
echo $foo;                 // $foo 的值也被修改
?>
```
###### 变量范围

```php
<?php
$a = 1; /* global scope */

function Test()
{
    echo $a; /* reference to local scope variable */
}

Test();
?>
```
上面代码的运行结果：
> * Notice: Undefined variable: a in D:\wamp\www\test.php on line 6

提示 \$a未定义，正确做法在 \$a 前加上个 global

------

#### 3.预定义变量
常见的预定义变量：
> * \$_SERVER — 服务器和执行环境信息
> * \$_GET — HTTP GET 变量
> * \$_POST — HTTP POST 变量
> * \$_FILES — HTTP 文件上传变量
> * \$_REQUEST — HTTP Request 变量
> * \$_SESSION — Session 变量
> * \$_COOKIE — HTTP Cookies

例子：获取文件路径
> * \$_SERVER['PHP_SELF'];

------

#### 4.常量
###### 4.1 语法

可以用 define() 函数来定义常量，在 PHP 5.3.0 以后，可以使用 const 关键字在类定义之外定义常量。一个常量一旦被定义，就不能再改变或者取消定义。
常量只能包含标量数据（boolean，integer，float 和 string）。可以定义 resource 常量，但应尽量避免，因为会造成不可预料的结果。

常量和变量有如下不同：
> * 常量前面没有美元符号（$）；
> * 常量只能用 define() 函数定义，而不能通过赋值语句；
> * 常量可以不用理会变量的作用域而在任何地方定义和访问；
> * 常量一旦定义就不能被重新定义或者取消定义；
> * 常量的值只能是标量。

###### 4.2 魔术常量

> * __LINE__	文件中的当前行号。
> * __FILE__	文件的完整路径和文件名。如果用在被包含文件中，则返回被包含的文件名。自 PHP 4.0.2 起，__FILE__ 总是包含一个绝对路径（如果是符号连接，则是解析后的绝对路径），而在此之前的版本有时会包含一个相对路径。
> * __DIR__	文件所在的目录。如果用在被包括文件中，则返回被包括的文件所在的目录。它等价于 dirname(__FILE__)。除非是根目录，否则目录中名不包括末尾的斜杠。（PHP 5.3.0中新增） =
> * __FUNCTION__	函数名称（PHP 4.3.0 新加）。自 PHP 5 起本常量返回该函数被定义时的名字（区分大小写）。在 PHP 4 中该值总是小写字母的。
> * __CLASS__	类的名称（PHP 4.3.0 新加）。自 PHP 5 起本常量返回该类被定义时的名字（区分大小写）。在 PHP 4 中该值总是小写字母的。类名包括其被声明的作用区域（例如 Foo\Bar）。注意自 PHP 5.4 起 __CLASS__ 对 trait 也起作用。当用在 trait 方法中时，__CLASS__ 是调用 trait 方法的类的名字。
> * __TRAIT__	Trait 的名字（PHP 5.4.0 新加）。自 PHP 5.4 起此常量返回 trait 被定义时的名字（区分大小写）。Trait 名包括其被声明的作用区域（例如 Foo\Bar）。
> * __METHOD__	类的方法名（PHP 5.0.0 新加）。返回该方法被定义时的名字（区分大小写）。
> * __NAMESPACE__	当前命名空间的名称（区分大小写）。此常量是在编译时定义的（PHP 5.3.0 新增）

------


# 7月4日 总结
### 运算符


位运算符 & （按位与） 和 逻辑运算符 &&（逻辑与）：
```php
<?php
$a = (2 & 5);
echo $a; // 0  ( 0 = 0000) = ( 2 = 0010) & ( 5 = 0101)
$b = (2 && 5);
var_dump($b); // bool(true) （真 && 真）= 真

?>
```
------
### 流程控制：
### if
if有两种使用形式
第一（推荐）：
```php
if(){
}else{
}
```
第二：
```php
if():
else:
endif;
```
### else if 与 elseif
> * else if只能在if使用第一种（花括号）形式时使用
> * esleif 两种情况下均能使用

### for
>for(表达式1，表达式2，表达式3）{}
> * 表达式1：在循环开始前无条件求值（并执行）一次。
> * 表达式2：在每次循环开始前求值。如果值为 TRUE，则继续循环，执行嵌套的循环语句。如果值为 FALSE，则终止循环。
> * 表达式3：在每次循环之后被求值（并执行）。

若用for 对数组操作，取数组长度（`count()` 或 `sizeof()` 都行，两个没区别）的操作不要写在for的第二个表达式，因为 for 的第二个表达式在每次循环都会执行一次，影响效率。

### foreach
对数组进行循环
```php
foreach (array_expression as $value)
    statement
foreach (array_expression as $key => $value)
    statement
```
第二种的\$key为数组的 键

------

### break 与 continue
break 与 continue 都可以跳出循环，break 跳出整个循环体，contiue 跳出此次循环，继续执行后面的语句。
```php
<?php
for($i = 0; $i < 4;$i++){
	if($i == 2){
		continue;
	}
	echo $i;
}
echo '<br>';
for($i = 0; $i < 4;$i++){
	if($i == 2){
		break;
	}
	echo $i;
}
?>
```
结果：
```php
013
01
```

### return
```php
<?php
$a = 1;
$b = 2;
$c = $a + $b;

return $c;

echo 123;

?>
```
结果：页面为输出123； return之后后面的代码不会输出
### required 与 include
require 和 include 几乎完全一样，除了处理失败的方式不同之外。require 在出错时产生 E_COMPILE_ERROR 级别的错误。换句话说将导致脚本中止而 include 只产生警告（E_WARNING），脚本会继续运行。

------