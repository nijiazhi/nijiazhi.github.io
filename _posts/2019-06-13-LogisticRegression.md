---
layout: post
title: 你真的了解逻辑回归？
categories: [Machine Learning]
tags: LogisticRegression
---

### Index
<!-- TOC -->
- [背景](#背景)
- [Logit函数](#Logit函数)
- [Sigmoid函数](#Sigmoid函数)
- [Softmax函数](#Softmax函数)
<!-- /TOC -->

---
## 背景

在各种机器学习入门教程中，逻辑回归模型（Logistic/Logit Regression）经常被拿来作为入门的机器学习模型，各种面试中手推逻辑回归也变成了一个必考科目。看起来，逻辑回归模型好像很简单，甚至容易被认为是一个拍脑袋想出的naive的模型。在这里，想问问你，你真的了解逻辑回归么？（本篇博客的逻辑框架参考了夕小瑶的文章，她确实思路很赞）


## 常用的符号表示

| 符号 | 含义 |
|:-----------:|:------------:|
| $$p$$    | 概率  |

---
# 浅入·逻辑回归

逻辑回归模型是用于**二类分类**的机器学习模型，有个几个注意点千万要懂：

- 不要说逻辑回归是一个回归模型啊！（虽然里面有线性回归的内容在，但它是做分类的)
- 不要说逻辑回归可以做多类分类啊！（那是二类分类器的组合策略问题，而与逻辑回归分类器本身的构造没有半毛钱关系）

那么，我们怎么将$n$维向量$\vec{x} = [x_1, x_2, \cdots, x_n]$映射成一个点$y$呢？很容易想到就是将向量$\vec{x}$与另一个向量做内积，这个向量我们称为参数$\vec{\theta}$，即$\vec{\theta} = [\theta_1, \theta_2, \cdots, \theta_n]$，所以做内积就是$\vec{x}*\vec{\theta}^\mathrm{T}$（即行向量$\vec{x}$ **乘以** 行向量$\vec{\theta}$的转置），最终会得到一个数。

但是，如果$\vec{x} = [0, 0, \cdots, 0]$时，输出$y$应等于1，那怎么办呢？

这时$\vec{x} * \vec{\theta}^\mathrm{T}$肯定也是$0$啊！所以为了解决这个问题，要再加个常数$b$，所以现在是$\vec{x} * \vec{\theta}\mathrm{T} + b$。为了看起来好看简洁，在$\vec{x}$的最开头加个$1$，把$b$扔到$\theta$的最开头，所以就成了新版的$\vec{x} * \vec{\theta}^\mathrm{T}$，当然此时有：

$$
\begin{cases}
    \vec{x}      = [1,\ \vec{x}]\\
    \vec{\theta} = [b,\  \vec{\theta}]\\
\end{cases}
$$



---
# 深出·逻辑回归

## Logit模型和Logistic模型 


### Logit函数

Logit可以理解成Log-it，这里的it指的是**Odds**（“几率”，等于$p/1-p$）。一个Logit变换的过程如下图所示：

![logit](/assets/images/blog/LogisticRegression/logit.png)

在统计学中，Logit函数也称为log-odds函数，它可以将概率值p（区间为$[0, 1]$）映射到$(-\infty， +\infty)$，图像如下：

![logit-pic](/assets/images/blog/LogisticRegression/logit-pic.png)

Logit函数的数学变换如下：

$$
\begin{aligned}
   logit(p) & = \log{\left( \frac{p}{1-p} \right)} \\
            & = \log{(p)} -log{(1-p)} \\
            & = -\log{\left( \frac{1}{p} - 1 \right)}
\end{aligned}
$$

### Logit模型 vs Logistic模型

当我们讨论**Logit模型**时候，指的是下面这种形式：

$$
\begin{aligned}
   logit(p) & = \log{\left( \frac{p}{1-p} \right)} \\
            & = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \cdots + \beta_n x_n
\end{aligned}
$$

注意，等号右侧是自变量的线性组合（是不是快想到了线性回归？）。当我们只考虑**一个自变量**时：

$$
\begin{aligned}
   \log{\left( \frac{p}{1-p} \right)} = \beta_0 + \beta_1 x_1
\end{aligned}
$$

两边同时做指数运算：

$$
\begin{aligned}
   \left( \frac{p}{1-p} \right) = e^{\beta_0 + \beta_1 x_1}
\end{aligned}
$$

最后，整理一下，可以得到：

$$
\begin{aligned}
   p & = \frac{e^{\beta_0 + \beta_1 x_1}}{1+e^{\beta_0 + \beta_1 x_1}} \\
     & = \frac{1}{1+e^{-(\beta_0 + \beta_1 x_1)}}
\end{aligned}
$$

哎呦，你看上式不就是Logistic模型么。所以这两个模型对应的函数，其实是互逆的。小结一下：

- Logit模型的左侧是Odds的对数，而Logistic模型的左侧是概率
- Logit模型的右侧是一个线性结构，而Logistic模型的右侧是非线性的
- 二者可以相互转化


## Sigmoid函数

## Softmax函数

---
# 相关引用
1. [Logit wikipedia](https://en.wikipedia.org/wiki/Logit)
2. [浅入深出被人看扁的逻辑回归](https://mp.weixin.qq.com/s?__biz=MzIwNzc2NTk0NQ==&mid=2247484011&idx=1&sn=42e4f331db843091c5c3809a4d259fad&chksm=970c2abda07ba3abb3963c2defcc644582f28bbdc23f3d669d022cd032e637d2ca8b6b48ca62&scene=21#wechat_redirect)
3. [深入深出Sigmoid与Softmax的血缘关系](https://mp.weixin.qq.com/s?__biz=MzIwNzc2NTk0NQ==&mid=2247484122&idx=1&sn=41628bf3169b9ef3fa107646d483bae5&chksm=970c2a0ca07ba31ae1939e316c15695c83556c347e0b38bb80dde3048533de7de388ec2a6544&scene=21#wechat_redirect)
4. [Logit模型和Logistic模型有什么区别？](https://zhuanlan.zhihu.com/p/30659982)
