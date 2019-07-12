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

在估计条件概率$$P(X\|Y)$$时出现概率为0的情况怎么办？

简单来说：引入$λ，当λ=1$时称为拉普拉斯平滑。


## Lipschitz条件
利普希茨连续条件（Lipschitz continuity），以德国数学家鲁道夫·利普希茨命名，是一个比通常连续更强的光滑性条件。
直觉上，利普希茨连续函数限制了函数改变的速度。
符合利普希茨条件的函数的**斜率**，必小于一个称为利普希茨常数的实数（该常数依函数而定）。

对于函数 $y=f(x)$ 在定义域为$D$上，如果存在$L∈R$ ,且$L>0$，对任意$x1,x2∈D$，有： 

\begin{equation}
   |f(x_1)-f(f_x2)| <= L*|x_1-x_2|
\end{equation}


**定理的大白话翻译**：
存在一个实数$L$，使得对于函数$f(x)$上的每对点，连接它们的线的斜率的绝对值不大于这个实数$L$。
最小的$L$称为该函数的Lipschitz常数，即$f(x)$在$D$上的**Lipschitz常数**。

从这里可以看出，**Lipschitz常数并不是固定不变的，而是依据具体的函数而定**。

**举个栗子**：
$f(x)=|x|，K=1$  符合利普希茨(Lipschitz)条件。
因为f(x)在x=0处是不可微的，由此可见符合Lipschitz条件的函数未必处处可微。 


## Jensen 不等式
Jensen不等式是关于凸函数性质的不等式，它和凸函数的定义是息息相关的。主要有以下两种应用场景：

- **Jensen不等式的两点形式(凸函数常规性质)**

凸函数是一个定义在某个向量空间的凸子集$C$(区间)上的实值函数$f$，如果在其定义域$C$上的任意两点$x_1, x_2, 0<=\lambda<=1$ ，有

$$
   \lambda f(x_1)-(1-\lambda)f(x_2) \geq f(\lambda x_1+(1-\lambda)x_2) \eqno{(1)}
$$

若对于任意点集${x_i}$，若$\lambda_i \geq 0$且$\sum_{i=1} \lambda_i=1$

$$
\begin{aligned}
   f(\sum_{i=1}^{M} \lambda_i x_i) \leq \sum_{i=1}^{M} \lambda_i f(x_i)
\end{aligned}
$$

- **期望的大小判断**

在概率论中，如果把$\lambda_i$看成取值为$x_i$的离散变量$X$的概率分布，那么可以写成

$$
\begin{equation}
   f(E[x]) \leq E[f(x)]
\end{equation}
$$

其中, $E[·]$ 表示期望。





---
# 相关引用
1. [Lipschitz常数、Lipschitz条件](https://blog.csdn.net/Chaolei3/article/details/81202544)
2. [Jensen不等式-维基百科](https://en.wikipedia.org/wiki/Jensen%27s_inequality)
3. [如何理解 Jensen 不等式？](https://www.zhihu.com/question/53866462)


---
# Latex使用
1. [Latex数学符号](https://blog.csdn.net/SSL_ZYC/article/details/80977235)
2. [Latex大型运算符上下标](https://blog.csdn.net/hfut_jf/article/details/51043642)
3. [latex公式标号测试](https://blog.csdn.net/itnerd/article/details/86001278)
4. [Latex公式与编号](https://www.xuebuyuan.com/3260115.html)

---
# markdown使用
1. [markdown需要转义的字符](https://blog.csdn.net/xianghongai/article/details/78976273)

