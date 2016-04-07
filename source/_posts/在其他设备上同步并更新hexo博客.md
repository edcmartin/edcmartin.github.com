title: 在其他设备上同步并更新hexo博客
date: 2016-01-11 13:13:02
tags: 
- hexo
---
<!--生成网易云音乐flash插件-->
<embed src="http://music.163.com/style/swf/widget.swf?sid=21973899&type=2&auto=0&width=320&height=66" width="340" height="86"  allowNetworking="all"></embed>

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

<!--插入MV-->
在 , 也不见 电影<再见,在也不见>主题曲 歌词版-- 孙燕姿
<embed src="http://player.yinyuetai.com/video/player/2540886/v_0.swf" quality="high" width="480" height="334" align="middle"  allowScriptAccess="sameDomain" allowfullscreen="true" type="application/x-shockwave-flash"></embed>