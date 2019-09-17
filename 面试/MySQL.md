```java
内部连接
select vend_name,prod_name,prod_price from vendors INNER JOIN products ON vendors.vend_id=products.vend_id;
两个表之间的关系是from子句的组成部分，这里以INNER JOIN指定；联结条件用特定的ON子句而不是where子句给出，传递给ON的实际条件与传递给where的相同

外部连接
select customers.cust_id,orders.order_num from customers INNER JOIN orders ON customers.cust_id=orders.cust_id;
select customers.cust_id,orders.order_num from cusomers LEFT OUTER JOIN orders ON customers.cust_id=orders.cust_id;
```
