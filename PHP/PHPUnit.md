# PHPUnit

## 安装 phpunit

### 项目安装

``` bash
composer require --dev phpunit/phpunit
```

使用 `./vendor/bin/phpunit`

### 全局安装

``` bash
composer global require --dev phpunit/phpunit
```

使用 `phpunit`

## 快速入门

### 基本格式

* 测试类命名： `类名 + Test` ， eg `FooClassTest`
* 测试方法命名： `test + 方法名`, eg `testFoo`

> 也可以使用注释 `@test` 来标注需要测试的方法

``` php
use PHPUnit\Framework\TestCase;

class SampleTest extends TestCase
{
    public function testSomething()
    {
        $this->assertTrue(true, 'This should already work.');
    }

    /**
     * @test
     */
    public function something()
    {
        $this->assertTrue(true, 'This should already work.');
    }
}
```

### 测试依赖(@depends)

有一些测试方法需要依赖于另一个测试方法的返回值，此时需要使用测试依赖。测试依赖
通过注释 `@depends` 来标记。

下列中， depends 方法的 return 值作为 testConsumer 的参数传入

``` php
use PHPUnit\Framework\TestCase;

class MultipleDependenciesTest extends TestCase
{
    public function testProducerFirst()
    {
        $this->assertTrue(true);
        return 'first';
    }

    public function testProducerSecond()
    {
        $this->assertTrue(true);
        return 'second';
    }

    /**
     * @depends testProducerFirst
     * @depends testProducerSecond
     */
    public function testConsumer($a, $b)
    {
        $this->assertSame('first', $a);
        $this->assertSame('second', $b);
    }
}
```

### 数据提供器(@dataProvider)

在依赖中，所依赖函数的返回值作为参数传入测试函数。除此之外，我们也可以用数据提供器
来定义传入的数据。

``` php
use PHPUnit\Framework\TestCase;

class DataTest extends TestCase
{
    /**
     * @dataProvider additionProvider
     */
    public function testAdd($a, $b, $expected)
    {
        $this->assertSame($expected, $a + $b);
    }

    public function additionProvider()
    {
        return [
            'adding zeros' => [0, 0, 0], // 0 + 0 = 0 pass
            'zero plus one' => [0, 1, 1], // 0 + 1 = 1 pass
            'one plus zero' => [1, 0, 1], // 1 + 0 = 1 pass
            'one plus one' => [1, 1, 2], // 1 + 1 = 2 pass
        ];
    }
}
```

### 测试异常(expectException)

需要在测试方法的开始处声明断言，然后执行语句。**而不是调用后再声明**

也可以通过注释来声明 `@expectedException`, `@expectedExceptionCode`, 
`@expectedExceptionMessage`, `@expectedExceptionMessageRegExp`

``` php
use PHPUnit\Framework\TestCase;

class ExceptionTest extends TestCase
{
    public function testException()
    {
        $this->expectException(\Exception::class);

        throw new \Exception('test');
    }

    /**
     * @throws \Exception
     * @test
     * @expectedException \Exception
     */
    public function exceptionExpect()
    {
        throw new \Exception('test');
    }
}
```

### 测试 PHP 错误

通过提前添加期望，来使测试正常进行，而不会报出 PHP 错误

``` php
use PHPUnit\Framework\TestCase;

class ExpectedErrorTest extends TestCase
{
    /**
     * @expectedException PHPUnit\Framework\Error\Error
     */
    public function testFailingInclude()
    {
        include 'not_existing_file.php';
    }
}
```

### 测试输出

直接添加期望输出，然后执行相关函数。和测试异常类似，需要先添加期望，再执行代码。

``` php
use PHPUnit\Framework\TestCase;

class OutputTest extends TestCase
{
    public function testExpectFooActualFoo()
    {
        $this->expectOutputString('foo');
        print 'foo';
    }

    public function testExpectBarActualBaz()
    {
        $this->expectOutputString('bar');
        print 'baz';
    }
}
```

## 命令行测试

此章节主要说明了命令行的一些格式和可用参数。可以参考官方文档
获取细节。[The Command-Line Test Runner](https://phpunit.readthedocs.io/en/7.4/textui.html)

## 基境

基境就是在测试前需要准备的一系列东西。

比如有的测试需要依赖数据库的数据，那么在测试类运作前需要进行数据的准备。

主要有两个函数 `setUp` 和 `tearDown`。

> 那为什么不直接用构造函数和析构函数呢？是因为这两个有他用，当然你可可以直接用构造函数，然后再执行 `parent::__construct`，但不是麻烦嘛;

## 组织你的测试代码

可以通过命令行的 `--bootstrap` 参数来指定启动文件，用于文件加载。正常情况下，可以指向 composer 的 autoload 文件。
也可以在配置文件中配置（推荐）。

``` bash
$ phpunit --bootstrap src/autoload.php tests
PHPUnit |version|.0 by Sebastian Bergmann and contributors.

.................................

Time: 636 ms, Memory: 3.50Mb

OK (33 tests, 52 assertions)
```

``` xml
<phpunit bootstrap="src/autoload.php">
  <testsuites>
    <testsuite name="money">
      <directory>tests</directory>
    </testsuite>
  </testsuites>
</phpunit>
```

## 有风险的测试(Risky Tests)

### 无用测试(Useless Tests)

默认情况下，如果你的测试函数没有添加预期或者断言，就会被认为是无用测试。

> 通过设置 `--dont-report-useless-tests` 命令行参数，或者在 xml 配置文件中配置 `beStrictAboutTestsThatDoNotTestAnything="false"` 来更改这一默认行为。

### 意外的代码覆盖(Unintentionally Covered Code)

当打开这个配置后，如果使用 `@covers` 注释来包含一些文件的覆盖报告，就会被
判定为有风险的测试。

> 通过设置 `--strict-coverage` 命令行参数，或者在 xml 配置文件中配置 `beStrictAboutCoversAnnotation="true"` 来更改这一默认行为。

### 测试过程中有输出(Output During Test Execution)

如果在测试过程中输出文本，则会被认定为有风险的测试。

> 通过设置 `--disallow-test-output` 命令行参数，或者在 xml 配置文件中配置 `beStrictAboutOutputDuringTests="true"` 来更改这一默认行为。

### 测试超时(Test Execution Timeout)

通过注释来限制某些测试不能超过一定时间：

* @large 60 秒
* @medium 10 秒
* [@small](https://learnku.com/users/24849) 1 秒

> 通过设置 `--enforce-time-limit` 命令行参数，或者在 xml 配置文件中配置 `enforceTimeLimit="true"` 来更改这一默认行为。

### 操作全局状态(Global State Manipulation)

phpunit 可以对全局状态进行检测。

> 通过设置 `--strict-global-state` 命令行参数，或者在 xml 配置文件中配置 `beStrictAboutChangesToGlobalState="true"` 来更改这一默认行为。

## 待完善的测试和跳过的测试

处于一些原因，我们希望跳过或者对某些测试方法标记未待完善

### 待完善的测试

使用 `$this->markTestIncomplete` 标记待完善的测试

``` php
use PHPUnit\Framework\TestCase;

class SampleTest extends TestCase
{
    public function testSomething()
    {
        $this->assertTrue(true, 'This should already work.');

        $this->markTestIncomplete(
          'This test has not been implemented yet.'
        );
    }
```

### 跳过的测试

使用 `markTestSkipped` 来标记跳过的测试。

``` php
use PHPUnit\Framework\TestCase;

class DatabaseTest extends TestCase
{
    protected function setUp()
    {
        if (!extension_loaded('mysqli')) {
            $this->markTestSkipped(
              'The MySQLi extension is not available.'
            );
        }
    }

    public function testConnection()
    {
        // ...
    }
}
```

### 结合 @require 来跳过测试

以下的示例中，使用 require 来限定测试需要依赖 mysqli 拓展和 5.3 以上
的 PHP 版本，否则跳过测试

``` php
use PHPUnit\Framework\TestCase;

/**
 * @requires extension mysqli
 */
class DatabaseTest extends TestCase
{
    /**
     * @requires PHP 5.3
     */
    public function testConnection()
    {
        // Test requires the mysqli extension and PHP >= 5.3
    }

    // ... All other tests require the mysqli extension
}
```

## 数据库测试

使用数据库测试之前先安装拓展 `composer require --dev phpunit/dbunit`。

总的来说，我们在好多的测试场景中都会用到数据库，我们可以结合 PHPUnit 的基境
章节中提到的 `setUp` 来进行测试。

我们来看一个示例

``` php
use PHPUnit\DbUnit\DataSet\ArrayDataSet;
use PHPUnit\DbUnit\TestCaseTrait;
use PHPUnit\Framework\TestCase;

/**
 * 测试之前，需要在 MySQL 中新建数据库 phpunit，并且新建表 guestbook
 * CREATE TABLE `guestbook` (
 * `id` bigint(20) NOT NULL,
 * `content` varchar(255) COLLATE utf8mb4_bin NOT NULL,
 * `user` varchar(255) COLLATE utf8mb4_bin NOT NULL,
 * `created` datetime NOT NULL
 * ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;
 * Class ConnectionTest.
 *
 * @requires extension pdo_mysql
 */
class ConnectionTest extends TestCase
{
    use TestCaseTrait;

    /**
     * @return \PHPUnit\DbUnit\Database\DefaultConnection
     */
    public function getConnection()
    {
        $pdo = new \PDO(
            'mysql:host=127.0.0.1:33060;dbname=phpunit;charset=utf8mb4',
            'root',
            '112233'
        );

        return $this->createDefaultDBConnection($pdo);
    }

    /**
     * 请注意，phpunit每次会先 TRUNCATE 数据库，然后把下面数组的数据插入进去.
     *
     * @return ArrayDataSet
     */
    public function getDataSet()
    {
        return new ArrayDataSet(
            [
                'guestbook' => [
                    [
                        'id' => 1,
                        'content' => 'Hello buddy!',
                        'user' => 'joe',
                        'created' => '2010-04-24 17:15:23',
                    ],
                    [
                        'id' => 2,
                        'content' => 'I like it!',
                        'user' => 'mike',
                        'created' => '2010-04-26 12:14:20',
                    ],
                ],
            ]
        );
    }

    public function testCreateDataSet()
    {
        $this->markTestSkipped('just an example, skipped');
        $tableNames = ['guestbook'];
        $dataSet = $this->getConnection()->createDataSet();
    }

    public function testCreateQueryTable()
    {
        $this->markTestSkipped('just an example, skipped');
        $tableNames = ['guestbook'];
        $queryTable = $this->getConnection()->createQueryTable('guestbook', 'SELECT * FROM guestbook');
    }

    public function testGetRowCount()
    {
        $this->assertSame(2, $this->getConnection()->getRowCount('guestbook'));
    }

    /**
     * 测试表的内容和给定的数据集相等.
     */
    public function testAddEntry()
    {
        $queryTable = $this->getConnection()->createQueryTable(
            'guestbook', 'SELECT * FROM guestbook'
        );
        $expectedTable = $this->createFlatXmlDataSet(__DIR__.'/expectedBook.xml')
            ->getTable('guestbook');
        $this->assertTablesEqual($expectedTable, $queryTable);
    }
}
```

其中 `getConnection` 和 `getDataSet` 都是 `TestCaseTrait` 中提供的方法，
我们在 `getConnection` 中设定数据库的链接动作，同时在 `getDataSet` 中设定
需要往数据库中写入的数据，注意，每次执行这个测试类时，都会执行

1. 清空数据库 TRUNCATE
2. 填充数据

> 如何验证呢？加一个字段为 datetime 类型，设置位数据库自动更新时间，即可看到每次执行测试时，时间都在变化

## 测试桩

所谓的桩测试，其实就是对一些类的方法进行一番 mock，强制其返回一些数据。因为在开发中，有一些类
依赖于第三方服务，而第三方服务又属于“不可控”因素，所以这个时候就需要使用“桩”了。

``` php
use PHPUnit\Framework\TestCase;

class StubTest extends TestCase
{
    public function testStub()
    {
        // Create a stub for the SomeClass class.
        $stub = $this->createMock(SomeClass::class);

        // Configure the stub.
        $stub->method('doSomething')
            ->willReturn('foo');

        // Calling $stub->doSomething() will now return
        // 'foo'.
        $this->assertSame('foo', $stub->doSomething());
    }

    public function testStub2()
    {
        // Create a stub for the SomeClass class.
        $stub = $this->getMockBuilder(SomeClass::class)
            ->disableOriginalConstructor()
            ->disableOriginalClone()
            ->disableArgumentCloning()
            ->disallowMockingUnknownTypes()
            ->getMock();

        // Configure the stub.
        $stub->method('doSomething')
            ->willReturn('foo');

        // Calling $stub->doSomething() will now return
        // 'foo'.
        $this->assertSame('foo', $stub->doSomething());
    }

    public function testReturnArgumentStub()
    {
        // Create a stub for the SomeClass class.
        $stub = $this->createMock(SomeClass::class);

        // Configure the stub.
        $stub->method('doSomething')
            ->will($this->returnArgument(0));

        // $stub->doSomething('foo') returns 'foo'
        $this->assertSame('foo', $stub->doSomething('foo'));

        // $stub->doSomething('bar') returns 'bar'
        $this->assertSame('bar', $stub->doSomething('bar'));
    }

    public function testReturnSelf()
    {
        // Create a stub for the SomeClass class.
        $stub = $this->createMock(SomeClass::class);

        // Configure the stub.
        $stub->method('doSomething')
            ->will($this->returnSelf());

        // $stub->doSomething() returns $stub
        $this->assertSame($stub, $stub->doSomething());
    }

    public function testReturnValueMapStub()
    {
        // Create a stub for the SomeClass class.
        $stub = $this->createMock(SomeClass::class);

        // Create a map of arguments to return values.
        $map = [
            ['a', 'b', 'c', 'd'],
            ['e', 'f', 'g', 'h'],
        ];

        // Configure the stub.
        $stub->method('doSomething')
            ->will($this->returnValueMap($map));

        // $stub->doSomething() returns different values depending on
        // the provided arguments.
        $this->assertSame('d', $stub->doSomething('a', 'b', 'c'));
        $this->assertSame('h', $stub->doSomething('e', 'f', 'g'));
    }

    public function testReturnCallbackStub()
    {
        // Create a stub for the SomeClass class.
        $stub = $this->createMock(SomeClass::class);

        // Configure the stub.
        $stub->method('doSomething')
            ->will($this->returnCallback('str_rot13'));

        // $stub->doSomething($argument) returns str_rot13($argument)
        $this->assertSame('fbzrguvat', $stub->doSomething('something'));
    }

    /**
     * 按照指定顺序返回列表中的值
     */
    public function testOnConsecutiveCallsStub()
    {
        // 为 SomeClass 类创建桩件。
        $stub = $this->createMock(SomeClass::class);

        // 配置桩件。
        $stub->method('doSomething')
            ->will($this->onConsecutiveCalls(2, 3, 5, 7));

        // $stub->doSomething() 每次返回值都不同
        $this->assertSame(2, $stub->doSomething());
        $this->assertSame(3, $stub->doSomething());
        $this->assertSame(5, $stub->doSomething());
    }

    public function testThrowExceptionStub()
    {
        $this->expectException(\Exception::class);

        // 为 SomeClass 类创建桩件
        $stub = $this->createMock(SomeClass::class);

        // 配置桩件。
        $stub->method('doSomething')
            ->will($this->throwException(new \Exception()));

        // $stub->doSomething() 抛出异常
        $stub->doSomething();
    }
}

class SomeClass
{
    public function doSomething()
    {
        // Do something.
    }
}
```

我们看到， `SomeClass` 的 `doSomething()` 本身没有返回数据，我们通过桩动作，来完成了测试。

> 这个在测试依赖于第三方服务的相关代码时很管用。

## 代码覆盖度

### 白名单文件(Whitelisting Files)

添加到白名单文件的文件或者文件夹，会进行代码覆盖度统计的工作。具体的参数可以看帮助文档

###　忽略代码块(Ignoring Code Blocks)

我们可以添加部分代码不进行覆盖度统计。通过一些注释来标记即可

``` php
use PHPUnit\Framework\TestCase;

/**
 * @codeCoverageIgnore
 */
class Foo
{
    public function bar()
    {
    }
}

class Bar
{
    /**
     * @codeCoverageIgnore
     */
    public function foo()
    {
    }
}

if (false) {
    // @codeCoverageIgnoreStart
    print '*';
    // @codeCoverageIgnoreEnd
}

exit; // @codeCoverageIgnore
```

### 执行方法进行统计(Specifying Covered Methods)

同样通过添加注释标记的方法来执行需要覆盖的方法。

``` php
use PHPUnit\Framework\TestCase;

class BankAccountTest extends TestCase
{
    protected $ba;

    protected function setUp()
    {
        $this->ba = new BankAccount;
    }

    /**
     * @covers BankAccount::getBalance
     */
    public function testBalanceIsInitiallyZero()
    {
        $this->assertSame(0, $this->ba->getBalance());
    }

    /**
     * @covers BankAccount::withdrawMoney
     */
    public function testBalanceCannotBecomeNegative()
    {
        try {
            $this->ba->withdrawMoney(1);
        }

        catch (BankAccountException $e) {
            $this->assertSame(0, $this->ba->getBalance());

            return;
        }

        $this->fail();
    }

    /**
     * @covers BankAccount::depositMoney
     */
    public function testBalanceCannotBecomeNegative2()
    {
        try {
            $this->ba->depositMoney(-1);
        }

        catch (BankAccountException $e) {
            $this->assertSame(0, $this->ba->getBalance());

            return;
        }

        $this->fail();
    }

    /**
     * @covers BankAccount::getBalance
     * @covers BankAccount::depositMoney
     * @covers BankAccount::withdrawMoney
     */
    public function testDepositWithdrawMoney()
    {
        $this->assertSame(0, $this->ba->getBalance());
        $this->ba->depositMoney(1);
        $this->assertSame(1, $this->ba->getBalance());
        $this->ba->withdrawMoney(1);
        $this->assertSame(0, $this->ba->getBalance());
    }
}
```

## 原文链接

* [https://github.com/rovast/phpunit-demo](https://github.com/rovast/phpunit-demo)
