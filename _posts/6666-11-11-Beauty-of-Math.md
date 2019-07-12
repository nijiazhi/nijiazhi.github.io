---
layout: post
title: 数学之美
categories: [Mathematics]
tags: Math
---

### Index
<!-- TOC -->
- [背景](#背景)
- [Laplace平滑](#Laplace平滑)
- [Lipschitz条件](#Lipschitz条件)
- [Jensen不等式](#Jensen不等式)
<!-- /TOC -->

---
## 背景
在机器学习/数据挖掘的学习过程中，你总会遇到一些神奇的数学表达（聊起来很高大上，感觉巨难无比）。在这里，想把相关的额概念做一些总结，帮助我们更好地理解和学习数学这个‘大坑’！


## Laplace平滑
中文名称：拉普拉斯平滑

在估计条件概率$$P(X|Y)$$时出现概率为0的情况怎么办？

简单来说：引入$λ，当λ=1$时称为拉普拉斯平滑。


## Lipschitz条件
利普希茨连续条件（Lipschitz continuity），以德国数学家鲁道夫·利普希茨命名，是一个比通常连续更强的光滑性条件。
直觉上，利普希茨连续函数限制了函数改变的速度。
符合利普希茨条件的函数的**斜率**，必小于一个称为利普希茨常数的实数（该常数依函数而定）。

对于函数 $y=f(x)$ 在定义域为$D$上，如果存在$L∈R$ ,且$L>0$，对任意$x1,x2∈D$，有： 

$$
\begin{equation}
   |f(x_1)-f(f_x2)| <= L*|x_1-x_2|
\end{equation}
$$

**定理的大白话翻译**：
存在一个实数$L$，使得对于函数$f(x)$上的每对点，连接它们的线的斜率的绝对值不大于这个实数$L$。
最小的$L$称为该函数的Lipschitz常数，即$f(x)$在$D$上的**Lipschitz常数**。

从这里可以看出，**Lipschitz常数并不是固定不变的，而是依据具体的函数而定**。

**举个栗子**：
$f(x)=|x|，K=1$  符合利普希茨(Lipschitz)条件。
因为f(x)在x=0处是不可微的，由此可见符合Lipschitz条件的函数未必处处可微。 


## Jensen 不等式
Jensen不等式是关于凸函数性质的不等式，它和凸函数的定义是息息相关的。主要有以下两种应用场景：
- 凸函数的常规使用场景

- 期望的大小判断






---
# 相关引用
1. [Lipschitz常数、Lipschitz条件](https://blog.csdn.net/Chaolei3/article/details/81202544)
2. [Jensen不等式-维基百科](https://en.wikipedia.org/wiki/Jensen%27s_inequality)
3. [如何理解 Jensen 不等式？](https://www.zhihu.com/question/53866462)
