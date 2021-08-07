[TOC]

# 第一节 概念

## 1、关联关系概念说明

- 一对一

  夫妻关系，人和身份证号

- 一对多

  用户和用户的订单，锁和钥匙

- 多对多

  老师和学生，部门和员工



## 2、创建模型

### ①创建实体类

```java
public class Customer {
    
    private Integer customerId;
    private String customerName;
    private List<Order> orderList;// 体现的是对多的关系
```



```java
public class Order {
    
    private Integer orderId;
    private String orderName;
    private Customer customer;// 体现的是对一的关系
```

> 双向关联关系：双方都能够引用到对方
>
> Customer中能够引用Order
>
> Order中能够引用Customer
>
> 在双向关联关系中使用toString()等方法时注意避免无限死循环。



> 单向关联关系：双方中只有一方能够引用到对方
>
> Customer中没有引用Order
>
> Order中引用了Customer



### ②创建数据库表插入测试数据

```sql
CREATE TABLE `t_customer` (
	 `customer_id` INT NOT NULL AUTO_INCREMENT, 
	 `customer_name` CHAR(100), 
	 PRIMARY KEY (`customer_id`) 
 ); 

CREATE TABLE `t_order` ( 
	`order_id` INT NOT NULL AUTO_INCREMENT, 
	`order_name` CHAR(100), 
	`customer_id` INT, 
	PRIMARY KEY (`order_id`) 
); 
INSERT INTO `t_customer` (`customer_name`) VALUES ('c01');
INSERT INTO `t_order` (`order_name`, `customer_id`) VALUES ('o1', '1'); 
INSERT INTO `t_order` (`order_name`, `customer_id`) VALUES ('o2', '1'); 
INSERT INTO `t_order` (`order_name`, `customer_id`) VALUES ('o3', '1'); 
```

> 实际开发时，一般在开发过程中，不给数据库表设置外键约束。
>
> 原因是避免调试不方便。
>
> 一般是功能开发完成，再加外键约束检查是否有bug。



[回目录](index.html) [下一节](verse02.html)