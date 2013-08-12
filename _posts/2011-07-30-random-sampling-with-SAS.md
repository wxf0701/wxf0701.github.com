--- 
layout: post
title: 利用SAS进行随机抽样
tags: 
- "机器学习"
- "抽样"
status: publish
type: post
published: true
---
在构建数据挖掘模型过程中，有时我们无法对所有的整体进行全面研究，有时我们希望将整体划分为训练集、验证集、测试集三份用于不同目的的数据集，甚至在[K-折交叉验证](http://en.wikipedia.org/wiki/Cross-validation_(statistics),"")中，我们需要把样本随机的划分为K份数据子集。本文介绍SAS的[SURVEYSELECT](http://support.sas.com/documentation/cdl/en/statug/63347/HTML/default/viewer.htm#surveyselect_toc.htm,"")过程和[RANUNI](http://support.sas.com/documentation/cdl/en/lrdict/64316/HTML/default/viewer.htm#a000202926.htm,"")函数在随机抽样方面的应用。

# 0 - 读入数据集，并对数据集按分层变量进行排序。本文数据集采用[students.txt](http://sdrv.ms/1cGK6CD,"")：

* 从students.txt读入文件到数据集students;

`
DATA students;
    INFILE 'C:\students.txt';
    INPUT id class $ gender $ math english history chem phys literat;
RUN;
`
	
* 查看数据集内容;

    PROC PRINT DATA = students;
        TITLE 'Students”s class gender & scores';
    RUN;

* 对二维列联表（班级、性别）进行频数统计;

    PROC FREQ DATA = students;
        TABLES class * gender /NOPERCENT NOROW NOCOL;
RUN;

* 首先对数据集按分层变量进行排序;

    PROC SORT DATA = students;
        BY class gender;
    RUN;


# 1 - 利用SURVEYSELECT过程进行等比例分层抽样

* 利用SURVEYSELECT过程对数据集进行等比例分层抽样;

    PROC SURVEYSELECT DATA = students out = samp1 method = srs samprate = .5 seed = 9876;
        STRATA class gender;
    RUN; 

* 查看分层抽样的结果;

    PROC FREQ DATA = samp1;
        TABLES class * gender /NOPERCENT NOROW NOCOL;
    RUN;


# 2 - 利用SURVEYSELECT过程进行不等比例分层抽样

* 利用SURVEYSELECT过程对数据集进行等不比例分层抽样;

    PROC SURVEYSELECT DATA = students out = samp2 method = srs samprate = (.4 .6 .4 .6 .4 .6) seed = 9876;
        STRATA class gender;
    RUN;

* 查看分层抽样的结果;

    PROC FREQ DATA = samp2;
        TABLES class * gender /NOPERCENT NOROW NOCOL;
    RUN;

# 3 - 利用SURVEYSELECT过程根据抽样数量进行分层抽样

* 利用SURVEYSELECT过程对数据集进行指定数量的分层抽样;

    PROC SURVEYSELECT DATA = students out = samp3 method = srs n = (8 4 6 8 5 7) seed = 9876;
        STRATA class gender;
    RUN;

* 查看分层抽样的结果;

    PROC FREQ DATA = samp3;
        TABLES class * gender /NOPERCENT NOROW NOCOL;
    RUN;


# 4 - 利用随机数函数RANUNI对数据集进行粗略划分

* 利用RANUNI函数将数据集粗略的划分为N=5份;

    DATA s1 s2 s3 s4 s5;
        SET students;
        r = RANUNI(991889);
        IF r<0.2 THEN OUTPUT s1;
        ELSE IF r<0.4 THEN OUTPUT s2;
        ELSE IF r<0.6 THEN OUTPUT s3;
        ELSE IF r<0.8 THEN OUTPUT s4;
        ELSE OUTPUT s5;
        DROP r;
    RUN;


# 5 - 利用随机数函数RANUNI对数据集进行精确划分

* 根据数据集创建视图students_v,增加随机数列;

    DATA students_v /view=students_v;
        SET students;
        srt = RANUNI(999890);
    RUN;

* 按照随机数列对数据集进行排序,创建数据集students_srt,删除随机数列;

    PROC SORT DATA = students_v OUT = students_srt(DROP = srt); 
        BY srt; 
    RUN;

*  将数据集精确地划分为N=5份;

    DATA s1 s2 s3 s4 s5;
        RETAIN per ;
        SET students_srt NOBS= total;
        IF _N_ = 1 THEN per = INT(total/5);
        if _N_<= per then output s1;
        ELSE IF _N_<= 2 * per THEN OUTPUT s2;
        ELSE IF _N_<= 3 * per THEN OUTPUT s3;
        ELSE IF _N_<= 4 * per THEN OUTPUT s4;
        ELSE OUTPUT s5;
        DROP per;
    RUN;