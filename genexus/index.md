# GeneXus


一个来自乌拉圭公司开发的低代码开发平台。

<!--more-->

## 劝退指南

根据产品介绍的说法大致是：传统的开发过程是定义好产品后就开始分小组进行代码开发，有 H5 小组负责网页的开发，有安卓组和 IOS 组负责移动端 app 的开发，于是乎这样就特别麻烦，所以 Genexus 就提供了这么一个低代码的开发平台，基础框架帮你搭好，让你在其上开发代码会更便捷更方便，包括移动端开发都会有自己的工具帮助开发。

![genexus](https://raw.githubusercontent.com/goatup/blog-images/main/genexus/20210730174748.png)

启动好了之后的界面长这样：![genexus_login](https://raw.githubusercontent.com/goatup/blog-images/main/genexus/20210730175016.png)

License 是收费的，贼鸡儿贵，一年大概2w多刀，但 License 是兼容向下版本的，只是一旦过期连界面都打不开。

对于 Genexus 来说知识库就是他的项目，Genexus 一般推荐与 SQL Server 搭配，当然其他数据库也可以。然后就是选择环境，可以选择 C# 也可以选择 .net，这个选择和你所要写的语言没有很大关系，因为自始至终 Genexus 都有一套自己的语言，你必须遵照它的结构和语法去编写；这里就引出了一个极为头疼的问题，Genexus 的中文资料实在是少之又少，甚至连中文API文档都没有，英文wiki社区什么的也是内容稀少，想从官方API文档中寻找更是困难重重（感觉组织得并不很好），这对于一个新接触这个软件的人来说确实十分焦急和恼火，还有更多千奇百怪的bug是无从下手的，这个时候就只有靠 Genexus 销售方提供的技术支持群内的技术人员帮助解答或者远程协助，但是这样确实是很麻烦。

Genexus 中的界面模板由插件 workWithPlus 提供，里面提供了一些内置的前端展示模板，但是很多设置还是很繁琐而且不够灵活，主要的问题是如果想要完全自己画一个界面出来就会非常麻烦，它采用“所见即所得”的方式来绘制界面，但是操作起来真的无比麻烦，各种属性的设置和启用能让你怀疑人生。后来我想着我先运行出来，在浏览器中直接写CSS然后返回去改总行了吧，但是对不起，Genexus 中的 CSS 设置好像和浏览器中的 CSS 设置不一样，上述方法完全行不通，这就十分崩溃了，一个简单的界面用 Genexus 根本难以绘出跟别说还有动态加载的问题了。

Genexus 中进行移动端app开发需要用到另一个插件貌似叫 smartDevice，然后你就会继续孤独的和 bug 作斗争。

总而言之这个所谓的“低代码平台”的本意就是想把一些繁琐重复性的框架帮你抽离出来，让我们可以投入更多的精力去书写有关逻辑的代码，但是这点本身就有利有弊，Genexus 的封装程度过高，导致很多地方操作十分不灵活，很难让我们发挥我们自己的想法，只能照着它的模板一步一步走，甚至都不敢随意乱动，不然出了莫名其妙的bug都不知道怎么解决。由于封装程度过高，所以使得它不适合与初学者，初学者连一些编程或者网络的基础知识都没掌握，虽然看起来从Genexus 入手好像更简单一点，学起来快一点，但是他们会在很多地方卡壳，因为他们不明白为什么需要这样做，一条链路的一个小环节没有搞清楚那之后的就会更加稀里糊涂。所以个人觉得小白同学还是先好好学一些基础知识再来学习，而且感觉 Genexus 更适合自由职业者或个人全栈开发工程师。

Genexus 在中国的市场其实也并不是很大，所以中文资料少之又少，这种情况下英文原生文档和社区又不强劲的情况下孤勇使用 Genexus 的学习曲线想必是很艰难的。况且 Genexus 内部使用自己的语言，这就意味着使用它就必须再掌握一门编程语言，相信这是很多程序员都比较讨厌的事情，况且国内不论是大厂还是小公司，使用 Genexus 的都很少，跟别说它自己的内部语言了，所以这个学习成本和回报是需要自己去掂量一下的。

------

## 环境配置

JDK：Java 开发用

[Tomcat](https://tomcat.apache.org/download-80.cgi)：Java 开发用

[SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)：安装genexus 必须环境

SQL Server Management Studio (SSMS)：可选

[GeneXus](https://www.genexus.jp/community-and-support-jp/downloads02)

WorkWithPlus：与GeneXus 对应版本

[PostgreSQL](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)

Tip：PostgreSQL13 和GeneXus15U10 不匹配，降为PostgreSQL12 即可

-----

## 项目迁移

1、Model：C盘根目录，全拷贝即可，并修改knowledgebase.connection 地址属性

2、SQL Server Management Studio (SSMS)：将项目文件附加到数据库![ssms](https://raw.githubusercontent.com/goatup/blog-images/main/genexus/20210730181717.png)命令行界面，执行genexus /install

3、UserControls：在**/GeneXus15/UserControls，全拷贝即可

4、pgAdmin4：Postgresql的图形化管理工具，用以备份和恢复![pgadmin](https://raw.githubusercontent.com/goatup/blog-images/main/genexus/20210730181746.png)Tip：如果报错pg_restore.exe file not found，修改File→Preferences→Path→Binary Path为C:\Program Files\PostgreSQL\12\bin

5、可直接拷贝Tomcat/webapps 目录中项目文件以减少编译时间

------

## 日常报错

首先确认【本地服务】有木有启动，按WIN + r 后键入services.msc 可见

Tip：Apache Tomcat 8.5、postgresql-x64-12、SQL Server (SQLEXPRESS)

