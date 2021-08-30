# Salesforce 零基础开发入门学习

想学 Salesforce，日英双语不好怎么办？Cover by 大佬 [zero.zhang](https://www.cnblogs.com/zero-zyq/)
<!--more-->

---

## 一、Salesforce 相关网站

salesforce 开发者官网：[https://developer.salesforce.com/](https://developer.salesforce.com/)

注：此链接可以作为salesforce的门户，找到所需要的大部分资源，比如IDE，PDF开发文档等等。

salesforce 教学视频：[https://trailhead.salesforce.com/zh-CN](https://trailhead.salesforce.com/zh-CN)

注：此链接为您提供全套教学以及考证指导，无论您是管理员、用户还是开发人猿。

IDE：[https://developer.salesforce.com/tools/vscode/](https://developer.salesforce.com/tools/vscode/)

注：此链接方便无基础人员安装IDE开发环境，里面有详细的操作说明。

---

## 二、变量基础知识，集合，表达式，流程控制语句

salesforce 如果简单的说可以大概分成两个部分：**Apex，VisualForce Page。**

Apex 基本和 Java 语法类似，有如下几种常用的基本变量 Integer，String，Decimal，Double，Long，Boolean，ID。

集合常用的对象：List<T>，Set<T>，Map<T>，均无子类。	

时间日期常用对象：Datetime，Time，Date。

其他：Object，sObject(与数据库相关，以后会讲)

与Java一个最大的区别是：Apex 中基本对象的初始值均为 null。

---

## 三、sObject及DML操作（SOQL）

详细了解点击[这里](https://developer.salesforce.com/trailhead/en/module/apex_database)，可前往官方网站学习。

数据库的操作比之Java等语言不同，salesforce使用的是Force.com平台数据库，其数据表一行数据可以理解成一个sObject变量。什么是sObject？

### 1. sObject

官方定义，sObject指的是存储在Force.com平台数据库的任何对象。

在Apex中只能使用SOAP API对象名称中声明的一行数据。比如Account数据表对应的API名称为Account，则`Account account = new Account();`的`account`就是一个sObject对象。

有两种快捷方式自定义对象：①設定・オブジェクトマネージャ・作成　②設定・作成(ホーム)

### 2. SOQL

SOQL全称为Salesforce Object Query Language。通过SOQL语句可以对sObject做CRUD操作。

Apex代码通过表以及列对应的API Name进行CRUD。

```sql
/*sObject有常用的两种初始化方式
	第一种为常见的new
	第二种为new时将参数作为构造函数内容穿进去，多个参数使用','分隔   
*/
Student__c student1 = new Student(Name__c='student1');
Student__c student2 = new Student();
student2.Name__c = 'student2';
 
//增加一条学生记录--> insert
insert student1;//SOQL 增加记录的简便写法，同Database.insert(student1),详见文档
insert student2;
//修改一条学生记录--> update
student1.Name__c = 'student update';
update student1;//SOQL修改记录简便写法，同Database.update(student1)
 
/*增加或修改一条学生记录 upsert
    upsert原理：upsert通过是否存在此ID来判断此条记录是否存在，
    1.如果不存在此ID则执行insert操作；
    2.如果存在并且只存在一个ID，则执行update操作；
    3.存在并且存在多个ID，则抛出DMLException
*/
//当上方执行 insert语句时，Id便赋予student1，所以下方代码执行 update操作
student1.Name__c = 'student upsert';
upsert student1;//SOQL简便写法，同Database.upsert(student1);
 
//删除一条学生记录 delete
delete student2;//SOQL简便写法，同Database.delete(student2);
 
//注意：进行DML操作时有可能发生DMLException，所以在进行DML操作时最好进行try,catch处理。
//e.g.:
try {
      insert student1;
} catch(DMLException e) {
      // TODO
} finally {
      // TODO
}
```

查询语句返回List<sObject>数据时，查询语句也可以进行相应的复杂处理，例如进行Where、include、limit等操作，以后会详细探讨SOQL语法细节和多表联查，这里仅简单描述：

```sql
/*Apex为参数传递提供了一种便捷的方式，使用‘：’符号来声明查询语句中使用的变量，类似于Java中的PreparedStatement。查询有两种方式：
	第一种通过[select...]方式来查询，此种方式不利于SQL扩展，故不推荐
	第二种通过构造查询字符串，通过Database.query(queryString)方式来检索，此方法灵活性扩展性强，故推荐
*/
//查询列表
String args1 = '%zhang%';
String args2 = 'zhangsan';
List<Student__c> students = [select Id,Name__c from Student__c where Name__c like :args1 limit 10000];//查询名称含zhang的学生列表
/*
上述语句等同与:
String query = 'select Id,Name__c from Student__c where Name__c like :args1 limit 10000';
List<Student__c> students = Database.query(query);
*/
//查询表数据条数
String countQuery = 'select count(Id) from Student__c where Name__c = :args2 ';//查询名称为zhangsan的学生个数
```

**需要注意的是：在Force.com平台数据库中，查询不能使用'*'符号代表全部字段，如果查询全部字段需全部列出来；而且salesforce对查询记录条数以及DML操作次数均有严格的限制，查询条数一次不能超过50000条，DML操作一次不能超过10000条，如果超过限制则抛出异常。如果需要大量的进行DML操作，请使用批处理方式进行数据处理。**

---

## 四、多表关联下的SOQL以及表字段Data Type详解


