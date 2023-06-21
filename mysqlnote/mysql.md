# 关系型数据库设计规则

![loading-ag-530](mysql_screenshoot/5a9dd679-1ab2-47f6-8a48-c2e335e31c64.png)

ORM思想体现：

数据库中的一个表  <---> JAVA或Python中的一个类

表中一条数据    <------------>类中一个对象（或实体）

表中一个列  <--------------->类当中的一个字段（属性、field）

# 命令：

## mysql控制台登录：

-P(大写的)是端口号,不同数据库管理程序可以使用不同端口，不同版本也是，通常不会用到    -h 主机名(或者数据库所在主机的ip地址)  -p(小写)密码  -u用户名



## 创建数据库：

create database 数据库名

## 使用数据库

user database 数据库名

## 创建表

create table 表名 (字段名 字段类型,字段名 类型)

## 往表中插入数据

insert into 表名 values(字段1，字段2) 字段1字段2必须和创建表时候的顺序一样

## 修改字符编码：

show variables like 'character_%'; 查看各个功能的编码方式

![loading-ag-532](mysql_screenshoot/852a1008-bf84-4d41-aef2-0440b9316301.png)

修改数据库目录下的配置文件my.ini

在mysql标签下加入

default-character-set=utf8

mysqld标签下加入

character-set-server=utf8

collation-server=utf8_general_ci

改完之后要重启服务



8.0版本之后默认是utf8 

## mysql重置密码：

![loading-ag-534](mysql_screenshoot/b30fed04-7c6b-4758-b0cb-634f175aaf24.png)

## 单独修改数据表编码：数据库也类似,只不过table改成database

![loading-ag-536](mysql_screenshoot/be55801a-ccc1-45d3-b71a-8592813a81ee.png)



# SQL语句

是structural query language（结构化查询语言）的缩写

## 分类：

### ddl(data definition language、数据定义语言)

rename重命名、truncate清空表、表、数据库等删除用drop、删除记录用delete

![loading-ag-538](mysql_screenshoot/ad1efc91-645e-4783-beeb-efa7a6f5c89e.png)

### dml(Data Manipulation Language、数据操作（定义）语言)   增删改查、select最重要

![loading-ag-540](mysql_screenshoot/1230d690-61e8-484a-958a-49b4ae8ec836.png)

### dcl(Data Control Language、数据控制语言)

![loading-ag-542](mysql_screenshoot/31b392b6-b2d5-4023-b349-59717aec4b15.png)



## sql语言的规则与规范

\g:其实和分号一样，表示一行命令的结束

![loading-ag-544](mysql_screenshoot/67f0b7a5-6b6b-4b18-a129-3286c72bcca4.png)

字符串、日期时间类型的变量需要使用一对单引号''表示

列的别名尽量使用双引号不建议省略as



### sql大小写规范：

windows不区分大小写、

但是Linux区分大小写，必须大小写也一模一样,不过Linux中关键字、函数名、列明、列的别名是忽略大小写的

![loading-ag-546](mysql_screenshoot/82441332-0358-4086-bf54-ff52e2875cfe.png)

### 注释

![loading-ag-548](mysql_screenshoot/f8eafa11-7634-44e2-aaeb-24eb84909d14.png)

## 导入现有的数据到数据库

方式1：source 文件的全路径名

方式2：基于具体的图形化界面的工具可以导入数据



## 最基本select语句：

SELECT 字段1，字段2，。。。FROM 表明

\*  :  表中所有字段



## 别名

select字段 as 别名 from 表名即可,如   as可省略，但不建议 as 全称：alias(别名)不是好像

SELECT employee_id as id,last_name as name,salary
FROM employees;

查询出来后结果集字段名就会显示成别名，

列的别名可以使用一对双引号引起来,双引号也可以省，但部分情况不能省,如别名中包含空格

## 去除重复行

在字段前加个DISTINCT

SELECT DISTINCT department_id FROM employees



## 空值参与运算：结果也一定为空(null),注意空值和0不是一个东西

## 着重号``在表名或字段名等和sql关键字重复时，需要用着重号括起来表示这不是关键字



## 查询常数：select后有常数的话会在每一行都加上常数

![loading-ag-550](mysql_screenshoot/836f297e-5a3e-487d-90f5-b1a483bd8b47.png)



## 显示表结构：describe 表名 DESC也是一样的



## WHERE过滤数据

select \* from xx where xxx = xxx

where必须紧挨着from后面



## 运算符

1.算术运算符：+-* / div % mod

select 100 + '1' 在java中，结果是1001，因为当作字符串拼接

而在sql中+没有拼接作用只表示加法运算，会隐式转换为数值进行计算

select 100 + 'a' 此处a会当作0处理

select 100  +  null    任何与null作的运算都为null



sql中除法默认返回浮点型

取模时符号只与被模数有关，与模数无关



## 比较运算符

![loading-ag-552](mysql_screenshoot/1781e183-989d-4170-9f06-38800ec7071c.png)

一边数字一边字符会将字符隐式转换成数字（非数字字符为0，数字字符则相应数值）

如果是字符与字符比较则会根据ascii码值比较大小而不会进行隐式转换





判断时如果判断式子为 xxx=null则不会返回任何值。因为比较是要为1才返回，而null与任何值比较都是null不为1所以不会返回



### 安全等于<=>

可以让null作比较

![loading-ag-554](mysql_screenshoot/c317f7a9-a78c-4af0-88c0-587634b185bd.png)

### 常用运算符

![loading-ag-556](mysql_screenshoot/29c51cd9-80be-4971-a553-d22aea54bf38.png)

<>不等于号



between 下限 and 上限

上下限写反了就找不到了

not between 就取两边

in/not in筛选离散的数值时候用这个,后面跟的是一个集合(括号括起来，逗号分隔)，就是属于或者不属于这个集合的才被输出出来

### 模糊匹配：

%:表示不确定个数的字符包括0个

_ 一个下划线代表一个不确定字符

名字第二个字符是a的员工姓名：

![loading-ag-558](mysql_screenshoot/aa98de6f-715d-41c2-a998-315478266c1b.png)

转义字符：\如果需要查有下划线相关的就\\_



## 正则表达式

![loading-ag-560](mysql_screenshoot/58d376ad-8779-4d91-a87c-2c4e379e7b68.png)



查出数据再用，所以总在select xxxx from xxxx之后



## 逻辑运算符

![loading-ag-562](mysql_screenshoot/32784c94-2dca-457e-961c-983be5614766.png)



异或：追求的”异“，只有两个一个满足一个不满足才为真

and优先级高于or

![loading-ag-564](mysql_screenshoot/08f8fe86-970d-4297-bf6d-ee929c3e0544.png)



![loading-ag-566](mysql_screenshoot/40c6e003-cbe3-4f3d-bc06-1989b1a3ae9a.png)



# 排序与分页



## 排序：

使用order by 对查询到的数据进行排序操作

在排序的字段后加上desc变成降序，默认为升序asc

可以使用别名进行排序

![loading-ag-568](mysql_screenshoot/4195d390-ed45-4c34-bacd-27e762887220.png)



列的别名只能在ORDER BY 使用，不能在WHERE使用。

![loading-ag-570](mysql_screenshoot/f280d65c-4889-415c-833a-6f033f08c034.png)

如果where使用别名会报错

且ORDER BY 必须在WHERE 后面

ORDER BY 的字段也可以不是查询的字段



### SQL语句执行顺序

1.from 和 where 语句

2.select 语句

3.ORDER BY语句

所以from where 处无法使用select中创建的别名，因为别名还没声明。而ORDER BY 可以



### 二级排序：

在前面排序基础上还相等则按照二级排序来排

后面应该还可以整三级四级,原理是一样的，都是前面相同再使用后面的排序



## 分页

![loading-ag-572](mysql_screenshoot/19223bc1-0ac5-4bf5-90e4-a3694c5fc633.png)

需要访问那一页数据再查，否则不查，节约资源



mysql使用limit实现分页显示

![loading-ag-574](mysql_screenshoot/bae581fa-ad48-44d4-afd3-29cc8e6c0258.png)

LIMIT后第一个参数是偏移量，即往后多少条数据开始查询。20代表从21条开始查，跳过前面20条

第二个参数是每页多少条数据

公式： LIMIT (oageNo-1)\*pageSize,pageSize;

如果LIMIT从0开始0可以省略只写每页页数

即 LIMIT 0,20 等价于 LIMIT 20



### WHERE  ORDER BY   LIMIT $声明$顺序：

LIMIT 在 ORDER BY 后面，ORDER BY 在WHERE 后面



### 8.0新特性

LIMIT XXX OFFSET XXX

输入数字顺序和上面的反一下，这里偏移在后面，页数在前面



# 多表查询

防止为了查询某个信息需要来回发送多次请求和多次io才能找到某个数据，提高查找效率

因为多表查询如果分开来的话是要执行很多次才能找到。如果放到一条sql就能大幅提高效率



## 笛卡尔积

两张表，其中一张表每一条数据都与另一张表所有数据进行匹配并返回，

最终得到第一张表数据条数*第二张表数据条数的数目。这就是笛卡尔积，就是把两张表所有可能的组合都输出了



### 出现笛卡尔积错误的原因：

缺少了多表的连接条件

![loading-ag-576](mysql_screenshoot/0b3c25f3-ead2-4350-9eaf-97e27c04962a.png)



### 多表查询正确方式：需要有连接条件

查询链接条件的字段时会报歧义的错误，这时需要在select中告诉他需要查那张表中的字段

![loading-ag-578](mysql_screenshoot/8a45d168-be70-4c43-998b-b48773526834.png)

![loading-ag-580](mysql_screenshoot/e1bc0c8b-465c-4d52-a061-d46cc686c503.png)

建议：从sql优化的角度，建议多表查询时，每个字段前都指明其所在的表

这样写时sql语句过长，可读性差，可以起别名缩短语句

表名取别名在from中

![loading-ag-582](mysql_screenshoot/e1f30209-d8df-4dad-a3ba-6338f611385f.png)

#### 如果起了别名就不能用原名，只能用别名



## 多表查询分类：等值连接，非等值连接、自链接，非自连接、内连接，外连接

### 非等值连接例子：

查询员工工资等级：因为等级是一个工资范围，而等级和工资又分别在两张表，所以需要非等值连接

![loading-ag-650](mysql_screenshoot/4c69cf85-403d-4c3e-91f4-8a9b6b8a1c08.png?msec=1687332037953)

### 自连接例子

查询员工id，员工姓名及其管理者的id和姓名

![loading-ag-652](mysql_screenshoot/7d9ab3a0-8e10-4b65-bb86-589b0ce7a203.png?msec=1687332037953)

## 内连接、外连接

![loading-ag-654](mysql_screenshoot/2d80d2a4-b313-45c2-a80a-620cae3712f4.png?msec=1687332037954)

就是两个表没有关系的行也列出来，因为有些关联的地方是null时就会少查出一点数据

外连接分类：左外连接、右外连接、满外连接

### SQL92的外连接：

使用+

![loading-ag-656](mysql_screenshoot/4f21f3ca-4c35-4401-982d-9a27e0e30c74.png?msec=1687332037954)

哪边短哪边给个+号

### SQL99语法使用 JOIN....ON 实现多表查询

#### 内连接：

表名 join 表名 on 合并条件

还有的话再 join 再 on

#### 外连接：

左外连接：left join 、右外：right join

#### 满外连接：

FULL OUTER JOIN 、MySQL不支持

#### union、union all

union：需要去重、效率低

union all：效率高，但交集会重复

所以当没有交集用union all效率最高

有交集用union保证数据不重复

![loading-ag-658](mysql_screenshoot/a9aac8f7-0451-4986-ad38-a8500d1c7e1b.png?msec=1687332037955)

![loading-ag-660](mysql_screenshoot/a0c761fa-fd32-43f8-ac3c-a60789e8f160.png?msec=1687332037955)

下面两个图可以用上面的union all组合而来

所以重要的是实现上面五个图

### sql99新特性1：自然连接

会自动查询两张连接表中所有相同字段然后进行等值连接

虽然简洁但是不灵活，比较死板

### sql99新特性2：USING

![loading-ag-662](mysql_screenshoot/3ded8254-795c-4fef-8875-9e6997eba9dd.png?msec=1687332037955)

简单来说就是指定用哪个字段来连接

# 函数

![loading-ag-664](mysql_screenshoot/b4cd52ea-01a0-4f8e-85f1-ec2ebfbfba6d.png?msec=1687332037956)

![loading-ag-666](mysql_screenshoot/3b85dc7a-32b4-4022-943e-183646e40660.png?msec=1687332037956)

## 两种SQL函数

![loading-ag-668](mysql_screenshoot/c1f745f7-27b4-4c55-ad23-3de82425fa4e.png?msec=1687332037956)

### 单行函数：

进去一个参数出来一个结果

![loading-ag-670](mysql_screenshoot/322423de-0985-42b8-88bc-cb3b55c96c5a.png?msec=1687332037956)

### 多行函数:

进去多个参数出来一个结果

## 数值函数

![loading-ag-672](mysql_screenshoot/0d58aa71-074d-401f-a328-fa9bca5aece6.png?msec=1687332037958)


















