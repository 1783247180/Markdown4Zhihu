# DML

## insert

```sql
insert 表名(字段名1，字段名2) values(值1，值2);
```

字符和日期型数据应包含在单引号中。

![image-20200713162555124](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/mysql-hand/image-20200713162555124.png)

## delete

## update

使用UPDATE 语句更新数据。

可以一次更新多条数据。

如果需要回滚数据，需要保证在DML前，进行设置：SET  
  AUTOCOMMIT = FALSE;

## select

```sql
select 字段名 from 表名 where name = "name";
```

查询表达式可以使用[ AS] alias-name为其赋予别名。

别名可用于 GROUP BY， ORDRE BY或 HAVING子句。

### where-比较运算符

like  'condition'

condition中%(匹配多个字符)和_(匹配一个字符)

![image-20200713145904446](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/mysql-hand/image-20200713145904446.png)

### order by

```sql
SELECT field1, field2 FROM table_name1
ORDER BY field1 [ASC [DESC]], [field2...] [ASC [DESC]]
```

### group by

GROUP BY 语句根据一个或多个列对结果集进行分组。

```sql
select 字段组A from 表名 GROUP BY 字段组B HAVING condition;
```

字段组A-聚合函数=字段组B

字段组B相同的数据放在一起

having子句在分组后对组记录进行筛选。condition必须在字段组A

### cas-when

![image-20200713161418567](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/mysql-hand/image-20200713161418567.png)

```sql
SELECT last_name,  job_id,  salary,
    CASE   job_id   WHEN  'IT_PROG'  THEN 1.10*salary
                    WHEN  'ST_CLERK' THEN 1.15*salary
                    WHEN  'SA_REP' THEN  1.20*salary
                    ELSE  salary   
    END  "REVISED_SALARY"
FROM employees;
```

![image-20200713161732509](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/mysql-hand/image-20200713161732509.png)

### limit

限制查询结果返回数量：

```sql
SELECT * FROM table_name LIMIT 2; // 一个数字限制查询结果数量为 2 条 。
SELECT * FROM  table_name  LIMIT 2,3 ;// 从第三个开始（第一个为0），返回三条。 
```

### 连接

- INNER JOIN（内连接,或等值连接）：获取两个表中字段匹配关系的记录。
- LEFT JOIN（左连接）：获取左表所有记录，即使右表没有对应匹配的记录。
- RIGHT JOIN（右连接）：与 LEFT JOIN 相反，用于获取右表所有记录，即使左表没有对应匹配的记录。

SELECT a.id,b.count FROM tbl a INNER JOIN tb2 b ON a.id = b.id;

等价于

SELECT a.id,b.author FROM tbl a, bl b WHERE a.id = b.id;

### 日期与数字

SQL语句中的数学表达式：对于数值和日期型字段，可以进行 “加减乘除” select id+10 from user where id =1;

# DDL

create table

drop table

alter table

## create index

```sql
create index 索引名 on 表名(字段名);
```

## drop index

```sql
drop index 索引名
```

# DCL

## grant

```sql
grant 权限类型 on 表名 to 用户名
grant 角色名 to 用户名
```

## revoke

```sql
revoke 权限类型 on 表名 from 用户名
revoke 角色名 from 用户名
```

**权限类型**

all，select，insert，update，delete

**表名**

数据库名.* （表示该数据库下的所有表），视图名

**角色名**

dba （数据库管理员）

commit

rollback

# 函数

## 组函数

| avg   | 求平均值     |

| ----- | ------------ |

| count | 统计行的数量 |

| max   | 求最大值     |

| min   | 求最小值     |

| sum   | 求累加和     |


不能在where子句中使用组函数

可以在having子句中使用组函数

## 大小写函数

![image-20200713151636036](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/mysql-hand/image-20200713151636036.png)



## 字符控制函数

concatenate 美 /kɑn'kætə,net/  连接

substr 子串

length

instr 定位子串

lpad 左填充

rpad 右填充

replace 替换

![image-20200713151651873](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/mysql-hand/image-20200713151651873.png)

## 数字函数

round 四舍五入

truncate 截断

mod 求余

![image-20200713155059536](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/mysql-hand/image-20200713155059536.png)

## 日期函数

```
str_to_date(string,format)
DATE_FORMAT(date,format)
```

![image-20200713155114734](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/mysql-hand/image-20200713155114734.png)

![image-20200713155447860](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/mysql-hand/image-20200713155447860.png)

# 事务

在MySQL中，默认情况下，事务是自动提交的，也就是说，只要执行一条DML(insert、update、delete)语句就开启了事物，并且提交了事务

执行select 语句的时候是不会开启事务的

关闭事务自动提交

```sql
SET  AUTOCOMMIT = FALSE;
```

## 事务可能出现的问题

事务并发运行导致的问题:幻读,脏读,不可重复读

## 事务隔离级别

（1）read uncommitted 未提交读

所有事务都可以看到没有提交事务的数据。

（2）read committed 提交读

事务成功提交后才可以被查询到。

（3）repeatable 重复读

同一个事务多个实例读取数据时，可能将未提交的记录查询出来，而出现幻读。mysql默认级别

（4）Serializable可串行化

强制的进行排序，在每个读读数据行上添加共享锁。会导致大量超时现象和锁竞争。





# 用户基本操作

## 创建用户

CREATE USER 'wan' IDENTIFIED by  'root';

如果创建的用户登录不了则重启mysql服务

## 删除用户

drop user username

## 修改用户密码

ALTER USER 'wan' IDENTIFIED WITH mysql_native_password BY 'wan';

flush privileges;

## flush privileges

flush privileges 命令本质上的作用是将用户信息/权限信息提取到内存里。MySQL用户数据和权限有修改后，希望在"不重启MySQL服务"的情况下直接生效，那么就需要执行这个命令。

# 数据位数



| 数据类型 | 储存         | 范围（有符号）（无符号） | 格式                | 默认值                                                       |

| -------- | ------------ | ------------------------ | ------------------- | ------------------------------------------------------------ |

| tinyint  | 1字节（8位） | -128~127  0~255          |                     | 如果代替boolean类型则设置为1(启用)<br />如果代替enum类型则设置为0 |

| int      | 4字节        |                          |                     |                                                              |

| bigint   | 8字节        |                          |                     |                                                              |

| year     | 1字节        |                          | YYYY                | 不支持默认值                                                 |

| date     | 3字节        |                          | YYYY-MM-DD          | 不支持默认值                                                 |

| datetime | 8字节        |                          | YYYY-MM-DD HH:MM:SS | CURRENT_TIMESTAMP<br />还要设置ON UPDATE CURRENT_TIMESTAMP   |

|          |              |                          |                     |                                                              |

|          |              |                          |                     |                                                              |

|          |              |                          |                     |                                                              |


# int类型与varchar类型

int的长度并不影响数据的存储精度，长度只和显示有关

首先 mysql 5.X 以上的版本的 定义中 表示的字符长度，如上varchar（20）你既可以添加20个英文字符，也可以添加二十个中文字符。 表示的字符长度

# 技巧

**技巧1 使用`TINYINT`来代替`ENUM`**

`ENUM`增加新值要进行`DDL`操作

**技巧2 明知只有一条查询结果，那请使用 “LIMIT 1”**

“LIMIT 1”可以避免全表扫描，找到对应结果就不会再继续扫描了。

**技巧3 如何选择合适的数据类型**

能用TINYINT就不用SMALLINT，能用SMALLINT就不用INT。

1.1 在MySql中如何定义像Java中类型的Boolean类型数据？其实，mysql中 是没有直接定义成Boolean这种数据类型，它只能 定义成 tinyint(1) ；当booean 等于1 代表true,boolean 等于2的时候代表false；

1.2 Long型数据对应MySQL数据库中 bigint 数据类型；

**技巧4 禁止大表Join和子查询**

能写一个几十行、几百行的SQL语句是不是显得逼格很高？然而，为了达到更好的性能以及更好的数据控制，你可以将他们变成多个小查询。

**技巧5 字段not null并设计默认值**

不要以为 NULL 不需要空间，其需要额外的空间，并且，在你进行比较的时候，你的程序会更复杂

**技巧6 为获得相同结果集的多次执行，请保持SQL语句前后一致**

这样做的目的是为了充分利用查询缓冲。

比如根据地域和产品id查询产品价格，第一次使用了：

```sql
select * from product where id < 5 and region = 'changsha'; 
```

那么第二次同样的查询，请保持以上语句的一致性，比如不要将where语句里面的id和region位置调换顺序。

**技巧7 禁止使用 “ SELECT \* ”**

如果不查询表中所有的列，尽量避免使用 SELECT *，因为它会进行全表扫描，不能有效利用索引，增大了数据库服务器的负担，以及它与应用程序客户端之间的网络IO开销。

**技巧8 哪些列需要索引**

JOIN 子句里面的列建立索引

where 子句后面的列建立索引

ORDER BY 的列建立索引

**技巧9 不要储存大文件到数据库**

禁止在数据库中存储大文件，例如照片，可以将大文件存储在对象存储系统，数据库中存储路径

**技巧10 使用INT UNSIGNED存储IPv4**

很多程序员都会创建一个 VARCHAR(15) 字段来存放字符串形式的IP而不是整形的IP。如果你用整形来存放，只需要4个字节，并且你可以有定长的字段。而且，这会为你带来查询上的优势，尤其是当你需要使用这样的WHERE条件：IP between ip1 and ip2。

ip转成int 使用 INET_ATON 函数 (address to number)

int转成ip使用 INET_NTOA 函数

![img](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/mysql-hand/20190919111105285-1594642644455.png)

当用unsigned int 存储IP地址之后,可以方便的使用 between and进行ip地址比较

```sql
SELECT * FROM  USER  WHERE INET_NTOA(ip) BETWEEN '192.168.1.1' AND '192.168.1.3';
结果是INET(ip)为
192.168.1.1 192.168.1.2 192.168.1.3
的三条记录
```

**技巧11 日期储存**

存储年使用`year`，存储日期使用`date`，存储时间使用`datetime`
\> `datetime`使用`DEFAULT CURRENT_TIMESTAMP` 和 `ON UPDATE CURRENT_TIMESTAMP`定义默认值和默认更新

**技巧12 手机号储存**

使用`varchar(20)`存储手机号，不要使用整数
\> 牵扯到国家代号，可能出现+/-/()等字符，例如+86
\> 手机号不会用来做数学运算
\> `varchar`可以模糊查询，例如like ‘138%’

**技巧13  禁止%开头的模糊查询**

会导致不能命中索引，全表扫描

**技巧14 or改成in**

同一个字段上的`OR`必须改写成`IN`