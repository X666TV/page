---
title : '用ksweb快速搭建博客'
slug : build-a-blog
date : 2022-04-04T02:37:00+08:00
draft : false
tags : ['教程','备忘']
toc : ture
scrolltotop : ture
hasCJKLanguage : true
---

{{< admonition type=note title="Note" >}}
早期整活，修复了图片再次发布
{{< /admonition >}}

_想要零基础建个网站？_
_想要让旧手机发挥余热？_
_想建个个人博客但不知道怎么做？_
_那么看这篇文章就对了_

## 简介
ksweb是一个安卓app，也是一个集成php服务器环境。用ksweb你可以在手机上轻松搭建Apache/nginx/litghttpd+php+mysql环境，使用该环境配合博客框架你可以轻松搭建一个属于自己的博客。这个教程将带你一步一步完成博客的搭建，如果中途出现了问题可以参考教程的最后，由于我也是个小白，没法讲清楚所有东西，所以如果有不明白的还可以百度自行寻找解决办法。

## 下载一个可以用的ksweb

我们只需要用到一个软件ksweb,百度可以很容易找到汉化版，尽量找较新的版本安装，以避免不必要的麻烦。
打开后的界面是这样的
{{< figure src="/images/build-a-blog/ksweb.png" alt="image" caption="ksweb主界面" class="right" >}}

**状态**栏可以总览服务器状态，后面还有[__LIGHTTPD__][2], [__NGINX__][3], [__APACHE__][4], 这三个都是web服务器，功能类似，我们只要选其中一个打开就行('开启服务')；[__MYSQL__][5]是数据库服务器，保持打开状态，[__PHP__][6] 本是一门编程语言，这里是一个解析php程序的服务器，保持打开状态。大概的工作流程是，web服务器与访问网站的用户终端直接交互，拿到用户的请求并转交给PHP服务器处理，PHP根据需要从Mysql存取数据，并把处理后的数据交给web服务器发回给用户。
后面还有FTP(传文件用的)，计划任务，这两个一般用不上，保持关闭，不用管它。

## 配置&更新(可选)

一般情况下，ksweb装完后就可以直接用了，
保持一个web服务器为打开状态，比如说之前那张图我的lighttpd是打开状态，下面有一个"主机0"( 如果没有可以去相应的服务器栏下点加号创建)，点那个http://localhost:xxxx链接会自动打开浏览器跳转服务器测试界面，如果能加载出东西一般就没问题。
但是我们在正式使用前还想配置一下。如果你打算像我一样让ksweb一直运行，请打开设置，把 保护服务器被非授权终止，锁定Wi-Fi,Turn off bettary saving 三个选项勾上(最后一个可能勾不上，那就算了)；其他选项除非你知道是用来干什么的，否则不要动它。
点击phpmyadmin，第一次打开他可能会自动安装，如果下载很慢也可以手动安装，详见文章最后，一般情况下点击会显示这个
{{< figure src="/images/build-a-blog/chose-server.png" alt="image" caption="ksweb主界面" class="left" >}}

选择你已经打开的服务器，点确认，然后你会发现状态栏里相应的服务器下多了一个主机，打开它，会进入数据库管理界面

{{< figure src="/images/build-a-blog/php-my-admin.jpg" alt="image" caption="phpMyAdmin主界面" class="right" >}}

__phpmyadmin初始账户是root，密码为空__
登录进去后记得改密码

{{< figure src="/images/build-a-blog/ch-pswd.jpg" alt="image" caption="修改密码" class="normal" >}}

进入PHP栏，选择PHP版本，最好选7.4.0及之后的版本，有时你会发现没得选，可以按照他的提示安装拓展，安装完后，就会发现多了许多PHP版本可选。还有时候会提示有新版本可升级，可以根据需要升级。

## 下载安装WordPress/Typecho
[WordPress][9]和[Typecho][10]都是用PHP编写的博客平台，前者插件众多、功能强大；后者轻量快速，原生支持[Markdown][11]。两个平台的配置安装过程大致相同，这里我就介绍Typecho，WordPress可类比。
1. 下载解压Typecho:去Typecho官网http://typecho.org/ 下载Typecho，得到的是一个zip压缩包，将其解压，把解压得到的文件夹里的东西移动至手机的/htdocs目录下
2. 创建数据库:进入phpmyadmin数据库界面，创建一个数据库，记住数据库名，之后要用。
{{< figure src="/images/build-a-blog/create-db.jpg" alt="image" caption="创建数据库" class="right" >}}
3. 安装:浏览器访问http://localhost:8080/install ，就是之前那个测试页面的链接后面加了个"/install"，(其实有时候不加也没问题)，进入安装界面，要注意以下三点，其他地方如果不清楚就保持默认，然后“确认，开始安装”
{{< figure src="/images/build-a-blog/install.png" alt="image" caption="" class="left" >}}
4. 安装好了就会进入博客后台管理界面，然后你就可以开始写博客了，现在你可以在局域网内访问你的博客，地址为http://IP地址:端口 ，就是把localhost换成手机的IP地址，ip地址显示在ksweb状态栏，例如按下图就用http://10.241.120.170:8080访问博客网站，用http://10.241.120.170:8080/admin进入后台。
{{< figure src="https://s3.bmp.ovh/imgs/2022/04/06/d4487aebdd31d228.png" alt="image" caption="ip">}}
5. 恭喜你成功建立了一个属于自己的博客，博客平台的使用就得靠你自己探索了，typecho支持安装插件和切换主题，推荐一个网站https://typecho.me/ 里面有许多免费的主题和插件，下载下来解压后，主题放在/htdocs/usr/themes文件夹下，插件放在/htdocs/usr/plugins文件夹下，然后就可以在后台[控制台]看到了。

## 一些可能遇到的问题
### 关于文件路径的问题
按我讲的操作，/htdocs文件夹下应该有一个index.php，像这样
![htdocs文件夹][15]
但有的朋友直接把解压后的文件夹挪到htdocs文件夹里，那么index.php应该会在/htdocs/typecho下，像这样
![typecho文件夹][16]
如果是这样，那么你在安装和访问博客时的链接应该加上"/typecho"，例如http://localhost:8080/typecho/install
按此规律类推
### 手动安装/升级phpmyadmin
下载phpmyadmin最新安装包，解压至/ksweb/tools目录下，文件夹命名为phpMyAdmin，替换掉原有的phpMyAdmin文件夹(两个文件夹内容应该差别不大，可以稍微注意一下)，正常情况下至此就完成升级了，可以打开phpmyadmin看看有没有问题，如果有问题可以尝试删除原有主机，重启ksweb，检查文件夹内容等方法，还有可能你下的不是安装包而是源码，那么可以试试在链接后加个/setup，例如http://localhost:8001/setup  也可以试试点ksweb的PHP栏下的composer START。


[2]: https://baike.baidu.com/item/lighttpd/6735570
[3]: https://baike.baidu.com/item/nginx/3817705
[4]: https://baike.baidu.com/item/Apache/6265
[5]: https://baike.baidu.com/item/mySQL/471251
[6]: https://baike.baidu.com/item/PHP/9337

[9]: https://wordpress.com/zh-cn/
[10]: http://typecho.org/
[11]: https://baike.baidu.com/item/markdown/3245829

[15]: https://s3.bmp.ovh/imgs/2022/04/06/1a25b6c993a833c2.png
[16]: https://s3.bmp.ovh/imgs/2022/04/06/0c5434fd277d25d0.png
