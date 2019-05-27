# PHP 的 SPL-Exception

PHP 的 SPL 里自带了 13 种 Exception，很多看起来意思也都差不多，那么到底它们应该在什么时候使用？各自的意义又有什么不同？

SPL 的 Exception，只有两个是直接继承自 \Exception 的。一个是 RuntimeException，一个是 LogicException。另外 11 个 Exceptions 都是又继承自它们。所以只要搞清楚它们两兄弟的区别，整个 SPL Exception 也就搞清楚一大半了。

RuntimeException 顾名思义，是运行时的异常。相对应的，LogicException 则是编译时的异常。说到这里，可能有的小伙伴就会问了，PHP 不是解释性脚本语言吗，怎么还分编译时和运行时呢？小伙伴的话说得很对（当然 PHP 也是有代码 => opcode 这个过程的，可以看作编译），但这个概念不能直接套用在 Exception 上。我们看看 PHP 官方文档对这两种 Exception 的阐述：

> RuntimeException: Exception thrown if an error which can only be found on runtime occurs.  
> LogicException: Exception that represents error in the program logic. This kind of exceptions should directly lead to a fix in your code.

也就是说，RuntimeException 这种意外，往往是用户造成，是代码调用者无法通过写更多逻辑代码来避免的。比如封装一个 ORM，在找不到数据的时候返回 NotFoundException（继承自 RuntimeException），ORM 调用者也无法避免此意外的产生，只能根据 NotFoundException 来作出意外处理，比如再抛出 Http404Exception 什么的。

而 LogicException 呢，则是相关代码创作人可以避免的，按照上面引用官方的说法，这类 Exception 都是应该被直接修复掉的。比如说你调用一个作除法的函数，抛出一个除数为 0 的 LogicException，函数使用者就应该对代码除数先作检查，避免用户输入 0 的时候还去调用此函数。

由此可见相对于 RuntimeException 而言，LogicException 更像是跟调用者说：你的调用方式不对，请检查您的代码！

说完 Logic/Runtime Exception 的区别，我们在看看其他 SPL 提供的 Exception 的意义：

1. Bad(Method/Function)CallException: Method 本身继承自 Function，都是调用时出错，这肯定是 LogicException，一定是方法调用者又没有好好看文档了。
2. DomianException: 官方文档的第一个评论就是一个很好的栗子：说好了是处理图片的方法，其他类型的文件就请先过滤掉吧。Domain 是域的意思，这个例子即是在表达文件类型必须属于图片类型这个域的意思。
3. InvalidArgumentException: 第一个评论同样提供了很好的栗子。其实在 PHP 的世界，因为没有基础类型的 type hint，所以往往都使用 InvalidArgumentException 来作为非法参数类型的错误。
4. LengthException: 官方文档里没有很明确的说明，从名称上看应该是说对期望数组变量的长度的一种判断，如果长度不在期望范围之内应该抛出此异常。
5. OutOfBoundsException: 看官方说法也应该是针对数组的：如果 key 不合法，那么抛出此异常。此异常属于 Runtime 异常。
6. OutOfRangeException: 跟 OutOfBoundsException 完全一样，只是此异常是 Logic 类型。所以，如果你能非常确定某个数组有哪些 key，就用 OutOfRangeException；如果你也不知道某个数组有哪些 key（可能又来自数据库什么的），就只能使用 OutOfBoundsException
7. OverflowException: 如果一个容器已经满了，调用者还往里塞东西，就抛出此异常。容器什么时候满肯定是代码创调用者自己无法预知的，所以此 Exception 属于 RuntimeException
8. RangeException: Runtime 版本的 DomainException
9. UnderflowException: 这个一定是针对空容器的。比如从空容器里删除一个元素，就可以抛出此异常
10. UnexpectedValueException: 这是官方文档说得最详细的 SPL Exception 了，我就原话翻译一下：如果变量不在某一组期待值里，抛出此异常。主要用于一个函数调用另外一个函数时返回值不是期待的类型或者值，也没有算法或者缓冲问题出现的时候。
