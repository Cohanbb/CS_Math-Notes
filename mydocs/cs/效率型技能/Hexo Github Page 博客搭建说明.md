**本文索引**

- [Hexo 博客搭建简单说明](#hexo-博客搭建简单说明)
  - [配置 Git、hexo](#配置-githexo)
  - [GitHub Page 配置](#github-page-配置)
  - [配置主题](#配置主题)
  - [发布博客](#发布博客)

<hr>

# Hexo 博客搭建简单说明

## 配置 Git、hexo

1. 安装 [node.js](https://nodejs.org/en/)。

2. 安装 [Git](https://git-scm.com/download/win)。

3. 命令行输入命令检验是否安装成功
   
```bash
$ node -v
$ npm -v
$ git --version
```
 
1. 安装 hexo  
 命令行输入 `npm install hexo-cli -g`，输入 `hexo -v` 检验是否安装成功。
 
5. 初始化 hexo  
 命令行输入 `hexo init [folder]`，[folder] 为自定义名字，作为博客的根目录。

6. 根目录的结构  

    * _config.yml : 网站的配置信息，在此配置网站的功能和结构。
    * package.json: 应用程序的信息，可以查看安装的包。
    * scaffolds: 模版文件夹，Hexo 根据此来建立文件。
    * source: 资源文件夹，如 post、tags 等文件存放在此。
    * themes: 主题 文件夹。Hexo 会根据主题来生成静态页面。

7. 生成静态文件，在根目录下命令行输入 `hexo generate`  
启动服务器，输入 `hexo server`  
可在 http://localhost:4000/ 查看网站。

## GitHub Page 配置

1. 登录 [GitHub](https://github.com)，新建 repository，名字必须设为 **username.github.io**

2. 复制仓库的地址 SSH/HTTPs，推荐使用HTTPs，操作简单，但是网路状况不佳；使用 SSH 方式首先需要在本地生成 SSH Key，在终端输入 `$ ssh-keygen -t rsa -b 4096 -C "your github email"`，然后登录 GitHub 将刚刚生成的公钥添加到 SSH Key 即可。

3. 进入根目录下的 **_config.yml** 文件，在末尾加入： 
    
 ```yaml
 deploy: 
  type: git
  repo: https://github.com/username/username.github.io.git
  branch: master
 ```

4. 部署 GitHub  
 需要下载插件，根目录命令行输入 `npm install hexo-deployer-git --save`  
 发布网站到GitHub Page  
 `hexo deploy`

5. 然后在浏览器访问 https://username.github.io 即可进入博客主页。
 
 
## 配置主题
Hexo 博客默认主题为 landscape，若想修改主题，在 GitHub 上找到主题，克隆到 theme 文件夹下。本例为 next 主题。  

**获取主题**   
 theme文件夹下命令行输入：

```bash
$ git clone https://github.com/theme-next/hexo-theme-next themes/next
```

打开 next 的 _config.yml 文件，里面是 next 主题的配置信息，阅读该文档内的注释即可大致明白各部分的作用。  
要修改的主要内容为 `tags`, `categories`, `about`, `social`, `avatar`, `search`，网站的背景等。  

**tags 和 categories**   
tags 为标签，categories 为类别。在根目录下命令行输入 `hexo new page tags` ，进入 ./source/tags/index.md，修改为：

```yaml
---
title: tags
date: xxxxx
type: "tags"
---
```

如果想要文章加上标签，只用在文章上加入 `tags: xxxx` 即可。  
categories 与以上同理。
 
**about**   
 在 next/_config.yml 文件中找到 `menu` ，可在网站中增加 about。  
 根目录命令行输入 `hexo new page about` ，进入 ./source/about/index.md 可编辑 about 的内容。
 
**修改头像，网站的图标、背景**  

 * 修改头像，next/_config.yml 文件中找到 `avatar` 可配置头像。next/source/image/ 下 avatar.gif 为头像图片，进行更改即可。更改 logo.svg 以及 favicon 图片可以修改网站的图标。
 * 修改背景，在 next/_config.yml 文件查找 `custom` 可配置 style ` style: source/_data/styles.styl`
 后新建 ./source/_data/styles.styl 加入以下代码，后在 next/source/image 中增添背景图片，命名为 background.jpg 即可。

```css
body {
    background: url(/images/background.jpg); //图片路径，默认
    background-repeat: no-repeat;	//图片无法铺满时，是否重复及重复方式
    background-attachment: fixed;	//图片是否跟随滚动
    background-size: cover;	//覆盖
    background-position: center; //图片显示 
}
```

**启用search**  
安装插件，根目录下命令行输入 `npm install hexo-generator-searchdb --save`  
根目录/_config.yml 文件中加入：

```yaml
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

next/_config.yml 文件中找到 `localsearch` 修改为：

```yaml
local_search:
  enable: true
  # if auto, trigger search by changing input
  # if manual, trigger search by pressing enter key or search button
  trigger: auto
  # show top n results per article, show all results by setting to -1
  top_n_per_article: 1
```

**插入图片**   
需要将 \_config.yml 中的 `post_asset_folder` 设为 true，这样新建一个博客文件将生成一个同名的目录（文件夹），将图片放入该文件夹，在 markdown 文件中使用 `![](图片的名称)` 即可正常显示图片了。

## 发布博客
在根目录命令行输入：

```bash
$ hexo new [pagename]
```

即可创建新的文章，进入 ./source/_post/ 可找到该文章文件夹，编辑里面的 index.md 即为文章内容。  
编辑完成后根目录命令行输入以下命令发布博客。

```bash
$ hexo clean
$ hexo g
$ hexo d
```

如果 markdown 内容中有数学公式，需要在文章上方加入 `mathjax: true`，或是在 next/_config.yml 文件中找到 `mathjax`，将 `per_page` 后改为 `true`，后者会使所有文章都自动加入 `mathjax: true`，由于数学公式与 hexo 默认的 marked 渲染器有冲突，故建议卸载 marked 渲染器，使用 pandoc 渲染器。

```bash
$ npm uninstall hexo-renderer-marked --save
$ npm install hexo-renderer-pandoc --save
```
 
