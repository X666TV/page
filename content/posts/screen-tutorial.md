---
title : 'Screen快速上手'
slug : screen-tutorial
date : 2023-03-11T12:00:00+08:00
draft : false
tags : ['教程','备忘']
toc : false
---

screen其实分两级，第一级为screen（屏），第二级为window（窗），一个screen可以包含多个windows。

要使用screen，先要执行screen创建一个屏，或使用`screen -S name`创建一个命名的屏。屏创建的同时，创建一个默认窗。
使用`Ctrl a w`查看当前屏所有窗，带*的为当前窗
使用`Ctrl a A`重命名当前窗，注意这是临时的，当该窗执行某程序时，其名字会自动变成程序名
`Ctrl a c`新建一个窗
`Ctrl a n/p/Ctrl a` 切换到下一个/上一个/最近的窗
`Ctrl a k` 强制关闭当前窗

screen可以嵌套执行，即在一个窗中再创一个屏，这个screen就可以理解为在窗中跑了一个程序，嵌套执行后的screen只能使用最后一个屏（即最里面的screen，因为他会占用Ctrl a快捷键，所以切不出去）的窗，除非你把这个屏关了，所以平时使用作用不大。建议不要嵌套执行screen，不然很容易懵，盗梦空间看过吧，就那种感觉。

`exit` 退出终端，其实就是退出当前窗，当一个屏中所有窗都退出时，该屏自动关闭
`Ctrl a d`可以分离(detach)当前窗，即把当前窗放到后台执行，回到最初的界面，注意这是最初的界面，这个时候再执行exit就断开ssh连接了，不过detach的窗还会继续执行。
`screen -ls`可以查看所有屏，包括嵌套执行的屏，可以看到屏id和状态（attached/detached），对于detached屏，可以使用`screen -r id`恢复，对于attachde屏，说明有登录的用户正在占用，有时候ssh意外断开后，再重连就会看到原来的屏为attached，这时可以用`screen -d id`强行分离，再用`screen -r id`恢复。
`Ctrl a z` 暂时回到最初的界面，用`fg`命令回去

高级玩法：
`Ctrl a S`水平分屏，`Ctrl a |`竖直分屏，
`Ctrl a Tab`分屏焦点切换，
`Ctrl a X`关闭当前分屏，类似于最小化，屏中的窗不会关闭，还可以切换过去

知道上面的操作应该就能满足大部分使用需求了，想要知道更多高级用法可以自己上网查资料。
本文参考了[这篇文章][1]

  [1]: https://www.cnblogs.com/linyu51/p/15481474.html
