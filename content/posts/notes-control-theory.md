---
title : '自控原理笔记'
# slug : 'notes-control-theory'
date : 2024-03-17T14:40:00+08:00
draft : false
tags : ['笔记']
toc : ture
mathjax : ture
---


考研时的笔记，用于快速查阅，所以记得非常零散；笔记本快翻烂了，转移到电脑上。由于个人能力有限。不能保证笔记中的内容全都正确，如发现错误，欢迎在[GitHub](https://github.com/X666TV/page/issues)上留言。

## 经典控制理论部分

### 拉氏变换

即拉普拉斯变换，正变换公式如下，其中f(t)为原函数， F(s)为象函数

$$L[f(t)]=F(s)=\int_{0}^{\infty}f(t)e^{-st}dt$$

常用拉氏变换如下：

| f(t)                  | F(s)                          |
| --------------------- | ----------------------------- |
| 单位冲激 $\delta (t)$ | $1$                           |
| 单位阶跃 $1(t)$       | $\frac{1}{s}$                 |
| 单位斜坡 $t$          | $\frac{1}{s^2}$               |
| 正弦 $\sin(\omega t)$ | $\frac{\omega}{s^2+\omega^2}$ |
| 余弦 $\cos(\omega t)$ | $\frac{s}{s^2+\omega^2}$      |
| $e^{-at}$             | $\frac{1}{s+a}$               |

拉氏变换的性质

1. 线性：叠加性和齐次性

2. (时域)微分定理：$L[f'(t)]=sF(s)-f(0)$

3. (时域)积分定理：$L[\int_{0}^{t}{f(t)dt}]=\frac{1}{s}F(s)+\frac{1}{s}f^{-1}(0)$

   - 微分定理和积分定理本质上是一样的，把微分定理中的导函数换成普通函数，则函数变成其原函数，再移项即可得积分定理

4. 位移定理：正正反反（正变换位移符号不变，反变换位移符号相反）

   - 正：$$L[f(t-\tau)]=e^{-\tau s}F(s)$$

   - 反：$$F(s+a)=L[e^{-at}f(t)]$$

5. 终值定理：$\lim\limits_{t \to\infty }{f(t)} =\lim\limits_{s \to 0}{sF(s)}$

6. 初值定理：$\lim\limits_{t \to 0}{f(t)} =\lim\limits_{s \to \infty}{sF(s)}$

   - 终值定理和初值定理的使用条件是各极限存在

7. 卷积定理：

   记

    $$L[f(t)]=F(s)$$
    $$L[g(t)]=G(s)$$
    $$f(t)*g(t)=\int_{0}^{\infty}f(t-x)g(x)dx=\int_{0}^{\infty}f(x)g(t-x)dx$$

   则
     $$L[f(t)*g(t)]=F(s)\cdot G(s)$$
     $$L[f(t)\cdot g(t)]=F(s)*G(s)$$

传递函数：零初始条件下的拉氏变换之比

### 梅森(Mason)公式

需要先作出系统的信号流图，用熟了也可以直接用方框图

系统闭环传函：

$$T=\frac{1}{\Delta}\sum\limits_{k=1}^{n}p_k\cdot\Delta_k$$

其中：

$p_k$： 第k条前向通道(的增益)

$\Delta=1-\sum\limits L_1+\sum\limits L_2-\sum\limits L_3+\cdots+(-1)^n\sum L_n$

$L_1$：单独回环增益

$L_2$：互不接触(无公共节点)回环增益两两相乘的乘积之和

$L_2$：互不接触(无公共节点)回环增益每三个相乘的乘积之和

$\Delta_k$：去掉$p_k$所有节点和边后的信号流图的$\Delta$

### 一阶系统

![一阶系统](../assets/一阶系统.svg)

闭环传函：$G(s)=\frac{1}{Ts+1}$

单位脉冲响应：$r(t)=\delta(t)$

$$C(s)=\frac{1}{Ts+1}$$

$$c(t)=\frac{1}{T}e^{-\frac{t}{T}}$$


![单位脉冲响应](../assets/一阶系统单位脉冲响应.svg)

单位阶跃响应：$r(t)=1(t)$

$$C(s)= \frac{1}{s}\cdot\frac{1}{Ts+1}$$

$$c(t)=1-e^{-\frac{t}{T}}$$

![单位阶跃响应](../assets/一阶系统单位阶跃响应.svg)

> 若输入信号变为原来的导函数，则输出信号也变成原来的导函数

| $t$  | 各种时间参数的定义          | $\frac{c(t)}{c(\infty)}$ |
| ---- | --------------------------- | ------------------------ |
| T    | $c(t)=1-e^{-1}=0.632$       | 63.2%                    |
| 2.3T | 上升时间 $t_r$              | 90%                      |
| 3T   | 调节时间 $t_s(\Delta=0.05)$ | 95%                      |
| 4T   | 调节时间 $t_s(\Delta=0.02)$ | 98%                      |

* 上升时间也指10%~90%所用时间，此时$t_r=2.2T$，常用于过阻尼系统
* 一阶系统的单位阶跃响应不存在峰值时间$T_p$（或者说峰值时间为无穷大）、超调量$\sigma$或$\sigma\%$、衰减比n。

单位斜坡响应

$$C(s)=\frac{1}{s^2}\cdot\frac{1}{Ts+1}$$

$$c(t)=t-T+Te^{-\frac{t}{T}}$$

### 二阶系统

![标准二阶系统 ](../assets/标准二阶系统.svg)

闭环传函：$\Phi(s)=\frac{C(s)}{R(s)}=\frac{\omega_n^2}{s^2+2\xi_n\omega_ns+\omega_n^2}$

$\xi$：阻尼比

$\omega_n$：（无阻尼）自然振荡角频率，固有频率

$\omega_d=\omega_n\sqrt{1-\xi^2}$：阻尼振荡频率

| 阻尼比    | 系统类型     | 特征根分布           | 根       |
| --------- | ------------ | -------------------- | -------- |
| $\xi=0$   | 无阻尼系统   | 一对共轭纯虚根       | $\lambda_{1,2}=\pm j\omega_n $ |
| $0<\xi<1$ | 欠阻尼系统   | 一对共轭复根         | $\lambda_{1,2}=-\xi\omega_n\pm j\omega_d$ |
| $\xi=1$   | 临界阻尼系统 | 两个相等的负实根     | $\lambda_1=\lambda_2=-\omega_n$ |
| $\xi>1$   | 过阻尼系统   | 两个不等的负实根     | $\lambda_{1,2}=-\xi\omega_n\pm\omega_d$ |
| $\xi<0$   | 发散         | 存在位于正半平面的根 | $\cdots$ |

> 标准二阶欠阻尼系统的单位阶跃响应推导
$$
\begin{align*}
C(s)= & \mathit{\Phi}(s)R(s) \\\\
= & \frac{1}{s}\cdot\frac{\omega_n^2}  {s^2+2\xi_n\omega_ns+\omega_n^2}\\\\
= & \frac{1}{s} \\\\
\end{align*}
$$

## 现代控制理论部分

{{< admonition tip>}}
待续...
{{< /admonition >}}
