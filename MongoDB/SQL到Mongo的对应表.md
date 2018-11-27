# SQL 到 Mongo 的对应表

这个列表是 PHP 版本的 [» SQL to Mongo](http://www.mongoing.com/docs/reference/sql-comparison.html) 对应表（在 MongoDB 官方手册中有更加通用的版本）。

| SQL 查询语句 | Mongo 查询语句 |
| --- | --- |
| _CREATE TABLE USERS (a Number, b Number)_ | 隐式的创建，或 [MongoDB::createCollection()](mongodb.createcollection.php). |
| _INSERT INTO USERS VALUES(1,1)_ | _$db->users->insert(array("a" => 1, "b" => 1));_ |
| _SELECT a,b FROM users_ | _$db->users->find(array(), array("a" => 1, "b" => 1));_ |
| _SELECT * FROM users WHERE age=33_ | _$db->users->find(array("age" => 33));_ |
| _SELECT a,b FROM users WHERE age=33_ | _$db->users->find(array("age" => 33), array("a" => 1, "b" => 1));_ |
| _SELECT a,b FROM users WHERE age=33 ORDER BY name_ | _$db->users->find(array("age" => 33), array("a" => 1, "b" => 1))->sort(array("name" => 1));_ |
| _SELECT * FROM users WHERE age>33_ | _$db->users->find(array("age" => array('$gt' => 33)));_ |
| _SELECT * FROM users WHERE age<33_ | _$db->users->find(array("age" => array('$lt' => 33)));_ |
| _SELECT * FROM users WHERE name LIKE "%Joe%"_ | _$db->users->find(array("name" => new MongoRegex("/Joe/")));_ |
| _SELECT * FROM users WHERE name LIKE "Joe%"_ | _$db->users->find(array("name" => new MongoRegex("/^Joe/")));_ |
| _SELECT * FROM users WHERE age>33 AND age<=40_ | _$db->users->find(array("age" => array('$gt' => 33, '$lte' => 40)));_ |
| _SELECT * FROM users ORDER BY name DESC_ | _$db->users->find()->sort(array("name" => -1));_ |
| _CREATE INDEX myindexname ON users(name)_ | _$db->users->ensureIndex(array("name" => 1));_ |
| _CREATE INDEX myindexname ON users(name,ts DESC)_ | _$db->users->ensureIndex(array("name" => 1, "ts" => -1));_ |
| _SELECT * FROM users WHERE a=1 and b='q'_ | _$db->users->find(array("a" => 1, "b" => "q"));_ |
| _SELECT * FROM users LIMIT 20, 10_ | _$db->users->find()->limit(10)->skip(20);_ |
| _SELECT * FROM users WHERE a=1 or b=2_ | _$db->users->find(array('$or' => array(array("a" => 1), array("b" => 2))));_ |
| _SELECT * FROM users LIMIT 1_ | _$db->users->find()->limit(1);_ |
| _EXPLAIN SELECT * FROM users WHERE z=3_ | _$db->users->find(array("z" => 3))->explain()_ |
| _SELECT DISTINCT last_name FROM users_ | _$db->command(array("distinct" => "users", "key" => "last_name"));_ |
| _SELECT COUNT(*y) FROM users_ | _$db->users->count();_ |
| _SELECT COUNT(*y) FROM users where AGE > 30_ | _$db->users->find(array("age" => array('$gt' => 30)))->count();_ |
| _SELECT COUNT(AGE) from users_ | _$db->users->find(array("age" => array('$exists' => true)))->count();_ |
| _UPDATE users SET a=1 WHERE b='q'_ | _$db->users->update(array("b" => "q"), array('$set' => array("a" => 1)));_ |
| _UPDATE users SET a=a+2 WHERE b='q'_ | _$db->users->update(array("b" => "q"), array('$inc' => array("a" => 2)));_ |
| _DELETE FROM users WHERE z="abc"_ | _$db->users->remove(array("z" => "abc"));_ |
