--- 
layout: post
title: 中文分词技术简介
tags: 
- "机器学习"
- "自然语言处理"
- "分词"
status: publish
type: post
published: true
---
# 关于中文分词

分词是中文自然语言处理(Natural Language Processing)的第一步，在文本聚类、文本分类、智能检索、自动摘要等应用中，都要首先对中文文本进行分词处理，所谓中文分词 (Chinese Word Segmentation) 指的是将连续的字序列按照一定的规范重新组合成词序列的过程。

# 分词算法的基本思想

目前的分词算法交多，大致上可归纳为三类：基于字符串匹配的方法、基于理解的方法和基于统计的方法。

## 基于字符串匹配的方法


+ 该类型算法也称机械分词法，它按照一定的策略将待分析汉字串与词典中的词条进行匹配，若在词典中找到某个字符串，则匹配成功。该算法需要确定三个基本要素: 词典、扫描方向、匹配原则。比较成熟的几种方法有: 最大匹配法(Maximum Matching)、逆向最大匹配法(Backward Maximum Matching)、双向最大匹配法(Bi-Direction Matching)、最少切分法等。
+ 实际应用中，往往把基于字符匹配的分词方法作为一种初分手段，再通过各种其他的语言信息进一步提高切分的准确率。
+ 一种方法是改进扫描方式，称为特征扫描或标志切分，即在等待分析的字符串中识别和切分出一些带有明显特征的词，以这些词作为断点，可将原字符串分为较小的串再来进行机械分词，从而减少匹配的错误率。
+ 另一种方法是将分词和词类标注结合起来，利用丰富的词类信息对分词决策提供帮助，并且在标注过程中又反过来对分词结果进行检验、调整，从而提高切分的准确率。 

## 基于理解的方法

+ 该类算法通过模拟人对句子的理解，达到识别词的效果，其基本思想是在分词的同时进行语义分析、句法分析，利用句法信息和语义信息处理歧义现象。它包括了三个部分：分词子系统、句法语义子系统、总控部分。通常是在总控的协作下，分词子系统和句法语义系统来判断分词的歧义。
+ 这种分词方法的切分精度很高，但是必须依靠大量的语言信息和知识来支撑。而汉语的语言知识很复杂，也比较笼统，难以将各种语言信息直接组织成机器可读取的形式，所以目前应用基于理解的分词方法还比较少，还属于研究的初级阶段。

## 基于统计的方法

+ 该类算法认为词是稳定的汉字组合，在上下文中汉字与汉字相邻共现的概率能够较好地反映成词的可信度。因此对语料中相邻共现的汉字的组合频度进行统计，计算它们的互信息（Mutual Information）并作为分词的依据。
+ 定义两个字的互信息为M(X,Y)=log(P(X,Y)/(P(x)*P(Y))),其中P(X,Y)是汉字X、Y的相邻出现概率，P(X)、P(Y)分别为X、Y在语料中出现的概率。互现信息体现了汉字之间结合关系的紧密程度，该紧密程度高于某一阀值时，便可认为此字组可能构成了一个词。这种方法只需对语料中的字组频度进行统计，不需要切分词典，因而又叫做无词典分词法或统计取词方法。

# 分词算法对比

每种分词算法方法都有自己的优势和劣势，也无法证明哪一种方法最“好”，简单的对比见下表：

![分词算法对比](/upload/pic/2012-06-22-chinese-word-segmentation.png "")

# R语言中文分词示例

        ## 分词-rmmseg4j包 –> Max Matching SEGmentation, http://code.google.com/p/mmseg4j/
        library(rmmseg4j)
        mmseg4j("这是一个中文分词软件。")
        mmseg4j("中国人民银行。")
        mmseg4j("中国人民银行。", method="maxword")
        mmseg4j(c("这是一个中文分词软件。", "中国人民银行。"))

        # 使用自定义字典
        mmseg4j("不喜欢",dicDir="d:/")
        con=file("d:/wordstest.dic",encoding="UTF-8")
        writeLines("喜欢",con)
        close(con)
        mmseg4j("不喜欢",dicDir="d:/")
        mmseg4j("不喜欢",dicDir="d:/",reload=TRUE)
        # test reload
        con=file("d:/wordstest.dic",encoding="UTF-8")
        writeLines("不喜欢",con)
        close(con)
        mmseg4j("不喜欢",dicDir="d:/",reload=FALSE)
        mmseg4j("不喜欢",dicDir="d:/",reload=TRUE)

        ## 分词-rsmartcn包 –> http://code.google.com/p/imdict-chinese-analyzer/ 的接口
        library(rsmartcn) # 不支持个性化词库？
        smartcn("这是一个中文分词软件")
        smartcn(c("这是一个中文分词软件", "这是一个测试"))

        ## 分词-RQDA http://rqda.r-forge.r-project.org/
        library(RQDA)
        RQDA()
