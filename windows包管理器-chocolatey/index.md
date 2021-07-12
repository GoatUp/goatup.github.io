# Windows包管理器 - Chocolatey


fork

<!--more-->

以空间换时间，统一开发环境的基础【防止手贱】。

## 安装 choco

{{< admonition note "以管理员权限运行 cmd 或 powershell" >}}

cmd运行：

```shell
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

powershell运行：

```shell
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

{{< /admonition >}}

安装完成后，运行 `choco` 或 `choco -?` 检查是否安装正确。

## choco 安装软件

{{< admonition note "以管理员权限运行 cmd 或 powershell" >}}

执行过程中会提示你是否接受软件的安装协议等，输入  `-y`，可免去这一步，如下：

```shell
choco install <packagename> -y
# 或
cinst <packagename> -y
```

{{< /admonition >}}

​	安装 JDK8：

​	choco install jdk8

​	安装 git：

​	cinst git.install

​	安装chrome：

​	cinst googlechrome

​	安装7-zip：

​	cinst 7zip.install

​	更多安装包，请搜索这里：

​	[Chocolatey Gallery | Packages](https://link.zhihu.com/?target=https%3A//chocolatey.org/packages)

​	其他用法：

​	cinst jdk8 googlechrome vscode 7zip	//一次安装多个软件包

​	cinst nodejs.install --version 0.10.35	//安装指定版本

​	cinst dev-package.config	//安装config文件内描述的所有软件包

​	dev-package.config：

```xml
<?xml version="1.0" encoding="utf-8"?>
    <packages>
      <package id="jdk8" />
      <package id="googlechrome" version="71.0.3578.98" />
      <package id="vscode" />
      <package id="7zip" />
    </packages>
```

## 安装报错

- Error: Error building site: TOCSS: failed to transform "main.scss"

  解决办法：你需要安装 Hugo 扩展包

  choco install hugo-extended -y


