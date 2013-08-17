--- 
layout: post
title: Logistic回归模型：基本思想
tags: 
- "机器学习"
- "分类"
- "Logistic"
status: publish
type: post
published: true
---
回归分析是研究因变量Y与自变量X<sub>1</sub>, X<sub>2</sub>, …, X<sub>p</sub>之间的关系，建立Y为X<sub>1</sub>, X<sub>2</sub>, …, X<sub>p</sub>函数（回归函数）的过程，其主要目的是用自变量X<sub>1</sub>, X<sub>2</sub>, …, X<sub>p</sub>对Y进行预测。回归分析的模型按是否线性可分为：线性回归模型（Linear Regress Model）和非线性回归模型（Nonlinear Regress Model）。

多重线性回归要求因变量为连续型变量，且服从正态分布，它在定量分析的实际应用中非常流行。但是当因变量为分类变量，如是否流失，是否购买商品等时，多重线性回归就不适用了；Logistic回归模型通过构建以概率的某个函数（似然比的对数）为因变量的线性函数（也就是广义线性模型），来实现对分类因变量的预测。

# Logistic函数

Logistic函数的值域在0和1之间，可以用来描述一个事件发生的概率，它的曲线是一条S型的曲线，其特点是开始变化快，逐渐变慢，最后饱和。比如一个简单的Logistic函数有如下形式：

        f(z)=e<sup>z</sup>/(e<sup>z</sup> + 1)=1/(1+e<sup>-z</sup>)

该函数对应的曲线如下：

![LR](/upload/pic/2012-09-27-lr-curve.png "")

该曲线的好处是它的自变量的范围是从-∞到+∞，而值域的范围限制在0到1之间（概率函数），这样Logistic函数就和一个概率联系起来了。另外，自变量的取值范围在-∞到+∞，保证了可以把各个自变量用以下形式组合起来：

    z=β<sub>0</sub>+β<sub>1</sub>x<sub>1</sub>+β<sub>2</sub>x<sub>2</sub>+...+β<sub>k</sub>x<sub>k</sub>

不管组合成多大或多小的值，最后依然会得到一个概率分布。上述组合中，X表示影响概率预测的各种信息，β为各种信息的自回归参数，表示相应信息的重要性，β0是一个特殊参数，它和任何变量无关，可以保证在没有任何信息时，有一个稳定的概率分布。

为了方便理解，可以将以上logistic函数用另外两种等价形式改写：

    P=e<sup>Y</sup>/(1+e<sup>Y</sup>)，或ln(P/(1-P))=Y
    其中Y=β<sub>0</sub>+β<sub>1</sub>x<sub>1</sub>+β<sub>2</sub>x<sub>2</sub>+...+β<sub>k</sub>x<sub>k</sub>

# 两类问题的Logistic回归模型

两类问题的Logistic回归模型是预测向量x = (x<sub>1</sub>, x<sub>2</sub>, …, x<sub>p</sub>)<sup>T</sup>（x<sub>1</sub>, x<sub>2</sub>, …, x<sub>p</sub>为X<sub>1</sub>, X<sub>2</sub>, …, X<sub>p</sub>的观测值）关于类y（y∈{1,-1}）的后验概率。模型基于如下基本假设：类条件概率密度函数（Probability density function）的对数之差在x上是线性的，即

    log[p(x|y=1)/p(x|y=-1)]=β<sub>0</sub>+β<sub>T</sub>x    公式（2.1）

其中，参数β称为权向量，可通过非线性优化方法进行估计。

实践表明，上述模型在许多情况下都是正确的，并已大量应用于背离正态分布的真实数据集中。

对于两类问题，根据贝叶斯定理，向量x属于类y=1的后验概率为：

    p(y=1|x)=[p(y=1)*p(x|y=1)]/[p(y=1)*p(x|y=1)+p(y=-1)*p(x|y=-1)]    公式（2.2）

由全概率公式，可知

    p(x)=p(y=1)*p(x|y=1)+p(y=-1)*p(x|y=-1)

则，公式（2.2）可表示成：

    p(y=1|x)=[p(y=1)*p(x|y=1)]/p(x)

同理：

    p(y=-1|x)=[p(y=-1)*p(x|y=-1)]/p(x)

由公式（2.3）、公式（2.4）得到p(x|y=1)、p(x|y=-1)，代入公式（2.1）的等价形式：

    p(x|y=1)/p(x|y=-1)=exp(β<sub>0</sub>+β<sub>T</sub>x)

得到

    [p(y=1|x)*p(x)/p(y=1)]/[p(y=-1|x)*p(x)/p(y=-1)]=β<sub>0</sub>+β<sub>T</sub>x

又，

    p(y=-1|x)=1-p(y=1|x)

代入公式（2.5），求得p(y=1|x),即为两类问题的Logistic回归函数

    p(y=1|x)=exp(β<sub>0</sub><sup>'</sup>+β<sup>T</sup>)/[1+exp(β<sub>0</sub><sup>'</sup>+β<sup>T</sup>)]

其中，

    β<sub>0</sub><sup>'</sup> = β<sub>0</sub> + log[p(y=1)/p(y=-1)]

