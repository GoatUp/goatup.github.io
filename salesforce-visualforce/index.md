# Salesforce Visualforce


Visualforce is a framework that allows developers to build sophisticated, custom user interfaces that can be hosted natively on the Lightning platform. 

<!--more-->

## Part 1 What is Visualforce？

Visualforce 框架包括一种类似于 HTML 的基于标签的标记语言，以及一组服务器端“标准控制器”，它们使基本的数据库操作（例如查询和保存）非常容易执行。

### 1.1 Visualforce  Components and Tags

![visualforce_components](https://raw.githubusercontent.com/goatup/blog-images/main/salesforce%20visualforce/20210716180341.png)

### 1.2 What is Visualforce Page？

开发人猿可以使用 Visualforce 创建 Visualforce 页面定义。页面定义由两个主要元素组成：

- Visualforce markup
- A Visualforce controller

### Visualforce markup

Visualforce markup 包括 Visualforce tags，HTML，JavaScript 和其他任意能嵌入到 <apex:page>

的标签。标记定义了页面的组件，以及显示的方式。

### Visualforce Controllers

A Visualforce controller 是一组指令，用于控制用户与组件之间的交互动作。开发人猿可以使用 Lighting 平台提供的标准控制器，也可以使用 Apex 编写的类添加自定义控制器逻辑。

### 1.3 Where Can Visualforce Pages Be Used?

开发人猿可以使用 Visualforce Page 来：

- 覆盖标准按钮，例如客户的**新建**按钮或联系人的**编辑**按钮
- 覆盖选项卡概览页面，例如“帐户”选项卡主页
- 定义自定义选项卡
- 在详细信息页面布局中嵌入组件
- 创建仪表板组件或自定义帮助页面
- 在 Salesforce 控制台中自定义、扩展或集成侧边栏（自定义控制台组件）
- 在 Salesforce 移动应用程序中添加导航菜单项和操作

## FAQ

- Q：page 修改后没反应？

  A：检查 `page controller` 指向的页面是否正确，也可在 `Apex クラス` 中查询。

- Q：添加查询功能时，多条件会报错？

  A：仔细检查是否多或少一个 `+` 号。

