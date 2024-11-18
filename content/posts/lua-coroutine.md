---
title: "Lua的协程(coroutine)"
date: 2024-11-18T22:50:44+08:00
draft: false
toc: false
tags: ['Lua','笔记']
---

## 从create,resume和yield开始

协程顾名思义,多个程序相互协助运行,create,resume和yield这三个方法是lua协程最常用的方法;
主程序使用`coroutine.create()`创建协程,参数为一个函数,返回该其协程,创建后不会立马执行协程函数,需要使用`coroutine.resume()`启动协程,若协程函数还未执行,则resume方法的参数作为协程函数参数传入,协程函数执行过程中使用`coroutine.yield()`暂停执行回到主程序,yield方法传入的参数将被主程序的resume方法传出为主程序所用,若主程序再调用resume方法,则其传入参数又会被协程的yield方法传出,同时主程序阻塞而协程继续执行,如此往复实现主程序和协程的交互,直到协程函数执行完毕,最后其返回值通过主程序resume方法由主程序接收;下图示意了该过程.

![lua coroutine](../assets/lua-coroutine/lua-coroutine.svg)

lua的协程与一般多线程不太一样,一般多线程的程序可以同时运行几个线程,而协同程序却需要彼此协作的运行,在任一指定时刻只有一个协同程序在运行(如图中的实线).并且这个正在运行的协同程序只有在明确的被要求挂起的时候才会被挂起.lua的协程和dart里的sync与yield组合效果是一样的(同步生成器)(不懂也没关系).

参考代码

```lua
local function func(args)
    print ("func start")
    print("func args:",args)
    local v1=args+1
    print("func v1:",v1)
    local r2=coroutine.yield(v1)
    print("func r2:",r2)
    local v3=r2+1
    print("func v3:",v3)
    return v3
end

local function main()
    local co=coroutine.create(func)
    print("create coroutine")
    local status,r1
    local args=1
    status,r1=coroutine.resume(co,args)
    print("main r1:",status,r1)
    local v2=r1+1
    print("main v2:",v2)
    local r3
    status,r3=coroutine.resume(co,v2)
    print("main r3:",status,r3)
    local r4
    status,r4=coroutine.resume(co,666)
    print("main r4:",status,r4)
end

main()

--[[运行结果:
create coroutine
func start
func args:  1
func v1:  2
main r1:  true  2
main v2:  3
func r2： 3
func v3:  4
main r3:  true  4
main r4:  false  cannot resume dead coroutine
]]--
```

## status,wrap和running

`coroutine.status()`:查看 coroutine 的状态,coroutine 的状态有三种:dead,suspended,running

`coroutine.wrap()`:创建 coroutine,返回一个函数,一旦你调用这个函数就进入coroutine,相当于 create + resume

`coroutine.running()`:一个 coroutine 就是一个线程,当使用running方法的时候,就是返回当前coroutine的线程号,如果是主协程,后面就跟一个true,否则跟一个false

