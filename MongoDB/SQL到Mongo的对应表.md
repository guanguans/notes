# SQL 到 Mongo 的对应表

这个列表是 PHP 版本的 [» SQL to Mongo](http://www.mongoing.com/docs/reference/sql-comparison.html) 对应表（在 MongoDB 官方手册中有更加通用的版本）。

| SQL 查询语句 | Mongo 查询语句 |
| --- | --- |
|CREATE TABLE USERS (a Number, b Number)       | 隐式的创建，或 [MongoDB::createCollection()](mongodb.createcollection.php). |
|INSERT INTO USERS VALUES(1,1)       |$db->users->insert(array("a" => 1, "b" => 1));       |
|SELECT a,b FROM users       |$db->users->find(array(), array("a" => 1, "b" => 1));       |
|SELECT * FROM users WHERE age=33       |$db->users->find(array("age" => 33));       |
|SELECT a,b FROM users WHERE age=33       |$db->users->find(array("age" => 33), array("a" => 1, "b" => 1));       |
|SELECT a,b FROM users WHERE age=33 ORDER BY name       |$db->users->find(array("age" => 33), array("a" => 1, "b" => 1))->sort(array("name" => 1));       |
|SELECT * FROM users WHERE age>33       |$db->users->find(array("age" => array('$gt' => 33)));       |
|SELECT * FROM users WHERE age<33       |$db->users->find(array("age" => array('$lt' => 33)));       |
|SELECT * FROM users WHERE name LIKE "%Joe%"       |$db->users->find(array("name" => new MongoRegex("/Joe/")));       |
|SELECT * FROM users WHERE name LIKE "Joe%"       |$db->users->find(array("name" => new MongoRegex("/^Joe/")));       |
|SELECT * FROM users WHERE age>33 AND age<=40       |$db->users->find(array("age" => array('$gt' => 33, '$lte' => 40)));       |
|SELECT * FROM users ORDER BY name DESC       |$db->users->find()->sort(array("name" => -1));       |
|CREATE INDEX myindexname ON users(name)       |$db->users->ensureIndex(array("name" => 1));       |
|CREATE INDEX myindexname ON users(name,ts DESC)       |$db->users->ensureIndex(array("name" => 1, "ts" => -1));       |
|SELECT * FROM users WHERE a=1 and b='q'       |$db->users->find(array("a" => 1, "b" => "q"));       |
|SELECT * FROM users LIMIT 20, 10       |$db->users->find()->limit(10)->skip(20);       |
|SELECT * FROM users WHERE a=1 or b=2       |$db->users->find(array('$or' => array(array("a" => 1), array("b" => 2))));       |
|SELECT * FROM users LIMIT 1       |$db->users->find()->limit(1);       |
|EXPLAIN SELECT * FROM users WHERE z=3       |$db->users->find(array("z" => 3))->explain()       |
|SELECT DISTINCT last_name FROM users       |$db->command(array("distinct" => "users", "key" => "last_name"));       |
|SELECT COUNT(*y) FROM users       |$db->users->count();       |
|SELECT COUNT(*y) FROM users where AGE > 30       |$db->users->find(array("age" => array('$gt' => 30)))->count();       |
|SELECT COUNT(AGE) from users       |$db->users->find(array("age" => array('$exists' => true)))->count();       |
|UPDATE users SET a=1 WHERE b='q'       |$db->users->update(array("b" => "q"), array('$set' => array("a" => 1)));       |
|UPDATE users SET a=a+2 WHERE b='q'       |$db->users->update(array("b" => "q"), array('$inc' => array("a" => 2)));       |
|DELETE FROM users WHERE z="abc"       |$db->users->remove(array("z" => "abc"));       |


## 内嵌、引用选择

| 更适合内嵌 | 更适合引用 |
| --- | --- |
| 子文档较小 | 子文档较大 |
| 数据不会定期改变 | 数据经常改变 |
| 最终数据一致即可 | 中间阶段的数据必须一致 |
| 文档数据小幅增加 | 文档数据大幅增加 |
| 数据通常需要执行二次查询才能获得 | 数据通常不包含在结果中 |
| 快速读取 | 快速写入 |
