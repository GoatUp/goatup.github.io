# Salesforce Apex


Apex 是 Salesforce.com 开发的专有语言。类似于 Java 语法，也是一种强类型，面向对象的编程语言。

<!--more-->

## 第1章 了解 Apex 语法

Apex 代码通常包含许多我们可能从其他编程语言熟悉的东西。

**变量声明**：作为强类型语言，必须使用 Apex 中的数据类型声明每个变量。如下面的代码（下面的截图）所示，lstAcc 被声明为数据类型为帐户列表。

**SOQL 查询**：这将用于从 Salesforce 数据库获取数据。下面屏幕截图中显示的查询是从 Account 对象获取数据。

**循环声明**：此循环语句用于迭代一个列表或迭代一段代码指定的次数。在下面的屏幕截图中显示的代码中，迭代将与 lstAcc 中的记录数相同。

**流控制语句**：If 语句用于此代码中的流控制。基于特定条件，决定是执行还是停止执行特定代码段。例如，在下面显示的代码中，它检查列表是否为空或者它包含记录。

**DML 语句**：对数据库中的记录执行记录插入，更新，上升，删除操作。例如，以下代码正在使用新字段值更新帐户。

以下是 Apex 代码段的外观示例。我们将在本教程中进一步研究所有这些 Apex 编程概念。![apex_sample_code_syntax](https://raw.githubusercontent.com/goatup/blog-images/main/salesforce%20apex/20210711192246.jpg)

## 第2章 数据类型

变量命名规则：

- 小写字母开头，开头不能使用下划线 '_'
- 驼峰命名法，比如 Integer stuNumber

### 2.1 原始数据类型

Apex 和 SOAP API 使用相同的原始数据类型，如下：

[Apex Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/langCon_apex_primitives.htm)

```markdown
| Primitive |   Categories    | Description                                          |
| :-------: | :-------------: | ---------------------------------------------------- |
|  Integer  |     32-bit      | Integer i = 1;                                       |
|    ID     | 16/18-character | ID id = '00300000003T2PGAA0';                        |
|   Long    |     64-bit      | Long l = 12345678L;                                  |
|  Double   |     64-bit      | Double d = 3.14159;                                  |
|  Decimal  |     number      | ?                                                    |
|  String   |     string      | String s = 'lazy dog'                                |
|  Boolean  | true/false/null | Boolean b = True;                                    |
|   Blob    |      blob       | Blob b = Blob.valueOf('Data');                       |
|  Object   |    any data     | ?                                                    |
|   Time    |      time       | Time t = Time.newInstance(1,2,3,0);                  |
|   Date    |       day       | Date d = Date.newInstance(1960,2,17);                |
| Datetime  |    datetime     | Datetime dt = Datetime.newInstance(1960,2,17,1,2,3); |
# 标准对象使用的是格林威治时间，自定义对象需调整
# Datetime = Datetime.now().addHours(9);
```

### 2.2 集合类型


