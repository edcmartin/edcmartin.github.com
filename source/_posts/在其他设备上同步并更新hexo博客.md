title: 在其他设备上同步并更新hexo博客
date: 2016-01-11 13:13:02
tags: 
- hexo
---
我们利用Hexo在Github上创建了属于我们自己的主页，并可以在一台设备上更新博客内容。
若想在其他设备上更新博客怎么实现：
* 如何在两台设备间同步博客的内容
* 在另一台设备如何更新博客

<!--more-->
## 同步博客
设备A更新博客内容后，并发布到Github自己的主页中，将本地仓库中的文件都push到Github的项目中(分支blog存放git仓库文件，master分支发布博客网页)。

1. 设备B首先从自己的Github中获取资源
```
git status
git pull origin blog
```
2. 在设备B中添加新的博客
```
hexo new "博客"
```
3. 将本地文件push到blog分支
```
git status
git add .
git commit -m "add"
git push origin blog
```
## 更新博客
* 将网页发布到主页中(master分支)
```
hexo generate -d
```