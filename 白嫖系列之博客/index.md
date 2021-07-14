# 白嫖系列之博客


fork

<!--more-->

## 前言

云端，省事，不花钱，新鲜感过后低维护成本。

### Ⅰ 整体架构

GitHub Pages + Hugo + GitHub Actions + Domain

### Ⅱ 工作流程

整个方案流程大致如下：

1. 用 MarkDown 格式写作
2. 推送文章源码至 Github 仓库
3. 触发 Github Actions 并生成 HTML 静态文件发布到 Pages 进行托管
4. （可选）绑定自定义域名

博客编辑器推荐 Typora，域名注册和解析推荐 NameSoli，文章推送最好写个 deploy.bat。


## GitHub 创建仓库

推荐两种方式创建仓库（以我的 goatup 账号为例）：

1. 直接把 `goatup.github.io` 作为远程仓库发布；

2. 将源码、git pages、照片和其他资源分为多个仓库，例如：

   源码： `goatup.github.io.source` 	//权限设为 private

   页面： `goatup.github.io` 				//权限设为 public

   照片：  blog-images						  //图床

### Ⅰ 创建 Github Pages

创建 `goatup.github.io` 仓库，仓库名必须为 [username].github.io，必须使用 main 分支，默认权限 Public：
![goatup_github_io](https://raw.githubusercontent.com/goatup/blog-images/main/blog%20build/20210630121632.png)

### Ⅱ 创建源码仓库

仓库名随意，分支随意，权限随意：
![goatup_github_io_source](https://raw.githubusercontent.com/goatup/blog-images/main/blog%20build/20210630121324.png)

### Ⅲ 为两个仓库绑定 SSH Key

当我们通过 Git 提交源码到 `goatup.github.io.source` ，Github Actions 会编译成静态文件并通过 Git Pull 到 `goatup.github.io` ，因此这一步需要 Git 账号认证。

```shell
# 打开 cmd, Powershell, git shell 任意一个，输入
ssh-keygen -t rsa -C "your email address"
```

![ssh_keygen](https://raw.githubusercontent.com/goatup/blog-images/main/blog%20build/20210630122127.png)

这两步比较重要，我们要将生成的 **Public Key** 添加到 `goatup.github.io` 仓库，勾选可写权限：![Public_Key](https://raw.githubusercontent.com/goatup/blog-images/main/blog%20build/20210630123013.png)

然后将 **Private Key** 添加到 `goatup.github.io.source` 仓库，这里 **Secrets** 变量名记住哈, 后面会用到。![Private_Key](https://raw.githubusercontent.com/goatup/blog-images/main/blog%20build/20210630124231.png)

### Ⅳ 为 Hugo 初始化做准备

将 `goatup.github.io.source` 仓库克隆到本地，开始初始化 Hugo 系统。

```shell
# 选取一个目标
cd O:\Documents\

# 克隆 source 仓库
git clone git@github.com:username/goatup.github.io.source.git
# 如果报错，则使用下面这条命令
git clone https://username:password@github.com/username/repo_name.git

# 进入仓库
cd goatup.github.io.source
```


## Hugo初始化

使用 Hugo 生成静态博客站点非常简单，具体的步骤和用法可以参考官方文档的 [Quick Start](https://www.gohugo.org/)。

### Ⅰ 两种方式安装Hugo

1. choco install hugo -y	//用户需安装 Chocolatey
2. 在 [这个页面](https://github.com/gohugoio/hugo/releases) 选择适合的版本下载，然后设置 PATH 即可。

### Ⅱ 初始化

创建一个新的站点。

```shell
# 在当前目录生成 Hugo 源码
hugo new site . --force	//在非空目录中初始化
```

​	这会生成一个特定目录结构的项目文件夹，用来维护所有的站点内容，后续的操作和命令都会在这个根目录下执行：

```shell
.
├── archetypes # 内容类型，在创建新内容时自动生成内容的配置
├── content # 网站内容，Markdown 文件
├── data
├── layouts # 网站模版，选择主题后会将主题中的 layouts 文件夹中的内容复制到此文件夹中
├── static # 包含 CSS、JavaScript、Fonts、media 等，决定网站的外观。选择主题后会将主题中的 ststic 文件夹中的内容复制到此文件夹中
├── themes # 存放主题文件
└── config.toml # 网站的配置文件
```

### Ⅲ 安装主题

- 你可以不执行这一命令使用默认主题。

安装主题有三种方式：

1. 直接下载主题压缩文件，解压到 theme/ 目录下。
2. 通过 git submodule(推荐) 或 git clone 安装：
3. 通过 Hugo Modules 安装，需本机安装 GO 1.12 及以上版本，略。	

```shell
git submodule add https://github.com/dillonzq/LoveIt.git themes/LoveIt
```

- 安装后需要启用主题，方法是将主题名称写入到根目录下的默认配置文件 config.toml：

```shell
echo 'theme = "LoveIt"' >> config.toml
  或
cp themes/LoveIt/exampleSite/config.toml .	#这里需要修改主题路径 themeDir 配置，将其注释掉
```


### Ⅳ 启动 Hugo 预览服务器

Hugo 可以启动一个 Web 服务器，同时构建站点内容到内存中并检测到文件更改后重新渲染，方便我们在开发环境实时预览对站点所做的更改。

```shell
hugo server -D
```

添加 -D 选项以输出草稿状态的文章，执行后可通过 http://localhost:1313/ 访问站点


## 通过 GitHub Pages 发布

此段为科普，帮助理解，可跳过。

这一步 Hugo 的官方文档在 [Host on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/) 中进行了详细的介绍，并且还很贴心的提供了自动化操作的 Shell 脚本。有两种方式：

1. **通过个人主页发布**：必须创建一个 `<USERNAME>.github.io` 仓库来托管生成的静态内容，发布后的域名为 `https://<USERNAME>.github.io`。
2. **通过项目主页发布**：可以随意创建 `<PROJECT_NAME>` 仓库，发布后的域名为 `https://<USERNAME>.github.io/<PROJECT_NAME>`。

建议非特殊情况下使用第 1 种方式，原因是许多主题都不能很好的支持第 2 种，具体来说是将 `config.toml` 的 `baseURL` 设置为含子路径的地址时，不能正确的处理所有资源的构建位置。


## 通过 GitHub Actions 自动部署

目前我们的「创作-发布」流程如下：

1. 在项目仓库编辑原始内容并进行版本管理。
2. 执行自动脚本生成静态站点并推送到个人主页仓库完成发布。

这套流程已经很流畅，但还有一些改进空间：我们可以使用 [GitHub Actions](https://github.com/features/actions)，在每次向远程的项目仓库推送原始内容更改时自动执行第 2 步进行发布。

GitHub 上有许多这类自动化部署任务的开源 Actions 项目，我们选择了其中一个简单易用的 [GitHub Actions for Hugo](https://github.com/peaceiris/actions-hugo#getting-started)。具体的操作步骤截图和详细配置项可以查看该项目的 [README](https://github.com/peaceiris/actions-hugo#github-actions-for-hugo)。下面简单介绍下配置过程：

![GitHub_Actions_for_Hugo](https://raw.githubusercontent.com/goatup/blog-images/main/blog%20build/20210702190134.png)

点击上面 Actions > New workflow 按钮，直接将以下文件贴进去，修改仓库名和域名即可。

```yaml
name: Deploy Hugo Site to Github Pages on Main Branch

on:
  push:
    branches:
      - main  # Set a branch to deploy

jobs:
  build-deploy:
    runs-on: ubuntu-latest  # 镜像
    steps:
      - name: checkout      # 步骤声明，可省略
        uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          deploy_key: ${{ secrets.ACTIONS_DEPLOY_KEY }} # 这里的 ACTIONS_DEPLOY_KEY 则是上面设置 Private Key的变量名
          external_repository: goatup/goatup.github.io  # Pages 远程仓库 
          CNAME: zhongyang.online	# custom domain，换成自己的域名
          keep_files: false     # remove existing files
          publish_dir: ./public # 发布文件夹
          publish_branch: main  # deploying branch
          commit_message: ${{ github.event.head_commit.message }}
```

## 测试阶段	

​	如果你觉得满意没问题之后，可以试着推送文章到 Github 找找 bug：

```shell
git add .git commit -m "first commit"git push -u origin mian	# 2021年之前的文章大部分使用 master，不冲突
```

​	因为 Github Actions 执行需要一分钟，看到 `goatup.github.io.source` 的灯变绿，就 OK 了。自此，搭建就结束了。我们可以访问 Github 为 `goatup.github.io` 仓库生成的域名： https://goatup.github.io 查看效果


附带一份 deploy.bat

```shell
@echo off
set pan=.\public\
set repo=https://github.com/goatup/goatup.github.io.source.git
set branch=main
if exist %pan% (
    echo "clean public directory"
    rd /S /Q %pan%
    echo "Hugo again for new site"
    hugo
) else (
    echo "can not find public directory"
    echo "Hugo again for new site"
    hugo
)
if exist %pan% (
    ::cd %pan%
    echo "git commit and push"
    ::git init
    git add .
    git commit -m "update site at %time%"
    echo "set remote repository and push forcely"
    ::git remote add origin %repo%
    git push -f origin main:main -v
) else (
    echo "can not find public directory, hugo fail!"
)
pause
```

## 个人体验

​	由于沉迷于挑选主题不能自拔，断断续续的花了一天才把博客上线。咱说实话，hugo 是真没 hexo 的主题多（不能说丑，也就是不好看），最终选的这个还是个烂尾的家伙。不过啊，这速度，快是真快，go 也是真香。估计也就是把自动推送和域名部署完成后，热情就凉凉了。岁月静好！上班摸鱼！两个字，真TM舒服。



## 参考

​	[GitHub博客绑定自定义域名](https://ftzzloo.com/github-pages-and-domain-name-setting/)
