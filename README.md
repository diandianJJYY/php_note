看看 readme 能写多长
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
> * 变量名区分大小写 $var 与 $Var 不同
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

提示 $a未定义，正确做法在 $a 前加上个 global

------

#### 3.预定义变量
常见的预定义变量：
> * $_SERVER — 服务器和执行环境信息
> * $_GET — HTTP GET 变量
> * $_POST — HTTP POST 变量
> * $_FILES — HTTP 文件上传变量
> * $_REQUEST — HTTP Request 变量
> * $_SESSION — Session 变量
> * $_COOKIE — HTTP Cookies

例子：获取文件路径
> * $_SERVER['PHP_SELF'];

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
第二种的$key为数组的 键

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

# 2016-07-05 总结

标签（空格分隔）： php 基础 总结

---
#函数
方法：类里面的function
函数：类外面的function
> * 函数名不区分大小写 
```php
<?php
function f1(){
  echo 1;
}
functin F1(){
  echo 2;
}
f1();

/* result
Parse error: syntax error, unexpected 'F1' (T_STRING) in D:\wamp\www\test.php on line 5
*/
```
## 1.自定义函数
函数无需在调用之前被定义，除非是下面两个例子中函数是有条件被定义时。
当一个函数是有条件被定义时，必须在调用函数之前定义。
```php
<?php

$makefoo = true;

/* 不能在此处调用foo()函数*/
   
bar(); // 定义bar函数不需要条件，故可在函数定义前引用

if ($makefoo) {
  function foo()
  {
    echo "I am foo\n"; 
    /* '\n'在输出为文本的时候才能换行，在网页上应用'<br/>'(html标签);
    或者使用 echo nl2br("I am foo\nsdfdsa"); */
  }
}

foo(); // 当$makefoo = false 时，报错：函数未定义；

function bar()
{
  echo "I am bar\n";
}
```

## 2.函数参数
通过参数列表可以传递信息到函数，即以逗号作为分隔符的表达式列表。参数是从左向右求值的。
默认情况下，函数参数通过值传递（因而即使在函数内部改变参数的值，它并不会改变函数外部的值）。如果希望允许函数修改它的参数值，必须通过引用传递参数。

如果想要函数的一个参数总是通过引用传递，可以在函数定义中该参数的前面加上符号 &：
```php
<?php

function f1($f1){
  $f1 .= 'f1';
}
function f2(&$f2) // 加上了符号 &
{
    $f2 .= 'f2';
}
$f1 = $f2 = '123';
f1($f1);
f2($f2);
echo $f1;
echo '<br />';  
echo $f2;

/* result
123
123f2
*/
```

#### 2.1 函数调用传入的参数类型与默认参数的类型不符时：
```php
<?php
function makecoffee($arr = array('123'))
{
    return $arr;
}
var_dump(makecoffee());
var_dump(makecoffee(null));
var_dump(makecoffee("espresso"));
var_dump(makecoffee(false));
var_dump(makecoffee(true));
var_dump(makecoffee(0));
var_dump(makecoffee(1));
var_dump(makecoffee(array('345','789')));

/* result
array(1) {
  [0]=>
  string(3) "123"
}
NULL
string(8) "espresso"
bool(false)
bool(true)
int(0)
int(1)
array(2) {
  [0]=>
  string(3) "345"
  [1]=>
  string(3) "789"
}


```
传入的参数类型不改变；
注：echo 布尔类型的bool(false),结果为空；
    echo 布尔类型的bool(true),结果为1； 
    
#### 2.2 调用函数时传入参数而函数未定义参数：
```php
<?php

function f1(){
  echo '123' . '<br />';
  $c = func_get_args();
  var_dump($c);
}

$a = 456;
$b = array('aaa','bbb');

f1($a, $b);

/* result
123
array(2) { [0]=> int(456) [1]=> array(2) { [0]=> string(3) "aaa" [1]=> string(3) "bbb" } }
```
当函数未定义参数时，若调用函数时想传入参数可用[`func_get_args()`](http://php.net/manual/zh/function.func-get-args.php)或[`func_get_arg()`](http://php.net/manual/zh/functions.variable-functions.php)实现；

#### 2.3 调用函数时传入参数的个数与原函数定义的不符：
> * 书写规范：函数定义多个参数时应以逗号+空格隔开
```php
<?php
function f1($a = 1, $b = 2){
  echo $a + $b ;
}
f1('6and',2,4);

/* result
8
*/
```
注意当使用默认参数时，任何默认参数必须放在任何非默认参数的右侧；否则，函数将不会按照预期的情况工作。考虑下面的代码片断：
```php
<?php
function makeyogurt($type = "acidophilus", $flavour)
{
    return "Making a bowl of $type $flavour.\n";
}

echo makeyogurt("raspberry");   // won't work as expected
?>

/* result
Warning: Missing argument 2 in call to makeyogurt() in 
/usr/local/etc/httpd/htdocs/phptest/functest.html on line 41
Making a bowl of raspberry .
*/
```
## 3.返回值
> * 函数返回用return，如果省略了 return，则返回值为 NULL。
> * 函数内若要返回多个须以数组形式。

## 4.可变函数
> * call_user_func — 把第一个参数作为回调函数调用,传入call_user_func()的参数不能为引用传递。
> * call_user_func_array — 调用回调函数，并把一个数组参数作为回调函数的参数
```php
<?php
error_reporting(E_ALL);
function increment(&$var)
{
    $var++;
}

$a = 0;
call_user_func('increment', $a);
echo $a."\n";

call_user_func_array('increment', array(&$a)); // You can use this instead before PHP 5.3
echo $a."\n";

/* result
Warning: Parameter 1 to increment() expected to be a reference, value given in D:\wamp\www\test.php on line 9
0 1
*/
```

## 5.内置函数
join()函数是implode()的别名，作用：返回由数组元素组合成的字符串。
```php
<?php
$arr = array('Hello','World!','I','love','Shanghai!');
echo implode(" ",$arr);

/* result
Hello World! I love Shanghai!
*/
```

explode(),作用:使用一个字符串分割另一个字符串,此函数返回由字符串组成的数组。
```php
<?php
$str = "Hello world. I love Shanghai!";
print_r (explode(" ",$str));
?>

/* result
Array ( [0] => Hello [1] => world. [2] => I [3] => love [4] => Shanghai! )
*/
```
## 6.匿名函数
用use将变量传进来，此时的变量是局部变量，函数不会改变变量的值。
用global将变量传进来，此时的变量是全局变量，函数能够改变变量的值。
```php
<?php
$a = 1;
$b = 1;
$f1 = function() use ($a){
  $a = $a + 2;
  echo $a;
};
$f1();
echo '<br/>';
echo $a;

echo '<br>----<br>';

$f2 = function(){
  global $b;
  $b = $b + 2;
  echo $b;
};
$f2();
echo '<br/>';
echo $b;

/* resrult
3
1
----
3
3
*/

```