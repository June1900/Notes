# SQL语句学习
* SQL对大小写不敏感，在书写sql语句时推荐：sql关键字使用大写；表名，数据库名，列名等使用小写字母
## SQL基础
	* SQL查询语句：
		* SELECT DISTINCT country FROM websites 去除重复结果
		* SELECT country FROM websites 查询某一列
		* SELECT * FROM websites 查询全部列
	* SQL插入语句：
		* 在指定列插入数据：
		* INSERT INTO Websites (name, url, country) VALUES ('stackoverflow', 'http://stackoverflow.com/', 'IND')
		* 全部列插入数据
		* INSERT INTO websites (name,url,alexa,country) VALUES ('百度','https://www.baidu.com','2333','cn')
	* SQL更新语句：
		* 注意使用WHERE语句，如果不使用where，将全部更新数据
		* UPDATE websites SET country = 'CN' WHERE `name` = '百度'
	* SQL删除语句
		* 删除表中一条数据：DELETE FROM Websites WHERE name='百度' AND country='CN'
		* 删除表中全部数据：DELETE FROM table_name 或 DELETE * FROM table_name
	* SQL条件语句：
		* WHERE关键字 AND/OR关键字
			* SELECT * FROM websites WHERE name = 'Google'
			* SELECT * FROM websites WHERE name = 'Google' AND alexa = '1'
			* SELECT * FROM websites WHERE name = 'Google' OR country = 'CN'
		* WhERE子句中的运算符
			* = 等于
			* <> 不等于，在某一些数据库中也可以写为!=
			* > 大于
			* < 小于
			* >= 大于等于
			* <= 小于等于
			* BETWEEN 在某个范围内
			* LIKE 搜索某种模式
			* IN 指定针对某个列的多个可能值
		* 阅读：http://rdcqii.hundsun.com/portal/article/473.html
	* SQL查询结果排序：
		* DESC：逆序
			* SELECT * from websites ORDER BY country DESC
		* ASC：顺序（默认）
			* SELECT * FROM websites ORDER BY country 或者 SELECT * from websites ORDER BY country ASC 
## SQL高级
	* SQL分页查询： SELECT TOP（sql server数据库）, LIMIT（mysql数据库）, ROWNUM（Oracle数据库）
		*  SELECT * FROM websites LIMIT 0,3（mysql数据库为例）
	* SQL LIKE操作符：
		* SELECT * FROM websites WHERE `name` LIKE '%宝'
		* SELECT * FROM websites WHERE `name` NOT LIKE '%oo%'
	* SQL通配符
		* '%' ---- 替代 0 个或多个字符
		* '_' ---- 替代一个字符
		* '[charlist]' ---- 字符列中的任何单一字符 (mysql中使用REGEXP或NOT REGEXP来操作正则表达式)
		* '[^charlist] / [!charlist]' ---- 不在字符列中的任何单一字符
	* SQL IN操作符：
		* 允许在where语句中操作多个值--SELECT * FROM websites WHERE `name` IN ('百度','淘宝')
	* SQL between操作符：
		* 用于选取基于两个值之间的数据--SELECT * FROM websites WHERE alexa BETWEEN 12 AND 4000
	* SQL 别名：
		* 列别名
		* SELECT `name` AS n , country AS c FROM websites WHERE alexa BETWEEN 12 AND 4000
		* SELECT `name`, CONCAT(url,', ',alexa,', ',country) FROM websites
		* 表别名
		* SELECT * FROM websites AS w ,access_log AS a WHERE a.site_id = w.id 
		* 使用场景：在查询中涉及超过一个表，在查询中使用了函数，列名称很长或者可读性差，需要把两个列或者多个列结合在一起
	* SQL连接
		* INNER JOIN：如果表中有至少一个匹配，则返回行
			* SELECT Websites.name, access_log.count, access_log.date FROM Websites INNER JOIN access_log ON Websites.id=access_log.site_id
		* LEFT JOIN：即使右表中没有匹配，也从左表返回所有的行
		* RIGHT JOIN：即使左表中没有匹配，也从右表返回所有的行
		* FULL JOIN：只要其中一个表中存在匹配，则返回行
	* SQL UNION 操作符：合并两个或多个 SELECT 语句的结果
		* union：默认不允许重复值
		* union all ：允许重复值
		* SELECT country FROM Websites UNION SELECT country FROM apps ORDER BY country;
	* 数据库表拷贝
		* SELECT INTO 
		* MySQL 数据库不支持 SELECT ... INTO 语句，但支持 INSERT INTO ... SELECT语句
		* INSERT INTO Websites (name, country) SELECT app_name, country FROM apps;
	* 创建数据库：CREATE DATABASE my_db
	* 创建表：
	* SQL约束：
		* NOT NULL - 指示某列不能存储 NULL 值。
		* UNIQUE - 保证某列的每行必须有唯一的值。
		* PRIMARY KEY - NOT NULL 和 UNIQUE 的结合。确保某列（或两个列多个列的结合）有唯一标识，有助于更容易更快速地找到表中的一个特定的记录。
		* FOREIGN KEY - 保证一个表中的数据匹配另一个表中的值的参照完整性。
		* CHECK - 保证列中的值符合指定的条件。
		* DEFAULT - 规定没有给列赋值时的默认值。
	* SQL索引
		* CREATE INDEX index_name ON table_name (column_name)
		* CREATE UNIQUE INDEX index_name ON table_name (column_name)
	* 撤销索引，表，数据库
		* 删除索引-
		* 删除表-DROP TABLE table_name
		* 删除数据库-DROP DATABASE database_name
		* 只删除数据不删除表结构-TRUNCATE TABLE table_name
	* SQL alert语句
		* ALTER TABLE 语句用于在已有的表中添加、删除或修改列
	* auto increment字段
		* 一般用于表中主键，自增长
	* SQL 日期
		* 提示：如果您希望使查询简单且更易维护，那么请不要在日期中使用时间部分
	* SQL null值
		* 如果表中的某个列是可选的，那么我们可以在不向该列添加值的情况下插入新记录或更新已有的记录。这意味着该字段将以 NULL 值保存。
		* NULL 值的处理方式与其他值不同。
		* NULL 用作未知的或不适用的值的占位符。
		* 无法比较 NULL 和 0；它们是不等价的。
	* SQL 的null函数
	
	* SQL的通用数据类型
		* 数据类型定义列中存放的值的种类
* 视图（View）
	* 视图是可视化的表
	* SQL创建视图语句：CREATE VIEW view_name AS SELECT column_name(s) FROM table_name WHERE condition
	* SQL更新视图语句：CREATE OR REPLACE VIEW view_name AS SELECT column_name(s) FROM table_name WHERE condition
	* SQL撤销视图：DROP VIEW view_name
* sql函数
	* SQL Aggregate函数
		* AVG函数-返回平均值
		* count函数-返回行数
		* first函数-返回第一个记录（只有Microsoft的access支持）
		* Last函数-返回最后一个记录的值（只有Microsoft的access支持）
		* max-返回最大值
		* min-返回最小值
		* sum-返回总和
		* group by函数-可以结合一些聚合函数使用
		* having子句-where关键字无法与聚合函数一起使用，having函数可以让我们筛选分组后的各组数据
	* SQL Scalar函数
		* ucase函数-将某个字段转换为大写
		* lcase函数-将某个字段转换为小写
		* mid函数-从某个文本字段中提取字符
		* len函数-返回某个文本字段的长度
		* round函数-度某个数值字段进行小数位的四舍五入
		* now函数-返回当前的系统日期和时间
		* format函数-格式化某个字段的显示方式
## 视图
* http://www.cnblogs.com/furenjian/articles/2906115.html
# Android中sqlite数据库
* http://blog.csdn.net/linglongxin24/article/details/53230842