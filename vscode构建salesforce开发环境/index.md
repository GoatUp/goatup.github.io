# VSCode构建Salesforce开发环境


<!--more-->

## 第1章 构筑 Salesforce 开发环境

### 1.1 VSCode 安装

点击 [VSCode](https://code.visualstudio.com/download) 下载

### 1.2 Salesforce CLI

点击 [Salesforce CLI](https://developer.salesforce.com/tools/sfdxcli) 下载

### 1.3 Salesforce Extensions for VSCode

![Salesforce_Extensions_for_VSCode](https://raw.githubusercontent.com/goatup/blog-images/main/salesforce%20dev/20210712103821.png)

### 1.4 安装语言包

非必需项

### 1.5 JDK 安装

创建运行 Apex 项目时，需要 JVM 环境。

点击 [JDK](https://developer.salesforce.com/tools/vscode/en/getting-started/java-setup) 下载后，在 VSCode 键入 `>Open Setting`，将对应的环境配置加到最后。

## 第2章 连接 Salesforce 环境

以下操作均在 VSCode 中执行！

### 2.1 Create Project with Manifest

下载、安装、配置完 VSCode 后，

键入 `>sfdx Create Project with Manifest` （可简写）；

选择 `Standard ` Standard project template (default) 环境；

键入项目名称后选择项目文件夹。

### 2.2 Authorize an Org

键入 `>Authorize an Org` ；

选择 `Project Default` 或 `Production` 均可；

回车并登录。

### 2.3 差分工具

终端键入 `>sfdx plugins:install @salesforce/sfdx-diff`

## 扩展

VSCode 左下角可选择组织环境

