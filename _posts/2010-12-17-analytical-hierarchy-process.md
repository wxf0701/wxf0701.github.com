--- 
layout: post
title: 层次分析法(AHP)
tags: 
- "层次分析"
status: publish
type: post
published: true
---
关于层次分析法（Analytical Hierarchy Process, AHP）

      日常生活中有许多决策问题，当我们面临多种方案时需要依据一定的标准选择其中的一种方案：例如选购电冰箱，我们可能依据容量、制冷级别、价格、款式、耗电量、品牌信誉、售后服务等方面的因素选择某一种型号的冰箱。面临各种各样的方案，要进行比较、判断、评价并最终作出决策，这个过程主观因素占有相当的比重，这个运用数学方法解决问题带来了极大的不便；

      事实上，过分的依赖于数学模型或过多的依赖人的经验、逻辑推理都不利于正确决策的制定；20世纪70年代美国运筹学家皮茨堡大学教授萨蒂（clip_image004）应用网络系统理论和多目标综合评价方法，提出的一种层次权重决策分析方法——层次分析法，它是一种有效处理上述问题的实用方法；

层次分析法的特点


综合定性与定量分析的方法，在对复杂的决策问题的本质、影响因素及其内在关系等进行深入分析的基础上，利用较少的定量信息使决策的思维过程数学化； 


适合解决多目标、多准则的复杂系统，特别是难以完全定量描述的复杂系统问题； 


思路清晰、方法简便、适用面广、系统性强、便于普及推广； 


在经济、科技、文化、军事、环境乃至社会发展等方面的管理决策中都有广泛的应用，常用来解决诸如综合评价、选择决策方案、估计和预测、投入量的分配等问题； 

层次分析法的基本思路


以购买电冰箱为例，首先，决策者对市场上的 6种不同型号的电冰箱进行了解后，选取7个中间标准进行考察，如：容量、制冷级别、价格、款式、耗电量、品牌信誉、售后服务等； 


然后，决策者考虑各种型号冰箱在上述各中间标准下的优劣排序；借助这种排序，最终作出选购决策； 


与人们对某一复杂决策问题的思维、判断过程大体一致，在决策时，由于6种电冰箱对于每个中间标准的优劣排序一般是不一致的，因此，决策者首先要对这7个标准的重要度做一个估计，给出一个排序，然后把6种冰箱分别对每一个标准的排序权重找出来，最后把这些信息数据综合，得到针对总目标即购买那种型号的电冰箱的排序权重。有了这个权重向量，决策就很容易了； 

层次分析法的基本步骤

clip_image006

1.    建立层次结构模型 

      一个复杂的无结构问题可分解为它的若干组成部分或因素， 例如，目标、约束、准则、子准则、方案等，按照属性的不同把这些因素分组形成互不相交的层次，上一层次的因素对相邻下一层次的全部或某些因素起着支配作用，形成按层次自上而下的逐层支配关系，具有这种性质的层次称为递阶层次；最高层：决策的目的、要解决的问题，最高层通常只有一个元素；


中间层：采取某种措施、方案等实现预定总目标所涉及的中间环节，一般可分为准则层、指标层、策略层、约束层等； 


最低层：决策时的备选措施、政策或方案，通常有几个方案可选； 


对于相邻的两层，称高层为目标层，低层为因素层；

       一个典型的层次结构模型可用下图表示： 

      clip_image008


若上层的每个因素都支配着下层的所有因素，或被下层所有因素所影响，则称为完全层次结构，否则，称为不完全层次结构；


层次数与问题的复杂程度和所需要分析的详尽程度有关；每一层次元素一般不超过9个（注：从心理学的角度看，一层中包含的元素过多会给两辆比较判断带来困难）；


一个好的层次结构对于问题的解决极为重要，好的层次结构建立在决策者对面临问题具有全面认识的基础之上；


层次分析法所要解决的问题是关于最低层对最高层的相对权重问题，按此相对权重可以对最低层中的各种方案、措施进行排序，从而做出最终决策；

 

2.    构造成对比较（判断）矩阵 

      在建立层次结构模型以后，上下层之间的隶属关系就确定了；假设上一层次元素clip_image010作为准则，对下一层元素clip_image012有支配关系，我们的目的是在准则clip_image010[1]之下按它们的相对重要性赋予相应的权重；在确定各层次各因素之间的权重时，如果只是定性的结果，往往不易令人信服，于是clip_image020等人提出构造成对比较矩阵clip_image016，clip_image018表示第i个元素相对于第j个元素的比较结果；成对比较矩阵不把所有的元素放在一起比较，而是两两相互比较，并且采用相对尺度，这样可以尽可能的减少性质不同的诸因素比较造成的困难，同时有利于提高准确性；

      成对比较矩阵的元素clip_image018[1]，可以采用clip_image020的clip_image022标度法给出：


1表示两元素相比，具有同样的重要性；


3表示两元素相比，一个元素比另一个元素稍微重要；


5表示两元素相比，一个元素比另一个元素明显重要；


7表示两元素相比，一个元素比另一个元素强烈重要；


9表示两元素相比，一个元素比另一个元素极端重要；


2，4，6，8表示上述两相邻判断的中值；

      由成对比较矩阵的定义可知，它具有如下性质：clip_image024，因此，clip_image026阶成对比较矩阵仅需要对其上（下）三角元素共clip_image028个进行判断即可；同时，满足以上性质的矩阵又称为正互反矩阵；

3.    层次单排序

      层次单排序的目的是确定下层各个因素对上层某因素的影响程度，它可以归结为求解成对比较矩阵的特征根和特征向量问题，即对成对比较矩阵clip_image030，计算满足clip_image032的特征根和特征向量，其中clip_image034为clip_image030[1]的最大特征根，clip_image036为对应的特征向量，即相应因素单排序的权值；

      常用的计算最大特征根和特征向量的方法——和法：


将成对比较矩阵中的每一列归一化：clip_image002；

clip_image004[1]


将每一列归一化后的矩阵按行相加：clip_image006[1]；

clip_image008[2]


将向量clip_image010[1]归一化：clip_image012[1]，所求得的clip_image014即为所求的特征向量；

clip_image016[1]


计算成对比较矩阵的最大特征根：clip_image018[1]，其中clip_image020[1]表示向量clip_image022[1]的第clip_image024[1]个元素；

clip_image026[1]

      常用的计算最大特征根和特征向量的方法——根法：


根法的具体步骤与和法基本相同，不同之处在于第二步中，和法为“按行相加”，而根法为“按行求积，并开clip_image028[1]次方”，即clip_image030[2]

      常用的计算最大特征根和特征向量的方法——幂法：


任取一个与判断矩阵同阶正规化的初值向量，例如取clip_image032[2]；

clip_image034[2]


计算clip_image036[2]

clip_image038[2]

clip_image040[3]


 clip_image042[1]归一化，即令clip_image044[1]

clip_image046[1]

clip_image048[1]


对于预先给定的精确度clip_image050[1]，如果clip_image052[1]，则clip_image054[1]为所求的特征向量，转入下一步，否则返回第二步；

clip_image056[1]，需要返回到第二步；

clip_image058[1]，转入下一步


计算最大特征值：clip_image060[1]

clip_image062[1]

4.    层次单排序的一致性检验

      在构造成对比较矩阵时，我们要求判断大体上具有一致性；如果出现甲比乙极端重要，乙比丙极端重要，而丙又比甲极端重要的情况是违反常识的，一个混乱的、经不起推敲的对比较矩阵有可能导致决策的失误，其结果的可能程度也值得怀疑；因此，必须对成对比较矩阵的一致性进行检验；

      在正互反矩阵clip_image030[2]中，若clip_image098， 即clip_image030[3]中的元素具有传递性，则称矩阵clip_image030[4]为一致阵，具有完全一致性；由于客观事物的复杂性和人类认识的片面性，要达到完全一致性非常困难；

一致性检验是根据矩阵理论来进行的，根据矩阵理论来进行的，根据矩阵理论有公式clip_image032[1]，当成对比较矩阵具有完全一致性时clip_image100，clip_image026[2]为clip_image030[5]的阶数；为了检验成对比较矩阵的一致性，需要计算一致性指标clip_image102；clip_image104的值越大，成对比较矩阵的不一致性越严重；clip_image104[1]的值越小，成对比较矩阵越接近于完全一致性；

      由于达到完全一致性比较困难，但是至少要达到满意一致性；什么是满意一致性呢？对于多阶成对比较矩阵，判断矩阵一致性指标clip_image104[2]与同阶平均随机一致性指标clip_image106之比称为随机一致性比率clip_image108，当clip_image110时，认为clip_image030[6]的不一致性程度在可接受的范围内，具有满意的一致性，通过一致性检验，否则，要重新构造成对比较矩阵clip_image030[7]，并对clip_image018[2]加以调整

注：平均随机一致性指标是多次（500次以上）重复进行随机判断矩阵特征根计算之后取算术平均得到的；袭木森、许树柏1986年得出的1-15阶判断矩阵重复计算1000次的平均随机一致性指标如下： 

image

5.    层次总排序及其一致性检验 

      层次总排序的目的是计算某一层次所有因素对于最高层（总目标）相对重要性的权值，这一过程是从最高层次到最低层次依次进行的；

      设clip_image030[8]层的clip_image114个因素clip_image116对总目标clip_image118的排序为clip_image120，clip_image122层的clip_image026[3]个因素对上层clip_image030[9]中因素clip_image124的层次单排序为clip_image126，则clip_image122[1]层的层次总排序为clip_image128（影响加和）；

      设clip_image122[2]层中的因素clip_image130对上层（clip_image030[10]层）中的因素clip_image132的层次单排序一致性指标为clip_image134，随机一致性指标为clip_image136，则层次总排序的一致性比率为clip_image138，当clip_image110[1]时，认为层次总排序通过一致性检验，具有满意的一致性，否则，要重新调整那些一致性比率高的判断矩阵的元素取值；

      至此，根据最下层（决策层）的层次总排序做出最后的决策；

层次分析法的优点和局限性

优点


层次分析法将研究对象作为一个系统，按照分解、比较判断、综合的思维方式进行决策， 成为继机理分析、统计分析之后发展起来的系统分析的重要工具；


层次分析法将定性和定量方法结合起来，能处理许多用传统的最优化技术无法着手的实际问题，应用范围很广，同时该方法使得决策者和决策分析者能够相互沟通，甚至决策者可以直接应用它，这就增加了决策的有效性；


层次分析方法的原理和步骤比较容易掌握，计算也非常简便，结果简单明确，容易被决策者了解和掌握；

局限性


只能从原有的方案中优选一个出来，没有办法得到更好的新方案；


定量数据较少，定性成份多，不易令人信服（可采用专家群体判断的方法克服这一缺点）；


指标过多时数据统计量大，且权重难以确认；


特征值和特征向量的精确求解算法比较复杂；