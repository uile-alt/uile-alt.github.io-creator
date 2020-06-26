---
title: "HugoToGithub"
date: 2020-05-24T18:01:18+08:00
draft: false
---

## 使用hugo搭建博客，并在GitHub Pages预览HTML
我使用的编辑器是Visual Studio Code，命令行工具是Bash。
1. 从hugo的 [GitHub Releases](https://github.com/gohugoio/hugo/releases)下载相应的版本

2. 添加hugo.exe的路径到Path，这命令行工具输入hugo version验证

3. 建立一个网站，名为blog
```
hugo new site blog
```
4. 下载主题
```
cd blog
git init
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
```
然后，将主题添加到站点配置中：
```
echo 'theme = "ananke"' >> config.toml
```
5. 添加文章
添加一个测试文件test.md
```
hugo new posts/test.md
```
编辑test.md，原来的内容不要删除，编写完内容修改draft为false。
6. 启动hugo服务器
```
 hugo server -D
```
按住ctrl单击运行完的链接，例如http://localhost:xxxx/，之后你就能在浏览器查看test.md的效果。博客已完成，接下来上传到GitHub。

7. 建立静态页面
```
hugo -D
```
执行完，项目会增加一个public文件夹，这个就是要上传到GitHub仓库的。
8. 初始化public仓库
首先在blog项目下创建.gitignore文件，里面添加/public/，然后直接下面命令.
```
cd public
git init
```
9. 添加到本地仓库
```
git add.
git commit -v
```
10. 创建GitHub仓库
在GitHub创建一个新的仓库，名字必须为用户名+.github.io
11. 上传到上面的仓库
```
git remote add origin git@github.com:用户名/用户名.github.io.git
git push -u origin master
```
12. 效果
进入仓库，点击setting，找到Github Pages的链接，就能预览了。

13. 问题及解决
问题：能进入博客首页，但详细页显示有误。
解决方法：在config.tomld的baseURL = "https://example.org/"改为baseURL = "https://用户名.github.io/"，重新hugo并将public上传到GitHub，上传的时候要注意输入命令的位置，是public还是项目名。如果上传的时候提示有错误，尝试添加一个1.md作为测试提交上去。