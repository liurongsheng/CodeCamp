# 数据库操作
会创建和删除数据库、创建用户、密码修改、授权及登录

# 数据类型
掌握数字类型、日期和时间、字符串等数据类型，能够根据实际情况设定对表字段设置相应的数据类型

1. 数字类型
- 整数：tinyint、smallint、mediumint、int、bigint
- 浮点数：float、double、real、decimal

2. 日期和时间
date、time、datetime、timestamp、year

3. 字符串类型
- 字符串：char、varchar
- 文本：tinytext、text、mediumtext、longtext
- 二进制（可以用来存储图片、音乐等）：tinyblob、blob、mediumblob、longblob

# 表操作
掌握创建表、删除表和修改表结构，同时能对表数据进行增加、删除、修改、查询、多表查询、主键及外键设置

1. Create table
1. Drop table
1. Alter table
1. Insert
1. Delete
1. Update
1. Select

# 索引操作
熟悉三种索引分类，能够按照对应的字段创建单表索引、唯一索引、组合字段索引
1. 索引分类
1. 创建索引
1. 删除索引

# 数据库函数
熟悉 MySQL 数据库自带的函数，能够根据实际情况运用 COUNT、AVG、MIN 等函数实现相关运算

1. COUNT
1. AVG
1. MIN
1. MAX
1. CURDATE
1. CURTIME

# Innodb 引擎和 MyIASM 引擎
悉常用的两种 MySQL引擎（Innodb 引擎和 MyIASm 引擎），能根据项目需要择相应的引擎

# 数据库设计三个范式
能按照三大范式建立冗余较小、结构合理的数据库表
1. 第一范式（确保每列保持原子性）
1. 第二范式（确保表中的每列都和主键相关）
1. 第三范式（确保每列都和主键列直接相关，而不是间接相关）

# 数据库优化技术
熟悉建表优化、査询优化和索引优化技术，能通过优化技术节约资源开销，提高数据库性能

1. 建表优化
2. 查询优化
3. 删除优化及索引优化技术

## MySQL 数据库设计三大范式
为了建立冗余较小、结构合理的数据库，设计数据库时必须遵循一定的规则
在关系型数据库中这种规则就称为范式。范式是符合某一种设计要求的总结。要想设计一个结构合理的关系型数据库，必须满足一定的范式

在实际开发中最为常见的设计范式有三个：
1. 第一范式（确保每列保持原子性）
第一范式是最基本的范式。如果数据库表中的所有字段值都是不可分解的原子值，就说明该数据库表满足了第一范式

第一范式的合理遵循需要根据系统的实际需求来定。比如某些数据库系统中需要用到 “地址” 这个属性，本来直接将 “地址” 属性设计成一个数据库表的字段就行
但是如果系统经常会访问 “地址” 属性中的 ”城市“ 部分，那么就非要将 ”地址“ 这个属性重新拆分为省份、城市、详细地址等多个部分进行存储，
这样在对地址中某一部分操作的时候将非常方便。这样设计才算满足了数据库的第一范式
![](/img/MySQL第一范式.png)

1. 第二范式（确保表中的每列都和主键相关）
第二范式在第一范式的基础之上更进一层。第二范式需要确保数据库表中的每一列都和主键相关，而不能只与主键的某一部分相关（主要针对联合主键而言）
也就是说在一个数据库表中，一个表中只能保存一种数据，不可以把多种数据保存在同一张数据库表中

比如要设计一个订单信息表，因为订单中可能会有多种商品，所以要将订单编号和商品编号作为数据库表的联合主键，如下表所示

![](/img/MySQL第二范式.png)

这样就产生一个问题：这个表中是以订单编号和商品编号作为联合主键。这样在该表中商品名称、单位、商品价格等信息不与该表的主键相关，而仅仅是与商品编号相关
所以在这里违反了第二范式的设计原则。

而如果把这个订单信息表进行拆分，把商品信息分离到另一个表中，把订单项目表也分离到另一个表中，就非常完美了

![](/img/MySQL第二范式修改.png)

这样设计，在很大程度上减小了数据库的冗余。如果要获取订单的商品信息，使用商品编号到商品信息表中查询即可

1. 第三范式（确保每列都和主键列直接相关，而不是间接相关）
第三范式需要确保数据表中的每一列数据都和主键直接相关，而不能间接相关

比如在设计一个订单数据表的时候，可以将客户编号作为一个外键和订单表建立相应的关系。而不可以在订单表中添加关于客户其它信息（比如姓名、所属公司等）的字段
如下面这两个表所示的设计就是一个满足第三范式的数据库表

![](/img/MySQL第三范式.png)

这样在查询订单信息的时候，就可以使用客户编号来引用客户信息表中的记录，也不必在订单信息表中多次输入客户信息的内容，减小了数据冗余


