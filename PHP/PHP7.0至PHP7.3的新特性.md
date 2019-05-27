# PHP7.0 至 PHP7.3 的新特性

## PHP7.0

### PHP7.0 新特性

#### 1. 组合比较符（<=>）

比合不能进行比较

``` php
var_dump('PHP' <=> 'Node'); // int(1)
var_dump(123 <=> 456); // int(-1)
var_dump(['a', 'b'] <=> ['a', 'b']); // int(0)
```

#### 2. null 合并运算符

由于日常使用中存在大量同时使用三元表达式和 isset 操作。使用空合并运算符可以简化操作

``` php
// php7以前
if (isset($_GET['a'])) {
  $a = $_GET['a'];
}
// php7以前
$a = isset($_GET['a']) ? $_GET['a'] : 'none';
// PHP 7
$a = isset($_GET['a']) ?? 'none';
```

#### 4. 变量类型声明

变量类型声明有两种模式。允许使用下列类型参数**int**，**string**，**float**，**bool**

同时不能再使用整型，字符串，浮点型，布尔作为类的名字了

``` php
function sumOfInts(int ...$ints)
{
    return array_sum($ints);
}
var_dump(sumOfInts(2, '3', 4.1)); // int(9)
// 严格模式
declare(strict_types = 1);
function add(int $x, int $y)
{
    return $x + $y;
}
var_dump(add('2', 3)); // Fatal error: Argument 1 passed to add() must be of the type integer
```

#### 5. 返回值类型声明

增加了返回类型声明，类似参数类型这样更方便的控制函数的返回值在函数定义的后面加上：类型名即可

``` php
function fun(int $a): array
{
  return $a;
}
fun(3); // Fatal error
```

#### 6. 匿名类

php7 允许新类{}创建一个匿名的对象。

``` php
// php7以前
class Logger
{
    public function log($msg)
    {
        echo $msg;
    }
}
$util->setLogger(new Logger());
// php7+
$util->setLogger(new class {
    public function log($msg)
    {
        echo $msg;
    }
});
```

#### 7. Unicode codepoint 转译语法

这接受一个以 16 进制形式的 Unicode codepoint，并打印出一个双引号或 heredoc 包围的 UTF-8 编码格式的字符串。可以接受任何有效的 codepoint，并且开头的 0 是可以省略的

``` php
echo "\u{aa}"; // ª
echo "\u{0000aa}"; // ª
echo "\u{9999}"; // 香
```

#### 8. Closure :: call

闭包绑定简短干练的暂时绑定一个方法到对象上闭包并并用它。

``` php
class A {
    private $x = 1;
}
// PHP 7 之前版本的代码
$getXCB = function() {
    return $this->x;
};
$getX = $getXCB->bindTo(new A, 'A'); // 中间层闭包
echo $getX();
// PHP 7+ 及更高版本的代码
$getX = function() {
    return $this->x;
};
echo $getX->call(new A);
```

#### 9. 带过滤的反序列化

提供更安全的方式解包不可靠的数据。它通过白名单的方式来防止潜在的代码注入

``` php
// 将所有的对象都转换为 __PHP_Incomplete_Class 对象
$data = unserialize($foo, ["allowed_classes" => false]);
// 将除 MyClass 和 MyClass2 之外的所有对象都转换为 __PHP_Incomplete_Class 对象
$data = unserialize($foo, ["allowed_classes" => ["MyClass", "MyClass2"]);
// 默认情况下所有的类都是可接受的，等同于省略第二个参数
$data = unserialize($foo, ["allowed_classes" => true]);
```

#### 10. IntlChar 类

这个类自身定义了许多静态方法用于操作多字符集的 unicode 字符。需要安装 intl 拓展

``` php
printf('%x', IntlChar::CODEPOINT_MAX);
echo IntlChar::charName('@');
var_dump(IntlChar::ispunct('!'));
```

#### 11. 预期

它使得在生产环境中启用断言为零成本，并且提供当断言失败时抛出特定异常的能力。以后可以使用这个这个进行断言测试

``` php
ini_set('assert.exception', 1);
class CustomError extends AssertionError {}
assert(false, new CustomError('Some error message'));
```

#### 12. 命名空间按组导入

从同一个命名空间下导入的类，函数，常量支持按组一次导入

``` php
// php7以前
use app\model\A;
use app\model\B;
// php7+
use app\model{A, B};
```

#### 13. 生成器支持返回表达式

它允许在生成器函数中通过使用  _return_  语法来返回一个表达式（但是不允许返回引用值），可以通过调用  _Generator :: getReturn（）_  方法来获取生成器的返回值，但是这个方法只能在生成器完成产生工作以后调用一次。

``` php
$gen = (function() {
    yield 1;
    yield 2;
    return 3;
})();
foreach ($gen as $val) {
    echo $val, PHP_EOL;
}
echo $gen->getReturn(), PHP_EOL;
// output
// 1
// 2
// 3
```

#### 14. 生成器委派

现在，只需在最外层生成其中使用 yield from，就可以把一个生成器自动委派给其他的生成器

``` php
function gen()
{
    yield 1;
    yield 2;
    yield from gen2();
}
function gen2()
{
    yield 3;
    yield 4;
}
foreach (gen() as $val)
{
    echo $val, PHP_EOL;
}
```

#### 15. 整数除法函数 intdiv

``` php
var_dump(intdiv(10, 3)) // 3
```

#### 16. 会话选项设置

session_start() 可以加入一个数组覆盖 php.ini 的配置

``` php
session_start([
    'cache_limiter' => 'private',
    'read_and_close' => true,
]);
```

#### 17. preg_replace_callback_array

可以使用一个关联数组来对每个正则表达式注册回调函数，正则表达式本身作为关联数组的键，而对应的回调函数就是关联数组的值

``` php
string preg_replace_callback_array(array $regexesAndCallbacks, string $input);
$tokenStream = []; // [tokenName, lexeme] pairs
$input = <<<'end'
$a = 3; // variable initialisation
end;
// Pre PHP 7 code
preg_replace_callback(
    [
        '~\$[a-z_][a-z\d_]*~i',
        '~=~',
        '~[\d]+~',
        '~;~',
        '~//.*~'
    ],
    function ($match) use (&$tokenStream) {
        if (strpos($match[0], '$') === 0) {
            $tokenStream[] = ['T_VARIABLE', $match[0]];
        } elseif (strpos($match[0], '=') === 0) {
            $tokenStream[] = ['T_ASSIGN', $match[0]];
        } elseif (ctype_digit($match[0])) {
            $tokenStream[] = ['T_NUM', $match[0]];
        } elseif (strpos($match[0], ';') === 0) {
            $tokenStream[] = ['T_TERMINATE_STMT', $match[0]];
        } elseif (strpos($match[0], '//') === 0) {
            $tokenStream[] = ['T_COMMENT', $match[0]];
        }
    },
    $input
);
// PHP 7+ code
preg_replace_callback_array(
    [
        '~\$[a-z_][a-z\d_]*~i' => function ($match) use (&$tokenStream) {
            $tokenStream[] = ['T_VARIABLE', $match[0]];
        },
        '~=~' => function ($match) use (&$tokenStream) {
            $tokenStream[] = ['T_ASSIGN', $match[0]];
        },
        '~[\d]+~' => function ($match) use (&$tokenStream) {
            $tokenStream[] = ['T_NUM', $match[0]];
        },
        '~;~' => function ($match) use (&$tokenStream) {
            $tokenStream[] = ['T_TERMINATE_STMT', $match[0]];
        },
        '~//.*~' => function ($match) use (&$tokenStream) {
            $tokenStream[] = ['T_COMMENT', $match[0]];
        }
    ],
    $input
);
```

#### 18. 随机数，随机字符函数

``` php
string random_bytes(int length);
int random_int(int min, int max);
```

#### 19.定义支持定义数组

``` php
// php7+
define('ALLOWED_IMAGE_EXTENSIONS', ['jpg', 'jpeg', 'gif', 'png']);
```

### PHP7.0 变化

#### 1. 错误和异常处理相关变更

PHP 7 改变了大多数错误的报告方式。不同于传统（PHP 5）的错误报告机制，现在大多数错误被作为  **错误**  异常抛出。

这也意味着，当前生错误的时候，以前代码中的一些错误处理的代码将无法被触发。因为在 PHP 7 版本中，已经使用抛出异常的错误处理机制了。（如果代码中没有捕获  **错误**  异常，那么会引发致命错误）.set_error_handle 不一定接收的是异常，有可能是错误。

ERROR 层级结构

``` php
interface Throwable
    |- Exception implements Throwable
        |- ...
    |- Error implements Throwable
        |- TypeError extends Error
        |- ParseError extends Error
        |- AssertionError extends Error
        |- ArithmeticError extends Error
            |- DivisionByZeroError extends ArithmeticError
```

``` php
function handler(Exception $e) { ... }
set_exception_handler('handler');
// 兼容 PHP 5 和 7
function handler($e) { ... }
// 仅支持 PHP 7
function handler(Throwable $e) { ... }
```

#### 2. 清单

list 会按照原来的顺序进行赋值。不再是逆序了

``` php
list($a,$b,$c) = [1, 2, 3];
var_dump($a); // 1
var_dump($b); // 2
var_dump($c); // 3
```

列出不再支持解开字符串，

#### 3. foreach 不再改变内部数组指针

``` php
$array = [0, 1, 2];
foreach ($array as &$val) {
    var_dump(current($array));
}
// php 5
int(1)
int(2)
bool(false)
// php7
int(0)
int(0)
int(0)
```

#### 4. 十六进制字符串不再被认为是数字

``` php
var_dump("0x123" == "291");
// php5
true
// php7
false
```

#### 5. $HTTP_RAW_POST_DATA 被移

`$HTTP_RAW_POST_DATA` 被移，使用 `php://input` 代替

#### 6. 移除了 ASP 和脚本 PHP 标签

| 开标签 | 闭标签 |
| --- | --- |
| `<%` | `%>` |
| `<%=` | `%>` |
| `<script language="php">` | `</script>` |

## PHP7.1

### PHP7.1 新特性

#### 1. 可为空（Nullable）类型

参数以及返回值的类型现在可以通过在类型前加上一个问号使之允许为空。当启用这个特性时，传入的参数或者函数返回的结果要么是给定的类型，要么是空

``` php
// php5
function($a = null){
  if ($a === null) {
    return null;
  }
  return $a;
}
// php7+
function fun() :?string
{
  return null;
}
function fun1(?$a)
{
  var_dump($a);
}
fun1(null); // null
fun1('1'); // 1
```

#### 无类型

返回值声明为 void 类型的方法要么干脆省去 return 语句。对于 void 来说，**NULL**  不是一个合法的返回值。

``` php
function fun() :void
{
  echo "hello world";
}
```

#### 3. 类常量可见性

``` php
class Something
{
    const PUBLIC_CONST_A = 1;
    public const PUBLIC_CONST_B = 2;
    protected const PROTECTED_CONST = 3;
    private const PRIVATE_CONST = 4;
}
```

#### 4. iterable 伪类

这可以被用在参数或者返回值类型中，它代表接受数组或者实现了**Traversable 的**接口的对象。

``` php
function iterator(iterable $iter)
{
    foreach ($iter as $val) {
        //
    }
}
```

#### 5. 多异常捕获处理

一个 catch 语句块现在可以通过管道字符（_|_ ）来实现多个异常的捕获。这对于需要同时处理来自不同类的不同异常时很有用

``` php
try {
    // some code
} catch (FirstException | SecondException $e) {
    // handle first and second exceptions
}
```

#### 6. 列出支持键名

``` php
$data = [
    ["id" => 1, "name" => 'Tom'],
    ["id" => 2, "name" => 'Fred'],
];
// list() style
list("id" => $id1, "name" => $name1) = $data[0];
var_dump($id1); // 1
```

#### 7. 字符串支持负向

``` php
$a = "hello";
$a[-2]; // l
```

#### 8. 将回调转闭包

Closure 新增了一个静态方法，用于将 callable 快速地转为一个 Closure 对象。

``` php
class Test
{
    public function exposeFunction()
    {
        return Closure::fromCallable([$this, 'privateFunction']);
    }
    private function privateFunction($param)
    {
        var_dump($param);
    }
}
$privFunc = (new Test)->exposeFunction();
$privFunc('some value');
```

#### 9. http2 服务推送

对 http2 服务器推送的支持现在已经被加入到 CURL 扩展

### PHP7.1 变更

#### 1. 传递参数过少时将抛出错误

过去我们传递参数过少会产生 warning.php7.1 开始会抛出错误

#### 2. 移除了 ext / mcrypt 拓展

## PHP7.2

### PHP7.2 新特性

#### 增加新的类型对象

``` php
function test(object $obj) : object
{
    return new SplQueue();
}
test(new StdClass());
```

#### 2. 通过名称加载扩展

扩展文件不再需要通过文件加载（Unix 下以_.so_为文件扩展名，在 Windows 下以  _.dll_  为文件扩展名）进行指定。可以在 php.ini 配置文件进行启用

``` ini
; ini file
extension=php-ast
zend_extension=opcache
```

#### 允许重写抽象方法

当一个抽象类继承于另外一个抽象类的时候，继承后的抽象类可以重写被继承的抽象类的抽象方法。

``` php
abstract class A
{
    abstract function test(string $s);
}
abstract class B extends A
{
    // overridden - still maintaining contravariance for parameters and covariance for return
    abstract function test($s) : int;
}
```

#### 4. 使用 Argon2 算法生成密码散列

Argon2 已被加入到密码散列（密码哈希）API（这些函数以  _密码_  _开头），以下是暴露出来的常量

#### 5. 新增 PDO 字符串扩展类型

当你准备支持多语言字符集，PDO 的字符串类型已经扩展支持国际化的字符集以下是扩展的常量：

* PDO :: PARAM_STR_NATL
* PDO :: PARAM_STR_CHAR
* PDO :: ATTR_DEFAULT_STR_PARAM

``` php
$db->quote('über', PDO::PARAM_STR | PDO::PARAM_STR_NATL);
```

#### 6. 命名分组命名空间支持尾部逗号

``` php
use Foo\Bar\{
    Foo,
    Bar,
    Baz,
};
```

### PHP7.2 变更

#### 1. number_format 返回值

``` php
var_dump(number_format(-0.01)); // now outputs string(1) "0" instead of string(2) "-0"
```

#### 2. get_class（）不再允许 null

``` php
var_dump(get_class(null)); // warning
```

#### 4. 计算作用在不是可数类型将发生警告

``` php
count(1); // integers are not countable
```

#### 5. 不带引号的字符串

在之前不带引号的字符串是不存在的全局常量，转化成他们自身的字符串。现在将会产生华林。

``` php
var_dump(HEELLO);
```

#### 6. __autoload 被废弃

__autoload 方法已被废弃

#### 7. 每个都被废弃

使用此函数遍历时，比普通的的 _foreach_  更慢，并且给新语法的变化带来实现问题。因此它被废弃了。

#### 8. is_object，gettype 修正

is_object 作用在 **__ PHP_Incomplete_Class**

将 gettype 作用在闭包在将正确返回的资源

#### 9. 转换对象/数组转换中的数字键

把数组转对象的时候，可以访问到整型键的值。

``` php
// array to object
$arr = [0 => 1];
$obj = (object)$arr;
var_dump(
    $obj,
    $obj->{'0'}, // now accessible
    $obj->{0} // now accessible
);
```

**PHP7.3**

* 添加了 array_key_first() 和 array_key_last() 来获取数组的第一个和最后一个元素的键名
* 添加了 fpm_get_status() 方法，来获取 FPM 状态数组，
* 添加了几个 FPM 的配置项，用来控制日志单行最大字符数，日志缓冲等：log_limit，log_buffering，decorate_workers_output
* 现在需要 libcurl >= 7.15.5
* curl 添加了一堆常量
* json_decode 添加了一个常量，JSON_THROW_ON_ERROR，如果解析失败可以抛出异常，而不是通过之前的方法 json_last_error() 去获取
* spl autoloader：如果一个加载失败，剩下的都不再执行
* 说明了一些循环引用的情况会得到怎样的结果
* heredoc/nowdoc 中如果遇到跟定界符相同的字符串就认为结束了，而最后真正的结束符则会被认为是语法错误;
* 在循环+ switch-case 语句的 case 中使用继会会报警
* 说明了，静态变量在被遗承时，如果在子类里发生了循环引用，父类里的静态变量会跟着变

## 参考资料

* http://php.net/manual/zh/migration70.new-features.php
* http://php.net/manual/zh/migration71.new-features.php
* http://php.net/manual/zh/migration72.new-features.php
* http://php.net/manual/zh/migration73.new-features.php
