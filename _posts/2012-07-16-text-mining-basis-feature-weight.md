--- 
layout: post
title: 文本挖掘基础：特征项权重的计算
tags: 
- "机器学习"
- "自然语言处理"
- "特征权重"
status: publish
type: post
published: true
---
在完成文档特征项的选取后，还需要计算每个特征项的权重。权重的大小可以直观地反映该特征项对文档类别的区分能力，它在很大程度上影响了文本分类算法的整体性能。

特征项权重计算函数主要有布尔函数（若第j个特征项在第i个文档的出现频率大于1，则文本i的第j个特征项的权值为1，否则为0）、根号函数(将第j个特征项在第i个文档的出现频率的根号值作为权重)、对数函数（将第j个特征项在第i个文档的出现频率+1的对数值作为权重）和TF-IDF函数。TF-IDF因其算法简单、有效，所以在工程实践中得到了广泛的青睐。

TF-IDF函数的基本思想

词频-逆向文档频率TF-IDF(Term Frequency–Inverse Document Frequency)是Salton在1988年提出的一种统计方法，用以评估一个特征项对于一个文档集中的其中一份文档的重要程度。其基本思想是：如果某个词或短语在一篇文章中出现的频率高，并且在其他文档中很少出现，则认为此特征项具有很好的类别区分能力。

TF-IDF函数解析

TF-IDF目前有很多公式变种，下面仅介绍最基本、最常用的一个。

所谓TF(Term Frequency)，即一个特征项在某一个文档中出现的频数，如“篮球”特征项在一个文档中出现了8次，则TF=8；

TF表示法的缺陷在于，没有考虑到如果一个特征项在众多文档中出现，那么这个特征项将失去特征化的作用。可以想象一下，如果100个文档中有99个文档出现了“好”这一特征项，那么，很显然“好”对于区分文档之间的差异化特征就几乎没有什么作用。

IDF(Inverse Document Frequency)正是用来弥补TF的这一缺陷的，它本质上是一个惩罚因子，用来度量特征项在所有文档集中出现的频繁程度。更明确的讲，如果一个特征项在所有的文档中出现，则通过IDF可以降低该特征项的权重，反之，如果该特征项在较少的文档中出现，则通过IDF提升该词的权重。

IDF的具体公式为IDF(i)=log(N/DF(i)+1)，其中N为所有文档的数量，DF(i)为出现第i个特征项的文档数量。

好了，有了TF、IDF后，对任意一个特征项权重就可以通过公式W(i)=TF(i)*IDF(i)来计算了。

不过上面的公式还有些问题，比如在一个短文档和一个长文档中，特征项“好”均出现了10次，根据上面的公式，TF和IDF的值都是相同的，因此计算得到的权重也是一样的，但是，显然有些不合常理，因为，在特征项“好”出现频次相同的情况下，与长文档相比，它应该更能反映短文档的特征信息。

基于以上理解，TF-IDF的公式最终修正为W(i)=[TF(i)/|V|]*IDF(i)，其中|V|为文档集中对应文档的长度，也就是所有特征项的词频数之和。

当然，由于TF-IDF结构本身的简单性，经典TF-IDF函数还存在着种种问题，如数据集关于类别分布的不均衡造成IDF惩罚作用的失效，TF-IDF未考虑特征项在类内、类间的分布情况造成权值计算结果不合理等等，在相关的论文中也提出了不少解决办法，感兴趣的同学可以翻一下相关的文献做进一步的研究。