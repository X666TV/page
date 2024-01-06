---
title : '软件分享|手机上使用linux'
slug : mobile-linux
date : 2022-04-09T03:57:00+08:00
draft : false
tags : ['教程','备忘']
toc : false
---

安卓系统是基于[linux][1]设计的，那么为什么不能在手机上使用linux终端呢？下面三个软件，可以让你可以在手机上体验linux。如何你有个闲置安卓手机或平板，不要急着拿去换脸盆挂闲鱼，用下面的软件装个终端，用来跑代码，搭服务器，装发行版，甚至接鼠标键盘作电脑用，这不比另外买个树莓派香

## Termux

+ 简洁，快速，稳定
+ 推荐

[Termux][2]是一个基于安卓linux内核的模拟终端，安装之后与无需获取root就可以直接工作，Termux自带pkg和apt包管理器，可以轻松安装各种包和应用。termux在国内还是比较出名的，已经有了很多国内源，例如[清华源][3]，中文资料也不少，我强力推荐[国光termux教程][4]。termux兼容大部分安卓手机，有的手机termux可能会出现文字显示分辨率不正常的问题，可通过安装插件termux:styling解决。另外，termux还可以安装linux发行版，可以参考这篇文章[知乎][5]。

## Aidlux

+ 重量级，功能强大
+ 一键部署开发环境
+ 对老旧手机不太友好

[Aidlux][7]原名Aid learning，后者原为一个开源项目，Aidlux是其商业化版本。Aidlux是个重量级AI移动端开发平台，除了linux环境，Aidlux还附带了python开发环境和一系列开发工具，自带图形界面，安装简单，功能极其强大。

可以将Aidlux理解为一个预装了图形界面和一些软件的termux，其一部分技术也确实是基于termux。

Aidlux很占空间且只有较新的安卓手机才能安装。

![桌面][8]
![终端][9]

## Linux Deploy

+ 适合老旧手机
+ 需要root
+ 安装配置稍复杂

正如其名，Linux Deploy专注于在手机上部署linux发行版，linux支持比较旧的安卓版本，我的一个安卓4.x的手机就是装的这个。Linux Deploy的安装有点麻烦，需要先root，在此基础上安装busybox，Linux deploy需要有busybox才能运行。linux deploy本身并不提供终端交互界面，安装启动后需要通过ssh访问，所以如果想在手机上终端交互的话，还得下个ssh客户端，这里我推荐[JuiceSSH][10]。还可选择安装图形界面，通过VNC访问。Linux deploy通过适当的配置，可以与手机系统和硬件实现较高程度的耦合，充分发挥旧手机性能。另外，好像自2020年后github上的linux deploy项目就没有再更新了。

  [1]: https://baike.baidu.com/item/Linux/27050?fr=kg_general
  [2]: https://termux.com/
  [3]: https://mirror.tuna.tsinghua.edu.cn/help/termux/
  [4]: https://www.sqlsec.com/2018/05/termux.html
  [5]: https://zhuanlan.zhihu.com/p/95865982

  [7]: https://www.aidlux.com/
  [8]: https://ywnz.com/uploads/allimg/20/1-20112Q6264U06.JPG
  [9]: https://ywnz.com/uploads/allimg/20/1-20112Q62AQ34.JPG
  [10]: https://www.juicessh.com/
