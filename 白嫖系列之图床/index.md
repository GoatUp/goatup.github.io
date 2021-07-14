# 白嫖系列之图床


fork

<!--more-->

## 1 前言

云端，便捷，无限容量，稳定不跑路，免费最重要。

### 1.1 整体架构

GitHub + Typora + PicGo

### 1.2 软件下载

略：太简单，自己去搜。

## 2 GitHub

创个库，当作图床，取名困难就 image。

### 2.1 获取令牌

也就是 Token，对外公钥，可访问API，步骤如下：

1. Settings
2. Developer settings
3. Personal access tokens
4. Generate new token

Select scopes时，看不懂可全选。

**生成的 Token 只显示一次。**

## 3 PicGo

安装后界面如下：![picgo_intall_interface](https://raw.githubusercontent.com/goatup/blog-images/main/image%20hosting/20210629181144.png)

对应设置即可；![picgo_setting_interface](https://raw.githubusercontent.com/goatup/blog-images/main/image%20hosting/20210629181208.png)

## 4 Typora

自定义安装后，按图配置：![typora_setting_interface](https://raw.githubusercontent.com/goatup/blog-images/main/image%20hosting/20210629181455.png)

### 4.1 上传失败解决办法

1. 换个IP，WIFI或4G
2. Failed to fetch 时，修改 Server Port 为36677


