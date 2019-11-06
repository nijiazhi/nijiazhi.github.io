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
| $p$         | 概率  |
| $h_\Theta$  | 逻辑回归中判别函数  |
| $h_w$       | 逻辑回归中判别函数（和上式相同，$w$和$\Theta$都表示参数）  |

---
# 浅入·逻辑回归

逻辑回归模型是用于**二类分类**的机器学习模型，有以下几个点千万注意：

- 不要说逻辑回归是一个回归模型啊！（虽然里面有线性回归的内容在，但它是做分类的)
- 不要说逻辑回归可以做多类分类啊！（那是二类分类器的组合策略问题，而与逻辑回归分类器本身的构造没有半毛钱关系）

>我们用几个常见考题来浅入逻辑回归：

- **问题1，如何将一个$n$维向量$\vec{x}$映射为1个点$y$？**

很容易想，将向量$\vec{x}$与另一个向量做内积，这个向量我们称为参数$\vec{\theta}$，即$\vec{\theta} = [\theta_1, \theta_2, \cdots, \theta_n]$，所以做内积就是$\vec{x}*\vec{\theta}^\mathrm{T}$（即行向量$\vec{x}$ **乘以** 行向量$\vec{\theta}$的转置），最终会得到一个数。

- **问题2，如果$\vec{x} = [0, 0, \cdots, 0]$时，输出$y$永远等于1，那怎么办呢？**

这时$\vec{x} * \vec{\theta}^\mathrm{T}$肯定也是$0$啊！所以为了解决这个问题，要再加个常数$b$，所以现在是$\vec{x} * \vec{\theta}\mathrm{T} + b$。为了看起来好看简洁，在$\vec{x}$的最开头加个$1$，把$b$扔到$\theta$的最开头，所以就成了新版的$\vec{x} * \vec{\theta}^\mathrm{T}$，当然此时有：

$$
\begin{cases}
    \vec{x}      = [1,\ \vec{x}]\\
    \vec{\theta} = [b,\  \vec{\theta}]\\
\end{cases}
$$

- **问题3，上述函数值域是$(-\infty,\ +\infty)$，但我们要得到的$0$或$1$，上述模型输出100000可咋办？**

直观上，我们需要要把值域限制一下，将值域正负无穷改为$(0, 1)$。那咋改呢？自然想到了下面这个sigmoid函数：

![sigmoid](/assets/images/blog/LogisticRegression/sigmoid.png)

$$
\begin{aligned}
   Sigmoid(z) & = \frac{1}{1+e^{-z}} \\
\end{aligned}
$$

在这个函数的限制下，哪怕输入为正无穷，输出也不会大于1，同理，输入为负无穷，输出也不会为小于-1。这时，我们只需要认为当模型输出值大于0.5时，就认为是逻辑1；当输出值小于0.5时，就认为是逻辑0。预测函数（假设函数）完成，可以给样本贴上类别标签了！

$$
\begin{aligned}
   h_{\theta}(X) & = Sigmoid(X * \Theta^\mathrm{T}) \\
\end{aligned}
$$

- **问题4，训练模型用的 *损失函数/代价函数/目标函数* 是什么呢？**

大概率，你会毫不犹豫的说出**交叉熵**这三个字，至于为什么会利用到交叉熵，而不用最小二乘的loss呢？（因为用了sigmoid的非线性+最小二乘导致非凸哈，感兴趣自己画一下）另外，与其相关的自信息、熵、KL散度、二项分布的交叉熵、最大似然等概念，你是否知道呢？（这里先不扯了，最大似然取对数也可以推出交叉熵这个loss）。它的一般形式如下：

$$
\begin{aligned}
   H(p, q) = \sum\limits_{i=1}^{n} p(x_i) \log{q(x_i)}
\end{aligned}
$$

其中，$p$代表真实分布，可以理解为真实概率，在二分类（二项分布）中，可以认为是label（因为只有0和1，它能当成概率）；$q$代表非真实分布，可以理解为我们的预测概率。所以上述交叉熵的一般形式推广到逻辑回归（二分类、二项分布）中作为损失函数的形式如下：

$$
\begin{aligned}
   J(\Theta) = \frac{1}{m} \sum\limits_{i=1}^{m} \left[ -y^{(i)}\log{h_\Theta(x^{(i)})} - (1-y^{(i)})\log{1-h_\Theta(x^{(i)})} \right]
\end{aligned}
$$

这公式看起来很不错呀，仔细一看也看明白，反正当类别预测值与实际类别完全对起来的时候，$J(\Theta$确实等于0的。

- **问题5，如何优化上述目标函数呢？**

答案很清晰了，**梯度下降**应该已经被说烂了吧。除了这个，那你知道为啥不用解析解、怎么应用牛顿法么？（解析解问题参见reference，它的推导有些小问题，但大致思路是对的，以两个特征为例，因为交叉熵loss和非线性函数，导致求解析解的方程中出现$w1*w2$，而不单纯是$w1,w2$的方程，无法求解）。最后，我们给出梯度下降所需的最终求导公式（过程参见手推图片，我太懒了，不想latex公式了）。

$$
\begin{aligned}
    \Theta_j := \Theta_j + \alpha \left( y^{(i)} - h_\Theta(x^{(i)}) \right) x^{(i)}_j
\end{aligned}
$$

![logistic_gradient](/assets/images/blog/LogisticRegression/logistic_gradient.jpg)

最后，等到$J(\Theta)$收敛到最优值，就得到了最优模型参数$\Theta$

- **问题6，上面几个问题看起来没毛病哈，难道每一步真的都是这么恰好的信手拈来的吗？**

Too young too simle, naive !!!


---
# 深出·逻辑回归

## 逻辑 · 回归

回归是一个基础概念，一个抽象而准确的描述是“回归即为两个或多个随机变量之间的相关关系建立数学模型”，设想一下，如果我们仅考虑两个随机变量，并且将其中一个随机变量看作机器学习的输入，也就是特征向量X，将另一个随机变量看作机器学习的输出，也就是类别预测y。那么回归就是**用一个数学模型*直接*描绘出X到y的映射关系**

想一想我们之前的朴素贝叶斯模型是怎么用X训练模型求y的？是不是用贝叶斯定理呀~也就是下面这样：

$$
\begin{aligned}
    p(C|F_1, \cdots, F_n) = \frac{p(C)p(F_1, \cdots, F_n|C)}{p(F_1, \cdots, F_n)}
\end{aligned}
$$

等式左边就是随机变量y，而等式右边并不是直接用X表示的，而是用其他东西**间接**描述y。所以！回归就是要**直接**用X描绘出y！是直接！

- 当随机变量X与随机变量y呈**线性关系**时，如果我们要用回归模型来描述这两个随机变量的关系，那么这里的回归模型是什么样子的呢？相信机智的你肯定想到啦，这里就是高中就学过的线性回归模型：y=ax+b
- 当随机变量X与随机变量y呈**逻辑关系**时呢？（逻辑不就是0/1嘛），也就是说当随机变量X取某值时，随机变量Y为某一个逻辑值（0或1），那么这里的回归模型是什么样子的呢？相信机智的你肯定想到啦，这里就是大学都没学过的逻辑回归模型（你是不是知道了为啥叫做逻辑回归）


其实我们仔细想一下，逻辑回归模型是难以像线性回归一样直接写出类似于$y=ax+b$这么简洁的形式的，因为y的取值为**离散**的，只有0和1，所以要怎么表示呢？当然是用模型分别表示**y取0的概率和y取1**的概率了。也就是用模型表示出$p(y=1\|X)$和$p(y=0\|X)$

其实为某种形式的回归建立数学模型并不是一件容易的事情，经过先烈的曲折探索，得出了一个神奇的logit函数：

$$
\begin{aligned}
   logit = \log{\left( \frac{q}{1-q} \right)} \\
\end{aligned}
$$

诶？看似简洁，然而有什么用呢？里面既没有x也没有y呀？

## Softmax函数与Sigmoid的血缘关系

先等等，还记得深度学习中经常加在神经网络的顶层来求后验概率$$p(y=j\|x)$$的Softmax函数吗？对就是下面这个熟悉的函数：

$$
\begin{aligned}
   p(y=j|x) = \frac{e^{x^\mathrm{T}} w_j}{\sum_{k=1}^{K} e^{x^\mathrm{T}} w_k}
\end{aligned}
$$

对于我们的二分类问题来说，有$p(y=0\|X)+p(y=1\|X)=1$，那么如果我们令logit公式中的$q=p(y=1\|x)$呢？然后$p(y=1\|x)$用softmax函数表示呢？看看下面优美的推导：

$$
\begin{aligned}
   logit &= \log{\left( \frac{q}{1-q} \right)} \\
         &= \log{\frac{p(y=1|x)}{p(y=0|x)}} \\
         &= \log{\frac{e^{x^\mathrm{T}} w_1}{e^{x^\mathrm{T}} w_0}} \\
         &= \log{e^{x^\mathrm{T}} \Delta w} \\
         &= x^\mathrm{T} \Delta w \\
\end{aligned}
$$

这时候，$x^\mathrm{T} \Delta w$的值不就是反映感知机模型的输出嘛！（即$x^\mathrm{T} \Delta w > 0$则预测类别为正，$x^\mathrm{T} \Delta w < 0$则预测类别为负），所以logit函数我们再把$x^\mathrm{T} \Delta w$整理的好看一点，变成更正常的形式：$wx+b$，然后就可以得到下面的结论：

$$
\begin{cases}
    p(y=1|x) = \frac{e^{w_0 x+b}}{e^{w_0 x+b} + \  e^{w_1 x+b}} = \frac{e^{w x+b}}{1 + e^{w x+b}} \\
    \ \\
    p(y=0|x) = \frac{e^{w_1 x+b}}{e^{w_0 x+b} + \  e^{w_1 x+b}} = \frac{1}{1 + e^{w x+b}}\\
\end{cases}
$$

其中$w=w_1-w_2$，这涉及到softmax其实有一个参数是冗余的，当面对sigmoid函数时候，二分类时只用一个参数$w$就能完整描述。这就是我们前面苦苦寻找的逻辑回归模型！看，随机变量X与随机变量Y的关系竟然直接纳入了一个模型下面！也就是说后验概率**直接**用随机变量X表示了出来！而不是像贝叶斯定理一样**间接**表示后验概率。


## 极大似然估计

有了上面**直接表示的后验概率**，于是建立**似然函数**，通过**极大似然估计**来确定模型的参数。因此设：

$$
\begin{aligned}
   p(y=1|x) = h_w(x)
\end{aligned}
$$

似然函数就表示为：
$$
\begin{aligned}
   L &=  \prod\limits_{i=1}^{m} \left[ [h_w(x^{(i)})^{y^{(i)}}] * [1 - h_w(x^{(i)})^{1-y^{(i)}}] \right]
\end{aligned}
$$

对数似然函数即：

$$
\begin{aligned}
   p(y_i) &=  \sum\limits_{i=1}^{m} \log{p(y^{(i)} | x^{(i)} ; w)} \\
          &=  \sum\limits_{i=1}^{m} \left[ y^{(i)}\log{h_w(x^{(i)})} + (1-y^{(i)})\log{1-h_w(x^{(i)})} \right]\\
\end{aligned}
$$

也就是本文的“浅入”环节的损失函数啦，原来是正儿八经的一步步推出来的！剩下的就交给梯度下降法优化出模型参数吧！


## Logit函数

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

## Logit模型 vs Logistic模型

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
- 二者可以互为逆函数


---
# 相关引用
1. [Logit wikipedia](https://en.wikipedia.org/wiki/Logit)
2. [浅入深出被人看扁的逻辑回归](https://mp.weixin.qq.com/s?__biz=MzIwNzc2NTk0NQ==&mid=2247484011&idx=1&sn=42e4f331db843091c5c3809a4d259fad&chksm=970c2abda07ba3abb3963c2defcc644582f28bbdc23f3d669d022cd032e637d2ca8b6b48ca62&scene=21#wechat_redirect)
3. [深入深出Sigmoid与Softmax的血缘关系](https://mp.weixin.qq.com/s?__biz=MzIwNzc2NTk0NQ==&mid=2247484122&idx=1&sn=41628bf3169b9ef3fa107646d483bae5&chksm=970c2a0ca07ba31ae1939e316c15695c83556c347e0b38bb80dde3048533de7de388ec2a6544&scene=21#wechat_redirect)
4. [Logit模型和Logistic模型有什么区别？](https://zhuanlan.zhihu.com/p/30659982)
5. [Why is the error function minimized in logistic regression convex?](http://mathgotchas.blogspot.com/2011/10/why-is-error-function-minimized-in.html)
6. [为什么LR的MLE无法求解析解？](https://www.zhihu.com/question/45962137)