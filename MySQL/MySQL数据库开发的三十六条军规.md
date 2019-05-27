# MySQL 数据库开发的三十六条军规

## 一、核心军规(5)

### 1.1 尽量不在数据库做运算

* 别让脚趾头想事情，那是脑瓜子的职责
* 让数据库多做她擅长的事:
    * 尽量不在数据库做运算
    * 复杂运算秱到程序端 CPU
    * 尽可能简单应用 MySQL
* 举例: md5() / Order by Rand()

### 1.2 控制单表数据量

* 一年内的单表数据量预估
    * 纯 INT 不超 1000W
    * 含 CHAR 不超 500W
* 合理分表不超载
    * USERID
    * DATE
    * AREA
    * ……
* 建议单库不超过 300-400 个表

### 1.3 保持表身段苗条

* 表字段数少而精
    * IO 高效
    * 全表遍历
    * 表修复快
    * 提高幵发
    * alter table 快
* 单表多少字段合适?
* 单表 1G 体积 500W 行评估
    * 顺序读 1G 文件需 N 秒
    * 单行不超过 200Byte
    * 单表不超过 50 个纯 INT 字段
    * 单表不超过 20 个 CHAR(10)字段
* 单表字段数上限控制在 20~50 个

### 1.4 平衡范式不冗余

* 严格遵循三大范式?
* 效率优先、提升性能
* 没有绝对的对不错
* 适当时牺牲范式、加入冗余
* 但会增加代码复杂度

### 1.5 拒绝 3B

* 数据库幵发像城市交通
    * 非线性增长
* 拒绝 3B
    * 大 SQL (BIG SQL)
    * 大事务 (BIG Transaction)
    * 大批量 (BIG Batch)
* 详细解析见后

### 1.6 核心军规小结

* 尽量不在数据库做运算
* 控制单表数据量
* 保持表身段苗条
* 平衡范式不冗余
* 拒绝 3B

## 二、字段类军规(6)

### 2.1 用好数值字段类型

* 三类数值类型:
    * TINYINT(1Byte)
    * SMALLINT(2B)
    * MEDIUMINT(3B)
    * INT(4B)、BIGINT(8B)
    * FLOAT(4B)、DOUBLE(8B)
    * DECIMAL(M,D)
* BAD CASE:
    * INT(1) VS INT(11)
    * BIGINT AUTO_INCREMENT
    * DECIMAL(18,0)

### 2.2 将字符转化为数字

* 数字型 VS 字符串型索引
    * 更高效
    * 查询更快
    * 占用空间更小
* 举例:用无符号 INT 存储 IP，而非 CHAR(15)
    * INT UNSIGNED
    * INET_ATON()
    * INET_NTOA()

### 2.3 优先使用 ENUM 或 SET

* 优先使用 ENUM 或 SET
    * 字符串
    * 可能值已知且有限
* 存储
    * ENUM 占用 1 字节，转为数值运算
    * SET 视节点定，最多占用 8 字节
    * 比较时需要加' 单引号(即使是数值)
* 举例
    * `sex` enum('F','M') COMMENT '性别'
    * `c1` enum('0','1','2','3') COMMENT '职介审核'

### 2.4 避免使用 NULL 字段

* 避免使用 NULL 字段
    * 很难进行查询优化
    * NULL 列加索引，需要额外空间
    * 含 NULL 复合索引无效
* 举例
    * `a` char(32) DEFAULT NULL
    * `b` int(10) NOT NULL
    * `c` int(10) NOT NULL DEFAULT 0

### 2.5 少用并拆分 TEXT/BLOB

* TEXT 类型处理性能远低亍 VARCHAR
    * 强制生成硬盘临时表
    * 浪费更多空间
    * VARCHAR(65535)==>64K (注意 UTF-8)
* 尽量不用 TEXT/BLOB 数据类型
* 若必须使用则拆分到单独的表
* 举例:

``` sql
CREATE TABLE t1 (
id INT NOT NULL AUTO_INCREMENT, data text NOT NULL,
‏PRIMARY KEY id
) ENGINE=InnoDB;
```

### 2.6 不在数据库里存图片

### 2.7 字段类军规小结

* 用好数值字段类型
* 将字符转化为数字
* 优先使用枚举 ENUM/SET
* 避免使用 NULL 字段
* 少用幵拆分 TEXT/BLOB
* 不在数据库里存图片

## 三、索引类军规(5)

### 3.1 谨慎合理添加索引

* 谨慎合理添加索引
    * 改善查询
    * 减慢更新
    * 索引不是赹多赹好
* 能不加的索引尽量不加
    * 综合评估数据密度和数据分布
    * 最好不赸过字段数 20%
* 结合核心 SQL 优先考虑覆盖索引
* 举例
    * 不要给“性别”列创建索引

### 3.2 字符字段必须建前缀索引

* 区分度
    * 单字母区分度:26
    * 4 字母区分度:26*26*26*26=456,976
    * 5 字母区分度:26*26*26*26*26=11,881,376
    * 6 字母区分度:26*26*26*26*26*26=308,915,776
* 字符字段必须建前缀索引:

``` sql
(
`pinyin` varchar(100) DEFAULT NULL COMMENT '小区拼音', KEY `idx_pinyin` (`pinyin`(8)),
) ENGINE=InnoDB
```

### 3.3 不在索引列做运算

* 不在索引列进行数学运算或凼数运算
    * 无法使用索引
    * 导致全表扫描
* 举例:

``` sql
BAD: SELECT * from table WHERE to_days(current_date) – to_days(date_col) <= 10
GOOD: SELECT * from table WHERE date_col >= DATE_SUB('2011-10- 22',INTERVAL 10 DAY);
```

### 3.4 自增列或全局 ID 做 INNODB 主键

* 对主键建立聚簇索引
* 二级索引存储主键值
* 主键不应更新修改
* 按自增顺序揑入值
* 忌用字符串做主键
* 聚簇索引分裂
* 推荐用独立亍业务的 AUTO_INCREMENT 列或全局 ID 生成 器做代理主键
* 若不指定主键，InnoDB 会用唯一且非空值索引代替

### 3.5 尽量不用外键

* 线上 OLTP 系统(线下系统另论)
    * 外键可节省开发量
    * 有额外开销
    * 逐行操作
    * 可'到达'其它表，意味着锁
    * 高并发时容易死锁
* 由程序保证约束

### 3.6 索引类军规小结

* 谨慎合理添加索引
* 字符字段必须建前缀索引
* 不在索引列做运算
* 自增列或全局 ID 做 INNODB 主键
* 尽量不用外键

## 四、SQL 类军规(15)

### 4.1 SQL 语句尽可能简单

* 大 SQL VS 多个简单 SQL
    * 传统设计思想
    * BUT MySQL NOT
    * 一条 SQL 叧能在一个 CPU 运算
    * 5000+ QPS 的高幵发中，1 秒大 SQL 意味着?
    * 可能一条大 SQL 就把整个数据库堵死
* 拒绝大 SQL，拆解成多条简单 SQL
    * 简单 SQL 缓存命中率更高
    * 减少锁表时间，特别是 MyISAM
    * 用上多 CPU

### 4.2 保持事务(连接)短小

* 保持事务/DB 连接短小精悍
    * 事务/连接使用原则:即开即用，用完即关
    * 与事务无关操作放到事务外面, 减少锁资源的占用
    * 不破坏一致性前提下，使用多个短事务代替长事务
* 举例
    * 发贴时的图片上传等待
    * 大量的 sleep 连接

### 4.3 尽可能避免使用 SP/TRIG/FUNC

* 线上 OLTP 系统(线下库另论)
    * 尽可能少用存储过程
    * 尽可能少用触发器
    * 减用使用 MySQL 凼数对结果进行处理
* 由客户端程序负责

### 4.4 尽量不用 SELECT 

* 用 SELECT * 时
* 更多消耗 CPU、内存、IO、网络带宽
* 先向数据库请求所有列，然后丢掉不需要列?
* 尽量不用 SELECT * ，叧取需要数据列 • 更安全的设计:减少表变化带来的影响
* 为使用 covering index 提供可能性
* SELECT/JOIN 减少硬盘临时表生成，特别是有 TEXT/BLOB 时
* 举例:

``` sql
SELECT * FROM tag WHERE id = 999184;
SELECT keyword FROM tag WHERE id = 999184;
```

### 4.5 改写 OR 为 IN()

* 同一字段，将 or 改写为 in()
* OR 效率:O(n)
* IN 效率:O(Log n)
* 当 n 很大时，OR 会慢很多
* 注意控制 IN 的个数，建议 n 小亍 200
* 举例:

``` sql
SELECT * from opp WHERE phone='12347856' or phone='42242233' \G;
SELECT * from opp WHERE phone in ('12347856' , '42242233');
```

### 4.6 改写 OR 为 UNION

* 不同字段，将 or 改为 union
* 减少对不同字段进行 "or" 查询
* Merge index 往往很弱智
* 如果有足够信心:set global optimizer_switch='index_merge=off';
* 举例:

``` sql
SELECT * from opp WHERE phone='010-88886666' or cellPhone='13800138000';
SELECT * from opp WHERE phone='010-88886666' union SELECT * from opp WHERE cellPhone='13800138000';
```

### 4.7 避免负向查询和% 前缀模糊查询

* 避免负向查询
    * NOT、!=、<>、!<、!>、NOT EXISTS、NOT IN、 NOT LIKE 等
* 避免 % 前缀模糊查询
    * B+ Tree
    * 使用不了索引
    * 导致全表扫描
* 举例:

``` sql
SELECT * from post WHERE title like '北京%'; -- 298 rows in set (0.01 sec)
SELECT * from post WHERE title like '%北京%'; -- 572 rows in set (3.27 sec)
```

### 4.8 COUNT(*)的几个例子

* 几个有趣的例子:
    * COUNT(COL) VS COUNT(*)
    * COUNT(*) VS COUNT(1)
    * COUNT(1) VS COUNT(0) VS COUNT(100)
* 示例:

``` sql
`id` int(10) NOT NULL AUTO_INCREMENT COMMENT '公司的id', `sale_id` int(10) unsigned DEFAULT NULL,
```

* 结论
    * COUNT(*)=count(1)
    *COUNT(0)=count(1)
    * COUNT(1)=count(100)
    * COUNT(*)!=count(col)
    * WHY?

### 4.9 减少 COUNT(*)

* MyISAM VS INNODB
    * 不带 WHERE COUNT()
    * 带 WHERE COUNT()
* COUNT(*)的资源开销大，尽量不用少用
* 计数统计
    * 实时统计:用 memcache，双向更新，凌晨 跑基准
    * 非实时统计:尽量用单独统计表，定期重算

### 4.10 LIMIT 高效分页

* 传统分页:
    * SELECT * from table limit 10000,10;
* LIMIT 原理:
    * Limit 10000,10  偏秱量赹大则赹慢
* 推荐分页:
    * SELECT * from table WHERE id>=23423 limit 11;
    *SELECT * from table WHERE id>=23434 limit 11;
* 分页方式二:
    * SELECT * from table WHERE id >= ( SELECT id from table limit 10000,1 ) limit 10;
* 分页方式三:
    * SELECT * FROM table INNER JOIN (SELECT id FROM table LIMIT 10000,10) USING (id);
* 分页方式四:
    * 程序取 ID:SELECT id from table limit 10000,10;
    * SELECT * from table WHERE id in (123,456...);
* 可能需按场景分析幵重组索引
* 示例:

``` sql
MySQL> SELECT sql_no_cache * from post limit 10,10; 10 row in set (0.01 sec)
MySQL> SELECT sql_no_cache * from post limit 20000,10; 10 row in set (0.13 sec)
MySQL> SELECT sql_no_cache * from post limit 80000,10; 10 rows in set (0.58 sec)
MySQL> SELECT sql_no_cache id from post limit 80000,10; 10 rows in set (0.02 sec)
MySQL> SELECT sql_no_cache * from post WHERE id>=323423 limit 10; 10 rows in set (0.01 sec)
MySQL> SELECT * from post WHERE id >= ( SELECT sql_no_cache id from post limit 80000,1 ) limit 10; 10 rows in set (0.02 sec)
```

### 4.11 用 UNION ALL 而非 UNION

* 若无需对结果进行去重，则用 UNION ALL
    * UNION 有去重开销
* 举例:

``` sql
SELECT * FROM detail20091128 UNION ALL SELECT * FROM detail20110427 UNION ALL SELECT * FROM detail20110426 UNION ALL SELECT * FROM detail20110425 UNION ALL SELECT * FROM detail20110424 UNION ALL SELECT * FROM detail20110423;
```

### 4.12 分解联接保证高并发

* 高幵发 DB 不建议进行两个表以上的 JOIN
* 适当分解联接保证高幵发
    * 可缓存大量早期数据
    * 使用了多个 MyISAM 表
    * 对大表的小 ID IN()
    * 联接引用同一个表多次
    * 举例:

``` sql
MySQL> SELECT * from tag JOIN post on tag_post.post_id=post.id WHERE tag.tag='二手玩具';

MySQL> SELECT * from tag WHERE tag='二手玩具';
MySQL> SELECT * from tag_post WHERE tag_id=1321;
MySQL> SELECT * from post WHERE post.id in (123,456,314,141);
```

### 4.13 GROUP BY 去除排序

* GROUP BY 实现
    * 分组
    * 自劢排序
* 无需排序:Order by NULL
* 特定排序:Group by DESC/ASC
* 举例:

``` sql
MySQL> SELECT phone,count(*) from post group by phone limit 1 ; 1 row in set (2.19 sec)
MySQL> SELECT phone,count(*) from post group by phone order by null limit 1; 1 row in set (2.02 sec)
```

### 4.14 同数据类型的列值比较

* 原则:数字对数字，字符对字符
* 数值列不字符类型比较
    * 同时转换为双精度
    * 进行比对
* 字符列不数值类型比较
    * 字符列整列转数值
    * 不会使用索引查询
* 举例:字符列不数值类型比较

``` sql
字段:`remark` varchar(50) NOT NULL COMMENT '备注, 默认为空',

MySQL>SELECT `id`, `gift_code` FROM gift WHERE `deal_id` = 640 AND remark=115127; 1 row in set (0.14 sec)
MySQL>SELECT `id`, `gift_code` FROM pool_gift WHERE `deal_id` = 640 AND remark='115127'; 1 row in set (0.005 sec)
```

### 4.15 Load data 导数据

* 批量数据快导入:
    * 成批装载比单行装载更快，不需要每次刷新缓存
    * 无索引时装载比索引装载更快
    * Insert values ,values，values 减少索引刷新
    * Load data 比 insert 快约 20 倍
* 尽量不用 INSERT ... SELECT
    * 延迟
    * 同步出错

### 4.16 打散大批量更新

* 大批量更新凌晨操作，避开高峰
* 凌晨不限制
* 白天上限默认为 100 条/秒(特殊再议)
* 举例:

``` sql
update post set tag=1 WHERE id in (1,2,3); sleep 0.01;
update post set tag=1 WHERE id in (4,5,6); sleep 0.01;
......
```

### 4.17 Know Every SQL

* SHOW PROFILE
* MySQLdumpslow
* EXPLAIN
* Show Slow Log
* SHOW QUERY_RESPONSE_TIME(Percona)
* MySQLsla
* Show Processlist

### 4.18 SQL 类军规小结

* SQL 语句尽可能简单
* 保持事务(连接)短小
* 尽可能避免使用 SP/TRIG/FUNC
* 尽量不用 SELECT *
* 改写 OR 语句
* 避免负向查询和% 前缀模糊查询
* 减少 COUNT(*)
* LIMIT 的高效分页
* 用 UNION ALL 而非 UNION
* 分解联接保证高幵发
* GROUP BY 去除排序
* 同数据类型的列值比较
* Load data 导数据
* 打散大批量更新
* Know Every SQL!

## 五、约定类军规(5)

### 5.1 隔离线上线下

* 构建数据库的生态环境
* 开发无线上库操作权限
* 原则:线上连线上，线下连线下
    * 实时数据用 real 库
    * 模拟环境用 sim 库
    * 测试用 qa 库
    * 开发用 dev 库

### 5.2 禁止未经 DBA 确认的子查询

* MySQL 子查询
    * 大部分情况优化较差
    * 特别 WHERE 中使用 IN id 的子查询  一般可用 JOIN 改写
* 举例:

``` sql
SELECT * from table1 where id id from table2) in (SELECT insert into table1 (SELECT * from table2); -- 可能导致复制异常
```

### 5.3 永远不在程序端显式加锁

* 永远不在程序端对数据库显式加锁
    * 外部锁对数据库不可控
    * 高并发发时是灾难
    * 极难调试和排查
* 并发扣款等一致性问题
    * 采用事务
    * 相对值修改
    * Commit 前二次较验冲突

### 5.4 统一字符集为 UTF8

* 字符集:
    * MySQL 4.1 以前叧有 latin1
    * 为多语言支持增加多字符集
    * 也带来了 N 多问题
    * 保持简单
* 统一字符集:UTF8
* 校对规则:utf8_general_ci
* 乱码:SET NAMES UTF8

### 5.5 统一命名规范

* 库表等名称统一用小写
    * Linux VS Windows
    * MySQL 库表大小写敏感
    * 字段名的大小写不敏感
* 索引命名默认为“idx_字段名”
* 库名用缩写，尽量在 2~7 个字母
    * DataSharing ==> ds
* 注意避免用保留字命名
* ……

### 5.6 注意避免用保留字命名

* 举例:

``` sql
SELECT * from return;
SELECT * from `return`;
```

<details>
<summary><b>MySQL系统关键字</b></summary>

* ADD
* ALL
* ALTER GOTO
* GRANT
* GROUP
* PURGE
* RAID0
* RANGE
* ANALYZE
* AND
* AS HAVING
* HIGH_PRIORIT Y
* HOUR_MICROSEC OND
* READ
* READS
* REAL
* ASC
* ASENSITIVE
* BEFORE HOUR_MINUTE
* HOUR_SECON D
* IF
* REFERENCES
* REGEXP
* RELEASE
* BETWEEN
* BIGINT
* BINARY IGNORE
* IN
* INDEX
* RENAME
* REPEAT
* REPLACE
* BLOB
* BOTH
* BY INFILE
* INNER
* INOUT
* REQUIRE
* RESTRICT
* RETURN
* CALL
* CASCADE
* CASE INSENSITIVE
* INSERT
* INT
* REVOKE
* RIGHT
* RLIKE
* CHANGE
* CHAR
* CHARACTER INT1
* INT2
* INT3
* SCHEMA
* SCHEMAS
* SECOND_MICROSEC OND
* CHECK
* COLLATE
* COLUMN INT4
* INT8
* INTEGER
* SELECT
* SENSITIVE
* SEPARATOR
* CONDITION
* CONNECTION
* CONSTRAINT INTERVAL
* INTO
* IS
* SET
* SHOW
* SMALLINT
* CONTINUE
* CONVERT
* CREATE ITERATE
* JOIN
* KEY
* SPATIAL
* SPECIFIC
* SQL
* CROSS
* CURRENT_DA TE
* CURRENT_TIM KEYS E
* KILL
* LABEL
* SQLEXCEPTION
* SQLSTATE
* SQLWARNING
* CURRENT_TIMESTA MP
* CURRENT_US ER
* CURSOR LEADING
* LEAVE
* LEFT
* SQL_BIG_RESUL T
* SQL_CALC_FOUND_R OWS
* SQL_SMALL_RESULT
* DATABASE
* DATABASES
* DAY_HOUR LIKE
* LIMIT
* LINEAR
* SSL
* STARTING
* STRAIGHT_JOIN
* DAY_MICROSECON D
* DAY_MINUTE
* DAY_SECOND LINES
* LOAD
* LOCALTIME
* TABLE
* TERMINATED
* THEN
* DEC
* DECIMAL
* DECLARE LOCALTIMESTAMP
* LOCK
* LONG
* TINYBLOB
* TINYINT
* TINYTEXT
* DEFAULT
* DELAYED
* DELETE LONGBLOB
* LONGTEXT
* LOOP
* TO
* TRAILING
* TRIGGER
* DESC
* DESCRIBE
* DETERMINISTI LOW_PRIORITY C
* MATCH
* MEDIUMBLOB
* TRUE
* UNDO
* UNION
* DISTINCT
* DISTINCTROW
* DIV MEDIUMINT
* MEDIUMTEXT
* MIDDLEINT
* UNIQUE
* UNLOCK
* UNSIGNED
* DOUBLE
* DROP
* DUAL
* MINUTE_MICROSECO ND
* MINUTE_SECO ND
* MOD
* UPDATE
* USAGE
* USE
* EACH
* ELSE
* ELSEIF MODIFIES
* NATURAL
* NOT
* USING
* UTC_DATE
* UTC_TIME
* ENCLOSED
* ESCAPED
* EXISTS
* NO_WRITE_TO_BINL OG
* NULL
* NUMERIC
* UTC_TIMESTAM P
* VALUES
* VARBINARY
* EXIT
* EXPLAIN
* FALSE ON
* OPTIMIZE
* OPTION
* VARCHAR
* VARCHARACTER
* VARYING
* FETCH
* FLOAT
* FLOAT4 OPTIONALLY
* OR
* ORDER
* WHEN
* WHERE
* WHILE
* FLOAT8
* FOR
* FORCE OUT
* OUTER
* OUTFILE
* WITH
* WRITE
* X509
* FOREIGN
* FROM
* FULLTEXT PRECISION
* PRIMARY
* PROCEDURE
* XOR
* YEAR_MONTH
* ZEROFILL
</details>

### 5.7 约定类军规小结

* 隔离线上线下
* 禁止未经 DBA 确认的子查询上线
* 永远不在程序端显式加锁
* 统一字符集为 UTF8
* 统一命名规范

## 六、原文链接

* [http://weibo.com/wushizhan](http://weibo.com/wushizhan)


