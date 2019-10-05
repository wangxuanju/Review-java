
# 选择数据库
```java
show databases;显示数据库列表
use t1;使用t1数据库
show tables;显示ti数据库中有哪些表
show columns from customers;显示customers表的内容；
```
# 建表
```java
CREATE TABLE customers
(
  cust_id      int       NOT NULL AUTO_INCREMENT,每当增加一行时自动增量
  cust_name    char(50)  NOT NULL ,
  cust_address char(50)  NULL ,
  cust_city    char(50)  NULL ,
  cust_state   char(5)   NULL ,
  cust_zip     char(10)  NULL ,
  cust_country char(50)  NULL ,
  cust_contact char(50)  NULL ,
  cust_email   char(255) NULL ,
  PRIMARY KEY (cust_id)因为cust_id是唯一的所以适合作为主键
) ENGINE=InnoDB;引擎类型为InnoDB
为表赋值
INSERT INTO customers(cust_id, cust_name, cust_address, cust_city, cust_state, cust_zip, cust_country, cust_contact, cust_email)
VALUES(10001, 'Coyote Inc.', '200 Maple Lane', 'Detroit', 'MI', '44444', 'USA', 'Y Lee', 'ylee@coyote.com');
更新表
alter table customers add cust_phone char(20);添加一列
alter table customers drop columns cust_phone;删除列cust_phone
删除表
drop talbe customers;
重命名表
rename table customers to customers1;
rename table customers to customers1,customers2 to customers3,customers4 to customers5;对多个表重命名
```
# 检索列
```java
select prod_name form products;从表中检索一个名为prod_name的列
select prod_id,prod_name,prod_price from products;检索多个列 
select * from products;检索所有的列

限制结果
select prod_name from products limit 5;mysql返回不多于5行
select prod_name from products limit 5,5;mysql返回的值从第五行开始，检索接下来的五行
```
# 排序
```java
select prod_id,prod_price,prod_name from products order by prod_price DESC;默认排序是升序（A-Z），进行降序用DESC关键字
select prod_id,prod_price,prod_name from products order by prod_price DESC,prod_name;排序时对prod_price按降序，prod_name按升序 

where子句
select prod_id,prod_price,prod_name from products where vend_id=1003 and prod_price<=10;and操作符
select prod_name,prod_price from products where vend_id=1002 or vend_id=1003;or操作符

select prod_name,prod_price from products where vend_id=1002 or vend_id=1003 and prod_price>=10;
允许where子句无数次包含or 和 and 操作符；并且处理or操作符前，优先处理and操作符
select prod_name,prod_price from products where(vend_id=1002 or vend_id=1003)and prod_price>=10;圆括号优先级高

select prod_name,prod_price from products where vend_id in (1002,1003) order by prod_name;IN操作符指定条件范围
select prod_name,prod_price from products where vend_id=1002 or vend_id=1003 order by prod_name;In操作符完成与or相同的功能
select prod_name,prod_price from products where vend_id not in (1002,1003) order by prod_name;not操作符
mysql允许not对in/between/exists子句取反

通配符
select prod_id,prod_name from products where prod_name LIKE 'jet%';使用了搜索模式‘jet%’，检索以jet开头的词，%告诉mysql，jet之后的任意字符
（根据mysql的配置方式，搜索可以区分大小写）
select prod_id,prod_name from products where prod_name LIkE '%anvil%';表示可以匹配任何包含文本anvil的值，不论之前或之后出现什么字符
（通配符可以在搜索模式中任意位置使用，并且可使用多个通配符）
select prod_name from products where prod_name LIKE 's%e';找出以s开头以e结尾的产品；通配符出现在搜索模式的中间；
（除了一个字符或多个字符外，%还能匹配0个字符。即%代表搜索模式中给定的0/1/多个字符）

select prod_id,prod_name from products where prod_name LIKE '_ ton anvil';下划线只匹配单个字符，不能匹配0个或多个字符。
select prod_id,prod_name from products where prod_name LIKE '% ton anvil';

函数
AVG（）返回某列的平均值
COUNT（）返回某列的行数
MAX（）返回某列的最大值
MIN（）返回某列的最小值
SUM（）返回某列的和
select AVG(prod_price) as avg_price from products where vend_id=1003;AVG函数返回所有产品的平均价格

分组
一般在使用order by 子句时，应该也给出group by 子句；这是保证数据正确排序的唯一方法；不要仅使用group by子句 
select order_num,SUM(quantityitem_price) as ordertotal from orderitems group by order_num having SUM(quantityitem_price)>=50; 
select order_num,SUM(quantityitem_price) as ordertotal from orderitems group by order_num having SUM(quantityitem_price)>=50 order by ordertotal; group by子句用来按订单号order_num分组数据；以便SUM(*)函数能够返回总计的订单价格；having子句过滤数据，使得只返回总计订单数大于等于50的订单； 最后用order by 子句排序输出

子查询
select order_num from orderitems where prod_id='TNT2';
select cust_id from orders where order_num IN(20005,20007);
把第一个查询变为子查询组合的两个查询
select cust_id from orders where order_num IN(
                            select order_num from orderitems where prod_id = 'TNT2');
                            
                            
把子查询分解为多行并且适当的进行缩进，能简化子查询的使用                            
select cust_name,cust_contact from customers where cust_id IN(10001,10004);
select cust_name,cust_contact from customers where cust_id IN(
                            select cust_id from orders IN(
                                            select order_num from orderitems where prod_id='TNT2'));
 where子句中使用子查询能编写出功能很强并且很灵活的SQL子句。对于能嵌套的子查询数目没有限制，实际中由于性能的限制不能嵌套太多

UNION ALL
select vend_id,prod_id,prod_price from products where prod_price<=5 union all
                                      select vend_id,prod_id,prod_price from products where vend_id in(1001,1002);
使用union all，mysql不取消重复的行（如果需要每个条件的匹配行全部出现（包括重复行），必须使用union all而不是where）
```
# 连接
```java
内部连接
select vend_name,prod_name,prod_price from vendors INNER JOIN products ON vendors.vend_id=products.vend_id;
两个表之间的关系是from子句的组成部分，这里以INNER JOIN指定；联结条件用特定的ON子句而不是where子句给出，传递给ON的实际条件与传递给where的相同

外部连接
select customers.cust_id,orders.order_num from customers INNER JOIN orders ON customers.cust_id=orders.cust_id;
select customers.cust_id,orders.order_num from cusomers LEFT OUTER JOIN orders ON customers.cust_id=orders.cust_id;
关键字OUTER JOIN来指定联结的类型

自连接
select p1.prod_id,p1.prod_name from products as p1,products as p2 where p1.vend_id=p2.vend_id and p2.prod_id='DTNTR';
两个表实际是形同的表，因此products表在from子句中出现了两次；为解决此问题使用了表别名，products的第一次出现为p1,第二次为p2

插入完整的行
insert into customers (cust_name,cust_city,cust_country) values ('Bill','shanghai','china');
insert into cusomers(cust_name,cust_city,cust_country) values('bill','shanghai','china'),('lily','shanghai','china');

更新数据
update customers set cust_name='The Fudds',cust_emain='elemer@fudd.com' where cust_id=10005;更新多个列时，只需要用单个set命令

删除数据
为删除某个列的值可以将它设为空
update customers set cust_email=NULL where cust_id=10005;用Null来去除cust_email列中的值
delete from customers where cust_id = 10006;delete from 要求指定从中删除数据的表名，where子句过滤要删除的行
（delete删除整行而不是整列；为了删除指定的列，请使用update语句）
```

# 视图
```java
create view productcustomers as select cust_name,cust_contact,prod_id from customers,orders,orderitems 
                                                                  where customers.cust_id=orders.cust_id
                                                                  and orderitems.order_num=orders.order_num;
select cust_name,cust_contact from productcustomers where prod_id='TNT2';
drop view productcustomers;删除视图
```
# 存储过程
```java
delimiter //
create procedure productpricing()
begin
   select Avg(prod_price) as priceaverage from products; 
end //
存储过程命名为productpricing，用create procedure productpricing()语句定义。如果存储过程接受参数，它们将在（）中列举出来； 没有参数，后跟的()仍然需要。begin和end语句用来限定存储过程体，过程体本来仅是一个简单的select语句；

call productpricing();执行刚创建的存储过程并显示返回的结果；因为存储过程实际上是一种函数，所以存储过程名后面要有（）符号
drop procedure productpricing;删除刚创建的存储过程，注意没有使用后面的（）；
```
```
delimiter //此步骤改变为//表示结束
create procedure cuncucustome(in id int unsigned)
begin
delete from customer where cust_id = id;
end
//


call cuncucustomer(3)；从customer表中删除cust_id=3的数据
drop procedure cuncucustomer;删除存储过程
```
# 游标
```java
delimiter //
create procedure processorders()
begin
declare ordernumbers cursor
for select order_num from  orders;
end //
declare命名游标，并定于相应的select语句，根据需要带where和其它的子句；本例命名的游标为ordernumbers(存储过程处理完成后，游标就消失；它仅局限于存储过程）
open ordernumbers;处理open语句时执行查询，存储检索出的数据以供浏览和滚动；
close ordernumbers;close释放游标使用的所有内存和内部资源，因此在每个游标不再需要时都应该关闭；


create procedure processorders()
begin 
    declare o TNT;
    declare ordernumbers cursor for select order_num from orders;
    open ordernumbers;
    fetch ordernumbers into o;
    close ordernumbers;
end;
fetch用来检索当前行的order_num列（将自动从第一行开始）到第一个名为o的局部变量中；
```
# 事务
## 控制事务处理
start transaction;用来标识事务的开始；
## 使用rollback
```java
使用rollback——此命令用来回退（撤销）mysql语句

select * from ordertotals;
start transaction;开始一个事务处理
delete from ordertotals;删除ordertotals中的所有行
select * from ordertotals;验证ordertotals确实为空
rollback;   此语句回退start transaction之后的所有语句
select * from ordertotals;（rollback只能在一个事务处理内使用，即执行一条start transaction命令之后）
```
## 使用commit
使用commit——隐含提交即提交（写或保存）操作是自动进行的 但是事务处理中，提交不会隐含的进行；为进行明确的提交，使用commit语句
```java
start transaction：
delete from orderitems where order_num=20010;
delete from order where order_num=20010;
commit;最后的commit语句仅在不出错时写出修改；
隐含事务关闭：当commit或rollback语句执行后，事务会自动关闭
```
