# Salesforce Apex


Apex 是 Salesforce.com 开发的专有语言。类似于 Java 语法，也是一种强类型，面向对象的编程语言。允许开发人猿在 Salesforce 平台服务器上执行流和事务控制语句，并结合对 API 调用。

<!--more-->

------

## Part 1 Apex の使用開始

了解 Apex 开发生命周期。按照分步教程创建 Apex 类和触发器，并将它们部署到生产环境。

### 1.1 Apex の基本概念

Apex 代码通常包含许多我们可能从其他编程语言熟悉的东西。

**变量声明**：作为强类型语言，必须使用 Apex 中的数据类型声明每个变量。如下面的代码（下面的截图）所示，lstAcc 被声明为数据类型为帐户列表。

**SOQL 查询**：这将用于从 Salesforce 数据库获取数据。下面屏幕截图中显示的查询是从 Account 对象获取数据。

**循环声明**：此循环语句用于迭代一个列表或迭代一段代码指定的次数。在下面的屏幕截图中显示的代码中，迭代将与 lstAcc 中的记录数相同。

**流控制语句**：If 语句用于此代码中的流控制。基于特定条件，决定是执行还是停止执行特定代码段。例如，在下面显示的代码中，它检查列表是否为空或者它包含记录。

**DML 语句**：对数据库中的记录执行记录插入，更新，上升，删除操作。例如，以下代码正在使用新字段值更新帐户。

以下是 Apex 代码段的外观示例。我们将在本教程中进一步研究所有这些 Apex 编程概念。![apex_sample_code_syntax](https://raw.githubusercontent.com/goatup/blog-images/main/salesforce%20apex/20210711192246.jpg)

**変数の命名**：

- 小写字母开头，开头不能使用下划线 '_'
- 驼峰命名法，比如 Integer stuNumber
- 不能使用任何 Apex 保留关键字

### 1.2 Apex を使用する必要がある状況は？

- 创建 Web 服务。
- 创建电子邮件服务。
- 对多个对象执行复杂的验证。
- 创建工作流不支持的复杂业务流程。
- 创建自定义事务逻辑（发生在整个事务中的逻辑，而不仅仅是单个记录或对象）。
- 将自定义逻辑附加到另一个操作（例如保存记录），以便在执行操作时发生该操作，无论它是源自用户界面、Visualforce 页面还是来自 SOAP API。

Apex 不能用于：

- 在用户界面中呈现除错误消息以外的元素
- 更改标准功能——Apex 只能阻止功能发生，或添加附加功能
- 创建临时文件
- 生成线程

### 1.3 Apex はどのように机能しますか？

Apex 完全在 Lighting 平台上编译、存储和运行。开发人猿编写 Apex 代码并将其保存到平台，用户通过用户界面触发 Apex 代码的执行。

![apex](https://raw.githubusercontent.com/goatup/blog-images/main/salesforce%20apex/20210716194211.png)

### 1.4 Apex 开発プロセスとは?

要开发 Apex，请获取 Developer Edition 帐户，编写和测试您的代码，然后部署您的代码。

我们推荐以下流程来开发 Apex：

1. [获取开发者版帐户。](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_intro_get_dev_account.htm)
2. [了解有关 Apex 的更多信息](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_intro_learning_apex.htm)。
3. [写下你的 Apex。](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_intro_writing_apex.htm)
4. 在编写 Apex 时，您还应该[编写测试](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_intro_writing_tests.htm)。
5. 可选择[将您的 Apex 部署到沙盒组织](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_intro_deploying_to_sandbox.htm)并进行最终单元测试。
6. [将您的 Apex 部署到您的 Salesforce 生产组织。](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_intro_deploying_to_production.htm)

除了部署您的 Apex，在编写和测试之后，您还可以[将您的类和触发器添加到 AppExchange 应用程序包中](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_intro_AppExchange.htm)。

### 1.5 Apex クイックスタート

本教程将展示如何创建简单的 Apex 类和触发器，以及如何将这些组件部署到生产组织。

## Part 2 Apex の作成

## Part 3 Apex の実行

## Part 4 Apex のデバック、テスト、リリース



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


