# Windows Tips


保存一些 Windows 上的问题解决方法和小技巧，避免忘记。

<!--more-->

## 软件类

### Tomcat

Java 定期会收到 update 通知，如果更新需在 Tomcat 端及时更正 jre 环境，否则会发生错误。

```markdown
ローカルコンピュータで Apache Tomcat8.5 Tomcat8 を開始できませんでした。詳細情報はシステムイベントログを参照してください。これがMicrosoft以外のサービスである場合は、サービスの製造元に問い合わせてください。その際、サービス固有のエラー コードが 1 であることを伝えてください。
```

解决方法：

启动 `C:\Program Files\Apache Software Foundation\Tomcat 8.5\bin\Tomcat8w.exe` ，将 `java` 目录下的 `Java Virtual Machine` 环境更正为最新版。

## 服务类

操作方法：Cortana搜索框输入"Services"打开"サービス"

### SysMain

原为Superfetch超级预读服务，将多余的物理内存作为缓存使用，对软件进行预加载操作，导致内存占用增大，延长开机时间。
**对于经常不关机或者睡眠模式的，个人推荐使用**，当系统启动变慢得无法忍受时，可以清空一下：C:\Windows\Prefetch\*.pf 文件
而**对于经常开关机的，建议关闭**

### Windows Search

这是为Windows提供搜索索引的服务，可以下载安装everything替代，**建议关闭**

### Connected User Experiences and Telemetry

这是后台自动收集错误及系统崩溃信息的服务，普通用户用不着，**建议关闭**

