# MySQL 常用函数汇总

字符串函数
=====

| 函数 | 功能 |
| --- | --- |
| CONCAT(s1,s2,……) | 字符串连接 |
| INSERT(str,x,y,instr) | 将指定开始标记到结束的字符串替换为指定字符串 |
| LOWER(str) | 将字符串所有字符转为小写 |
| UPPER(str) | 将字符串所有字符串转为大写 |
| LEFT(str,x) | 返回字符串 str 最左边的 x 个字符 |
| RIGHT(str,x) | 返回字符串 str 最右边的 x 个字符 |
| LPAD(str,n,pad) | 在 str 最左边填充 n 个 pad |
| RPAD(str,n,pad) | 在 str 最右边填充 n 个 pad |
| LTRIM(str) | 去掉字符串 str 左侧的空格 |
| RTRIM(str) | 去掉字符串 str 右侧的空格 |
| REPEAT(str,x) | 返回 str 重复 x 次的结果 |
| STRCMP(s1,s2) | 比较字符串 s1 和 s2 |
| REPLACE(str,a,b) | 用字符串 b 替换字符串 str 中所有出现的字符串 a |
| TRIM(str) | 去掉字符串行尾和行头的空格 |
| SUBSTRING(str,x,y) | 返回从字符串 str x 位置起 y 个字符长度的字串 |

数学函数
====

| 函数 | 功能 |
| --- | --- |
| ABS(x) | 返回 x 的绝对值 |
| CEIL(x) | 返回大于 x 的最小整数值 |
| FLOOR(x) | 返回小于 x 的最大整数值 |
| MOD(x,y) | 返回 x/y 的模 |
| RAND() | 返回 0～1 内的随机值 |
| ROUND(x,y) | 返回参数 x 的四舍五入的有 y 位小数的值 |
| TRUNCATE(x,y) | 返回数字 x 截断位 y 位小数的结果 |

日期和时间函数
=======

| 函数 | 功能 |
| --- | --- |
| CURDATE() | 返回当前日期 |
| CURTIME() | 返回当前时间 |
| NOW() | 返回当前的日期和时间 |
| UNIX_TIMESTAMP(date) | 返回日期 date 的 UNIX 时间戳 |
| FROM_UNIXTIME | 返回 UNIX 时间戳的日期值 |
| WEEK(date) | 返回日期 date 为一年中的第几周 |
| YEAR(date) | 返回日期 date 的年份 |
| HOUR(time) | 返回 time 的小时值 |
| MINUTE(time) | 返回 time 的分钟值 |
| MONTHNAME(date) | 返回 date 的月份名 |
| DATE_FORMAT(date,fmt) | 返回按字符串 fmt 格式日期 date 值 |
| DATE_ADD(date,interval expr type) | 返回一个日期或时间值加上一个时间间隔的时间值 |
| DATEDIFF(expr,expr2) | 返回起始时间 expr 和结束时间 expr2 之间的天数 |

流程函数
====

| 函数 | 功能 |
| --- | --- |
| IF(value,t f) | 如果 value 是真，返回 t；否则返回 f |
| IFNULL(value1,value2) | 如果 value1 不为空，返回 value1，否则返回 value2 |
| CASE WHEN [value1] THEN[result1]...ELSE[default]END | 如果 value1 是真，返回 result1，否则返回 result |
| CASE[expr] WHEN [value1]THEN[result1]...ELSE[default]END | 如果 expr 等于 value1，返回 result1，否则返回 default |

其他常用函数
======

| 函数 | 功能 |
| --- | --- |
| DATEBASE() | 返回当前数据库名 |
| VERSION() | 返回当前数据库版本 |
| USER() | 返回当前登录用户名 |
| INET_ATON(ip) | 返回 ip 地址的数字表示 |
| INET_NTOA(num) | 返回数字代表的 ip 地址 |
| PASSWORD(str) | 返回字符串 str 的加密版本 |
| MD5() | 返回字符串 str 的 md5 值 |
