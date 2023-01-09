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

