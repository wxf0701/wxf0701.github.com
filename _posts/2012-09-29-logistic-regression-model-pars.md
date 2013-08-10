--- 
layout: post
title: Logistic回归模型：模型参数
tags: 
- "机器学习"
- "分类"
- "Logistic"
status: publish
type: post
published: true
---
本文介绍Logistic回归模型参数的估计、检验和解释

模型参数的估计-最大似然估计

假设Y在X1,X2,…Xk作用下的某个事件是否发生的指示变量。其赋值为：

clip_image002[10]

那么，第i个观察对象对似然函数的贡献量为：

clip_image004[8]

其中Pi、Qi为某个事件发生的概率和不发生的概率（Pi + Qi=1）：

clip_image006[8] clip_image008[8]

clip_image010[8]

当各事件是独立发生时，则n个观察对象所构成的似然（Likelihood）函数L是每个观察对象的似然函数贡献量的乘积，即

clip_image012[8]

式中∏为i从1到n的连乘积。

根据最大似然估计法的原理（存在即是合理，最符合观察数据的最有优势），使得L达到最大时的参数值即为所求的参数估计值，计算时通常是将该似然函数取自然对数（称为对数似然函数）后，用Newton-Raphson迭代算法求解参数估计值。

模型参数的显著性检验

由样本估计参数，并建立了logistic方程后，参数的估计值不等于0并不一定意味着参数不等于0，也不意味着回归方程就一定成立，还需通过假设检验才能作出推断。与logistic回归分析有关的假设检验包括两个内容：一是检验整个模型，即检验因变量与自变量之间的关系能否用所建立的回归方程来表示；二是检验单个回归系数是否为0，即检验单个自变量对因变量的影响是否存在。

似然比检验(Likelihood Ratio Tetst)常用于对整个模型的检验，检验的假设为：H0：所有自变量的总体回归系数均为0，H1：自变量的总体回归系数不全为0。假设模型A含有p个自变量，相应的达到极大的对数似然函数值记为lnL0；模型B是在模型A的p个自变量基础上新加入一个或几个自变量，自变量个数变为l，其相应的达到极大的对数似然函数值记为lnL1。通过比较模型A与模型B的极大似然函数值，构建似然比检验统计量G，

clip_image002

如果说，极大对数似然函数值lnL0和lnL1分别度量p个自变量和l个自变量模型“似然”的程度，那么，统计量G度量的则是增加l-p个自变量后，模型“似然”程度的增量。可以证明，在H0成立的条件下，如果样本量较大，G近似地服从自由度为l-p的Chi-Square分布，因此上式亦常记为：

clip_image006

Wald检验（Wald Test）可用于对单个回归系数的检验，检验的假设为H0：βj=0，H1: βj<>0，Wald检验统计量为

clip_image014[8]

可以证明，在H0成立的条件下，如果样本量较大，前者近似地服从标准正态分布N(0,1)，后者近似地服从自由度为1的Chi-Square分布。

模型参数的意义

类似线性回归，β0表示模型中所有自变量均为0时，logit(P)的值；回归系数βj表示在控制其他自变量时，自变量Xj变化一个单位所引起logit(P)的改变量。

根据logistic回归模型的公式，我们有优势的表达式

clip_image016[8]

以网站客户流失分析为例，有一个变量X表示“是否为普通用户”，“普通用户”组(X=1)流失的优势为

clip_image018[8]

“非普通用户-会员”组（X=0）流失的优势为

clip_image020[8]

两组的优势比(Odds Ratio, OR) 为

clip_image022[8]

一般地，根据多个自变量的logistic回归模型，在其他变量取值不变的情形下，与变量Xj的二个水平C1与C2（C2> C1）相对应的事件的优势比为

clip_image024[8]

当Xj的二个水平相差1个单位时：

clip_image026[8]

可见，logistic回归模型的参数βj就是在其他变量取值不变的情形下，Xj增加1个单位后与增加前相比较，事件的优势比。当变量Xj的回归系数βj>0时，Xj增加1个单位后与增加前相比，事件的优势比ORj>1，表明与Xj相应的因素为危险因素；βj<0时，Xj增加1个单位后与增加前相比，事件的优势比ORj<1，表明与Xj相应的因素为保护因素；βj=0时，Xj增加1个单位后与增加前相比，事件的优势比ORj=1，表明与Xj相应的因素对结果变量不起作用。