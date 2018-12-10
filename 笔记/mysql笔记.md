# 	sql完成对表中数据的CRUD的操作

### mysql 的sql 语句

```mysql
DDL 数据定义语言：定义数据库，数据表他们的结构：create(创建) drop(删除) alter(修改)
DML 数据操纵语言：主要是用来操作数据 insert(插入) update(修改) delete(删除)
DCL 数据控制语言： 定义访问权限，取消访问权限，安全设置， grant
DQL 数据查询语言： select(查询) from  子句 where 子句
```



### 数据库的创建

```mysql
create database 数据库名 character set 字符集 collate 校对规则;
```

### 数据库的删除

```mysql
drop database 数据库名
```

### 修改数据库

```mysql
alter database 数据库 character set 字符集（utf8）
```

### 查询数据库

```mysql
show databases
show create database 数据库名
select database()
```

### 切换数据库

```mysql
use 数据库名；
```

### 表结构的操作

```mysql
1. 查看表：
	查看所有表：show tables;
	查看表的创建过程：show create table 表名;
	查看表结构：desc 表名;
 

2. 创建：create table 表名(
		列名 列的类型 约束条件，
		列名 列的类型
	)
	
	列的约束：
		主键约束：primary key 
		非空约束：not null
		唯一约束：unique
	自增：auto_increment	
		
3. 删除：drop table 表名
4. 修改：alter table 表名(add,modify,change,drop)
		alter table 表名 add 列名 列的类型 列的约束
		添加列（add）: alter table tableName add score int not null
		修改列（modify）:alter table student modify sex varchar(2)
		修改列名（change）:alter table student change sex gender varchar(2)
		删除列（drop）：alter table student drop score
			
		rename table 旧表名 to 新表名；
		alter table 表名 character set 字符集；



```

###### 列的类型

|    java     |                             sql                              |
| :---------: | :----------------------------------------------------------: |
|     int     |                             int                              |
| char/string |                         char/varchar                         |
|   double    |                            double                            |
|    float    |                            float                             |
|   boolean   |                           boolean                            |
|    date     | date(YYYY-MM-DD)、time(hh:mm:ss)、datetime(YYYY-MM-DD hh:mm:ss,默认为空)、timestamp(YYYY-MM-DD hh:mm:ss,默认为系统当前时间) |
|             |                             text                             |
|             |                             blob                             |

### 插入数据

```mysql
insert into 表名（列名1，列名2，列名3）values (值1，值2，值3);
insert into student(sid,sname,sage) vlaues(0,'lizhimeng',28);
--简单写法：如果插入是全列名的数据，表名后面的列名可以省略。
insert into 表名 values(值1，值2，值3);
insert into student values(1,'zhangsan',28);
--注意：如果是插入部分列的话，列名不能省略

--批量插入数据
insert into 表名 values(值1，值2，值3),(值1，值2，值3),(值1，值2，值3);
insert into student values(0,'lizhimeng',29),(1,'张三',23),(2,'张武',23);



--查看表中数据
select * from student;
```

命令行下插入中文问题：insert into student values(11,'李四'，100);

1. 临时解决方案：set names gbk;相当于是高速MySQL服务器软件，我们当前在命令行下输入的内容是GBK。当命令窗口关闭后，在输入中文就会存在问题。
2. 永久解决办法：修改my.ini配置文件：c:\program files\mysql\mysql server5.4
   * 暂停MySQL的服务
   * 在MySQL安装路径中找到my.ini配置文件
   * 将57行的编码改成gbk
   * 保存文件退出
   * 启动MySQL服务

### 删除记录

```mysql
delete from 表名 [where 条件];
delete from student where sid=10;
delete from student;如果没有指定条件，会将表中数据一条一条全部删除掉，清空表中所有数据
delete:DML 一条一条删除表中的数据
truncate:DDL 先删除表在重建表
关于哪一条执行效率高：具体要看表中的数据量
	如果数据比较少，delete比较高效
	如果是数据比较多，truncate 比较高效

```

### 跟新表记录

```mysql
update 表名 set 列名1=列的值,列名2=列的值 [where 条件];
--将id为0的列，改成年龄为4，名字为李四
--如果参数是字符串，日期要加上单引号
update student set age=4,name='李四' where id=0;

--不带条件，则更新所有列
update student set name='张三';

```

### 查询记录

```mysql
select [distinct] [*] [列名1，列名2] from 表名 [where 条件]
distinct:去除重复的数据

--商品分类
 1. 商品分类id
 2. 分类名称
 3. 分类描述
 create table category(
 cid int primary key auto_increment,
 cname varchar(10),
 cdesc varchar(30)
 );
 
 insert into category values(null,'手机数码','电子产品，国产手机一流');
 insert into category values(null,'鞋靴箱包','江南皮鞋厂倾情打造');
 insert into category values(null,'香烟烟酒','黄鹤楼，茅台，二锅头');
 insert into category values(null,'酸奶饼干'，'娃哈哈，蒙牛酸酸乳');
 insert into category values(null,'馋嘴零食','瓜子花生，八宝粥，辣条');
 
 select * from category;
 select cname,cdesc from category; 

--所有商品
1. 商品id
2. 商品名称
3. 商品价格
4. 生产日期
5. 商品分类id

商品和商品分类：所属关系
    create table product(
        pid int primary key auto_increment,
        pname varchar(10),
        price double,
        pdate timestamp,
        cno int
    );

    insert into product values(null,'小米 note3',2999,null,1);
    insert into product values(null,'华为 p20',5999,null,1);
    insert into product values(null,'阿迪王',99,null,2);
    insert into product values(null,'浏阳河',299,null,3);
    insert into product values(null,'江小白',199,null,3);
    insert into product values(null,'小浣熊饼干',299,null,4);
    insert into product values(null,'卫龙辣条',299,null,5);
    insert into product values(null,'旺旺饼干',299,null,5);

--简单查询
--查询所有的商品
	select * from product;
--查询商品名称和价格
	select pname,price from product;
--别名查询 .as的关键字，as关键字是可以省略
	--表别名：
	select p.name,p.price from product as p;(主要用在多表查询)
	--列别名：
	select pname as 商品名称,price as 商品价格 from product;
	select pname 商品名称，price 商品价格 from product;
	
--去掉重复的值
	--查询商品所有的价格,去重
	select distinct price from product;

--select 运算查询:仅仅在查询结果上做了运算 + — * /
    select *,price * 0.8 from product;
    select * ,price * 0.8 as 折后价 from product;
--条件查询[where 关键字]
--查询商品价格 > 100元的所有商品信息
	select * from product where price > 10;
--where 后的条件写法
	--关系运算符： > >= <= = != <>
--查询商品价格在10到100之间
	select * from product where price > 10 and price < 100;
	select * from product where price between 10 and 100;
	between...and ... 包含首尾[,];
--逻辑运算符：and ,or , not
	--查询商品价格 小于35 或者商品价格大于999
	select * from product where price <35 or price > 999;

--like: 模糊查询
_ :代表的是匹配一个字符
% :代表的是匹配多个字符

--查询出名字中带有饼的所有商品 '%饼%'
	select * from product where pname like '%饼%';
--查询第二个名字是龙的所有商品 '_龙%'
	select * from product where pname like "_龙%";
--in 在某个范围中获得值
	--查询出商品分类id在 1,4,5里面的所有商品
	select * from product where pid in (1,4,5);

--排序查询：order by 关键字
	asc:ascend 升序（默认的排序 ）
	desc:descend 降序
	--1. 查询所有的商品，按价格进行降序排序（asc-升序 desc-降序）
	select * from product order by price desc;
	--2. 查询名称有 小 的商品，按价格降序排序	
	select * from product where pname like '%小%' order by price desc;


--聚合函数：
	sum(): 求和
	avg(): 求平均值
	count(): 统计数量
	max(): 最大值
	min(): 最小值
	
	--1. 获得所有商品价格的总和：
	select sum(price) from product;
	--2. 获得所有商品的平均价格：
	select avg(price) from product;
	
	--注意：where条件后面不能接聚合函数
	--查出商品价格大于平均价格的商品
	select * from product where price > (select avg(price) from product);

--分组：grpup by
	--1. 根据cno字段分组，分组后统计商品的个数
	select cno ,count(*) from product group by cno;
	
	--2. 根据cno字段分组，分组统计每组商品的平均价格，并且商品平均价格 > 60；
	select cno,avg(price) from product group by cno having avg(price) > 60;
	
	--having 关键字 可以接聚合函数的，出现在分组之后
	--where 关键字 它是不可以接聚合函数，出现在分组之前
	
	--编写顺序
	--	S..F..W..G..H..O
	select..from..where..group by.. having.. order by
	
	--执行顺序
	--	F..W..G..H..S..O
	from..where..group by..having..select..order by
	
```

### 多表查询

1. 多表之间的关系维护

   外键约束：foreign key

   * 给product 中这个cno添加一个外键约束

     alter table product add foreign key(cno) references category(cid);

   > 网上商城表实例的分析：用户购物流程
   >
   > * 用户表（用户的id，用户名，密码，手机）
   >
   >   ```mysql
   >   create table user(
   >   	uid int primary key auto_increment,
   >   	username varchar(31),
   >   	password varchar(31),
   >   	phone varchar(11)
   >   );
   >   
   >   insert into user values(1,'李智孟','111111','13812211232');
   >   ```
   >
   > * 订单表（订单编号，总价，订单时间，地址，外键用户的ID）
   >
   >   ```mysql
   >   create table orders(
   >   oid int primary key auto_increment,
   >   sum int not null,
   >   otime timestamp,
   >   address varchar(100),
   >   uno int,
   >   foreign key(uno) references user(uid)
   >   );
   >   
   >   insert into orders values(1,11,null,'深圳',1);
   >   insert into orders values(2,11,null,'深圳',1);
   >   ```
   >
   > * 商品表（商品id,商品名称，商品价格，外键cno）
   >
   >   ```mysql
   >   create table product(
   >   pid int primary key auto_increment,
   >   pname varchar(10),
   >   price double,
   >   cno int,
   >   foreign key(cno) references category(cid)
   >   )
   >   ```
   >
   > * 订单项：中间表（订单id,商品id,商品数量，订单项总价）
   >
   >   ```mysql
   >   create table orderitem(
   >   	ono int,
   >   	pid int,
   >   	foreign key(ono) references orders(oid),
   >   	foreign key(pid) references product(pid),
   >   	ocount int,
   >   	subsum double
   >   )
   >   ```
   >
   >   
   >
   > * 商品分类表（分类id,分类名称，分类描述）
   >
   >   ```mysql
   >   create table category(
   >   	cid init primary key auto_increment,
   >   	cname varchar(10),
   >   	cdesc varchar(100)
   >   )
   >   ```

2. 使用商城表完成对商品信息的多表查询

   >###### 需求分析：
   >
   >在我们的商城案例中，我的订单中包含很多信息，打开我的订单需要去查询表
   >
   >###### 技术分析
   >
   >###### 多表查询
   >
   >* 交叉连接查询   笛卡尔积:查出来是两张表的乘积，查出来的结果没有意义
   >
   >  select * from product,category;
   >
   >  过滤出有意义的数据
   >
   >  select * from product,category where cno = pid;
   >
   >* 内连接查询
   >
   >  1. 隐式内连接查询
   >
   >     select * from product p,category c where p.cno=c.cid;
   >
   >  2. 显示内连接查询
   >
   >     select * from product p inner join category c on p.cno=c.cid;
   >
   >     区别：隐式内连接：在查询出结果的基础上去做的 where 条件过滤
   >
   >     ​	    显示内连接：带着条件去查询结果，执行效率高
   >
   >* 左外连接:会将左表中的所有数据都查询出来，如果右表中没有对应的数据，用null代替
   >
   >  select * from product p left outer join category c on p.cno=c.cid;
   >
   >* 友外连接：会将右表所有数据都查询出来，如果左表没有对应数据的话，用null代替
   >
   >  select * from  product p right outer join category c on p.cno=cid;
   >
   >###### 分页查询
   >
   >- 通过关键字limit  参数1，参数2,第一个参数是索引，第二个参数显示的个数
   >
   >  select * from product limit 0,3;
   >
   >###### 子查询（了解）
   >
   >查询出（商品名称，商品分类的名称）信息
   >
   >1. 左查询
   >
   >   select p.name ,c.name from product p left outer join category c on p.cno = c.cid;
   >
   >2. 子查询
   >
   >   select p.name,(select c.name from category where p.cno = c.cid) from product p;
   >
   >* 单行子查询（>    <     >=    <=   =  <>）
   >
   >  查询出高于10号部门的平均工资的员工信息
   >
   >* 多行子查询（in  not in any all）>any  >all
   >
   >  查询出比10号部门任何员工薪资高的员工信息
   >
   >* 多列子查询（实际使用较少）  in
   >
   >  和10号部门同名同工作的员工信息
   >
   >* slect 后面接子查询
   >
   >  获取员工的名字和部门的名字
   >
   >* from 后面接子查询
   >
   >  查询emp表中经理信息
   >
   >* where 接子查询
   >
   >  薪资高于10号部门平均工资的所有员工信息
   >
   >* having 后面接子查询
   >
   >  有哪些部门的平均工资高于30号部门的平均工资

   ### 事物

   1. 查看事务提交状态

      ```mysql
      show variabes like '%commit%';
      ```

   2. 关闭事务提交功能

      ```mysql
      set autcommit = off;
      ```

   3. 进行事务操作

      ```mysql
      进行事物操作开始
      start transaction;
      进行数据操作
      ...
      结束事物操作
      	失败使用 rollback;
      	成功使用 commit；
      ```

   4. 事务特性ACID

      * 原子性

        > 指的是事务中包含的逻辑，不可分割

      * 一致性

        > 事务执行前后：数据的完整性保持一致

      * 隔离性

        > 指的是 事务在执行期间不应该受到其他事务的影响

      * 持久性

        > 指的是 事务执行完成，那么数据应该持久保存到磁盘上。

   5. 数据安全与隔离级别

      + 安全问题

        ```markdown
        1.  读问题
        脏读：
        	读到另外未提交的数据
        不可重复读：
        	一个事务读到了，另一个事务提交的数据，造成了前后两次查询结不一致
        幻读：
        	事务A首先根据条件索引得到N条数据，然后事务B改变了这N条数据之外的M条或者增添了M条符合事务A搜索条件的数据，导致事务A再次搜索发现有N+M条数据了，就产生了幻读。也就是说，当前事务读第一次取到的数据比后来读取到数据条目少。
        	两者有些相似，但是前者针对的是update或delete，后者针对的insert	
        2. 写问题
        丢失更新：
        	1.B事务如果提交或回滚，那么之前提交的A事务提交无效
        两种解决方法：
        1.悲观锁(for update),查询时等上一个事务执行完毕。
        	select * from tableName for update;
        2.乐观锁，通过数据库版本自己控制
        A事务先提交：数据库version变成1，B事务在提交的时候，比对数据库version和自己的version,不一样，不允许提交。要更新才能提交。
        ```

        

      + 隔离级别

        ```mysql
        Read Uncommitted【读未提交】
        读到另外未提交的数据，出现脏读现象
        Read Committed【读已提交】
        在a窗口执行查询结果不一致。一次是在b窗口提交事务之前，一次是在b窗口提交	之后，即一个事务读到了，另一个事务提交的数据，造成了前后两次查询结果不一致，熟称：不可重复读现象
        Repeatable Read【重复读】
        mysql 默认隔离级别就是这个该隔离级别，可以让事务在自己的会话中重复读取数据，并且不受其他事务的影响，读取前后数据不变，一直维持自己的事务。
        Serializable 【可串行化】
        该事务级别是最高的事务级别了，比前面几种都要强大一点，也就是前面几种的问题【脏读、不可重复读，幻读】都能解决。但是有一些缺点。效率低，排队处理任务
        如果有一个连接的隔离级别设置为了串行化，那么谁先打开了事务，谁就有了执行权，谁后打开事务，谁就只能等着，等前面的那个事务，提交或回滚，才能执行。但是这种隔离级别一般比较少用，容易造成性能上的问题，效率比较低。
        
        效率划分：
        读未提交 > 读已提交 > 可重复读 > 可串行化
        拦截程度，
        可串行化 > 可重复读 > 读已提交 > 读未提交
        
        读未提交 ：引发问题：脏读
        读已提交：解决 脏读 引发 不可重复读
        可重复读：解决 脏读、不可重复读 引发 幻读（insert）
        可串行化：解决脏读、不可重复读、幻读。效率太低
        ```

   6. 事务隔离性

      ```mysql
      查看事务隔离级别，mysql 重复读  oracle 读已提交
      select @@tx_isolation;
      设置事务隔离级别
      set session(or global) transaction isolation level read uncommitted;
      ```

      事务只是针对连接对象，如果再开一个连接对象，那么那是默认的提交

   ### 数据库连接池

   1. 数据库的连接对象创建工作，比较消耗性能。

   2. 一开始先在内存中开辟一块空间（集合），一开始先往池子里面放置多个连接对象。后面需要连接的话，直接从池子里面去，不要去自己创建连接了，使用完毕，要记得归还连接。确保连接对象能循环利用

      ##### 开源连接池

      + DBCP(Database Connection Pool)数据库连接池，是java数据库连接池中的一种，有Apache开发，通过数据库连接池，可以让程序自动管理数据库连接的释放和断开
      + C3P0是一个开源的JDBC连接池，它实现了数据源和JNDI绑定，支持JDBC3规范和JDBC2的标准扩展。目前使用它的开源项目有Hibernate,Spring等。

#####            DBUtils增删改查

























































