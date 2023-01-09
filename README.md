## 安装环境

- 前端运行需要运行在 node 环境，请先安装[Node](https://nodejs.org/en/download/)
- 由于需要部署到 Github 上，请先安装[Git](https://git-scm.com/)

## 安装主题

#### 安装 Hexo

官网：https://hexo.io/zh-cn/

```shell
 # 全局安装hexo
 npm install hexo-cli -g
 # hexo初始化
 hexo init hexo-webstack-navication
  cd hexo-webstack-navication
```

#### 启动 Hexo

```shell
hexo server
# 创建文章
hexo new hexo
```

#### 安装主题

本主题根据 webstack 进行小幅度的修改，请看[源码](https://github.com/WebStackPage/WebStackPage.github.io)

克隆主题并把主题文件放入到`themes`下，并把目录文件修改为`butterfly`

原皮预览：http://webstack.cc/cn/index.html

```shell
# 安装hexo
hexo init hexo-webstack-navication
npm install hexo-theme-webstack -S
```

修改配置文件：主配置文件\_config.yml

```
theme: webstack
```

> 如果不想配置请克隆我的修改过后的主题文件,并换成个人基本信息和网络地址

```shell
# 克隆我的地址
git clone git@github.com:sundayskys/hexo-webstack-navigation.git
# 安装
npm install
# 启动
hexo server
```

导航浏览：http://nav88.cc

## 项目部署

#### 流水线部署

添加.github/workflows/audodeploy.yml

```yml
name: 自动部署
on:
  push:
    branches:
      - master # 只在master上push触发部署。
    paths-ignore: # 下列文件的变更不触发部署，可以自行添加
      - README.md
      - LICENSE

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: 检查分支
        uses: actions/checkout@v2
        with:
          ref: master

      - name: 安装Node
        uses: actions/setup-node@v1
        with:
          node-version: "16.x"

      - name: 安装 Hexo
        run: |
          export TZ='Asia/Shanghai'
          npm install hexo-cli -g
      - name: 安装依赖
        if: steps.cache-modules.outputs.cache-hit != 'true'
        run: |
          yarn install --save
      - name: 生成静态文件
        run: |
          hexo clean
          hexo generate

      - name: 部署到Github
        uses: JamesIves/github-pages-deploy-action@v4
        with:
          token: ${{secrets.ACCESS_TOKEN}}
          repository-name: sundayskys/hexo-navigation
          branch: main
          folder: public
          commit-message: "${{ github.event.head_commit.message }} Updated By  Actions"
```

> 请修改个人的仓库信息和token，注意修改仓库不是主题的仓库，而是部署页面的仓库。

hexo-navigation是编译后的文件也就是展示页面的仓库。而hexo-webstack-navigation是主题文件，也就是写代码的地方。

获取token**值**

进入个人设置获取token值，并复制，注意只显示一次，要提前复制

![Snipaste_2023-01-09_22-07-19](https://s2.loli.net/2023/01/09/rZOnE7bws4dm9MQ.png)

设置token永不过期

![Snipaste_2023-01-09_22-07-52](https://s2.loli.net/2023/01/09/GFMrL3vOnmUNZs8.png)

给项目添加token值，ACCESS_TOKEN 就是上面变量的值

![Snipaste_2023-01-09_22-08-53](https://s2.loli.net/2023/01/09/CFwrD6flOAy7Lnj.png)

#### 部署上线

修改个人网络地址和个人信息

```yml
# Site
title: 程序员导航
subtitle: ''
description: 'hexo 导航'
keywords:
author: 亿言
language: en
timezone: ''

# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
url: https://nav88.cc
```

添加DNS解析

![](https://s2.loli.net/2023/01/09/Rruyn21zv9NLSgG.png)
