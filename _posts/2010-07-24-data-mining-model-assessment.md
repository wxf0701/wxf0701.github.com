--- 
layout: post
title: 数据挖掘模型的评估
tags: 
- "机器学习"
- "效果评估"
status: publish
type: post
published: true
---
当构建好数据挖掘模型时，并不能保证模型能直接解决业务问题，我们要对挖掘模型进行评估，以确保对模型的实际数据执行情况能够达到可接受的程度。可以使用多种方法评估分类挖掘模型的性能：
<ul>
	<li>使用统计信息有效性的各种度量值来确定数据或模型中是否存在问题</li>
	<li>将数据划分训练集和测试集，以测试预测的准确性</li>
	<li>请商业专家查看数据挖掘模型的结果，以确定发现的模式在目标商业方案中是否有意义</li>
</ul>
这些方法在数据挖掘中都非常有用，在构建、优化和测试模型来解决特定问题时可以反复使用这些方法。

# 挖掘模型评估的三个方面 #
通常，对挖掘模型的评估包括三个方面：准确性、可靠性和有用性
<ul>
	<li>准确性：挖掘模型与所提供数据中的属性的相关联程度。</li>
	<li>可靠性：当提供不同的测试数据时，挖掘模型表现出稳定预测结果的能力。</li>
	<li>有用性：模型是否提供了有用信息的各种指标。比如有些挖掘模型在数据上表现完美，但对业务优化却毫无指导意义。</li>
</ul>

# 评估准确性——混淆矩阵（Confusion Matrix） #
混淆矩阵（Confusion Matrix）或分类矩阵（Classification Matrix）是快速评估分类模型的预测能力的工具。矩阵的行表示实际值，而列则表示模型的预测值。分类矩阵的每一个网格表示预测结果每个类别的计数及其合计。
<table border = '1' cellspacing='0'>
	<tr> 
		<td> </td>
		<td><strong>预测为负</strong></td>
		<td><strong>预测为正</strong></td>
		<td><strong>合计</strong></td>
	</tr>
	<tr>
		<td><strong>实际为负</strong> </td>
		<td align="center">A</td>
		<td align="center">B</td>
		<td align="center">A+B</td>
	</tr>
	<tr>
		<td><strong>实际为正</strong> </td>
		<td align="center">C</td>
		<td align="center">D</td>
		<td align="center">C+D</td>
	</tr>
	<tr>
		<td><strong>合计</strong> </td>
		<td align="center">A+C</td>
		<td align="center">B+D</td>
		<td align="center">A+B+C+D</td>
	</tr>
</table>

</br>
<ul>
	<li>A：实际为负，预测为负</li>
	<li>B：实际为负，预测为正</li>
	<li>C：实际为正，预测为负</li>
	<li>D：实际为正，预测为正</li>
	<li>A+B：实际为负</li>
	<li>C+D：实际为正</li>
	<li>A+C：预测为负</li>
	<li>B+D：预测为正</li>
	<li>A+B+C+D：样本总量</li>
</ul>

</br>
根据上表，从总体上看，有
<ul>
	<li>正确分类率=（实际为负且预测为负+实际为正且预测为正）/样本总量=(A+D)/(A+B+C+D) </li>
	<li>错误分类率=（实际为负且预测为正+实际为正且预测为负）/样本总量=(B+C)/(A+B+C+D)=1-正确分类率 </li>
</ul>

</br>
假设我们只关注“正”样本的预测情况，则有
<ul>
	<li>查全率recall=（预测为正，实际为正）/实际为正=D/(C+D) </li>
	<li>查准率precision=（预测为正，实际为正）/预测为正=D/(B+D) </li>
</ul>

更多参考：
<a href="http://en.wikipedia.org/wiki/Confusion_matrix" target="_blank">http://en.wikipedia.org/wiki/Confusion_matrix</a>

# 评估可靠性——K-折交叉验证（K-Fold Cross Validation） #
<ul>
	<li>第一步：K-折交叉验证将初始数据集被随机分为k（k>2）个互不相交的子集:S(1)、S(2)……S(k)。每个子集大小基本相同，子集中各类别的分布与初始数据集中的类别分布基本相同。 </li>
	<li>第二步：学习和测试分别进行k次。在第i次循环中，子集S(i)作为测试集，其它子集则合并到一起构成一个大训练数据集并通过学习获得相应的分类模型。这样，每一个数据参与测试1次，参与训练k-1次。 </li>
	<li>第三步：为每个模型生成一组标准准确性指标。 </li>
	<li>第四步：对整个初始数据集所得挖掘模型准确率精度的估计则可用k次循环中所获得的正确分类数目之和除以初始数据集的大小来获得。 </li>
	<li>第五步：通过比较为每个交叉部分生成的模型的指标，可以清楚地了解挖掘模型对于整个数据集的可靠程度。 </li>
</ul>

</br>
注：保持(Hold-Out)法和弃一交叉验证(Leave-One-Out)法是K-折交叉验证法相关的两个极端。
<ul>
	<li>保持(Hold-Out)法将样本集分为训练集和测试集两部分，通常训练集包括初始数据集三分之二的数据，而剩余的三分之一作为测试集，该方法与初始数据集的划分有密切关系，因此不适合用来验证模型的可靠性。 </li>
	<li>弃一(Leave-One-Out)交叉验证则将N-1个样本作为训练集（N为初始数据集的样本总量），剩下1个样本作为预测集。循环Ｎ次，使得每个样本都作为一次预测集，然后计算交叉验证的正确率，该方法的缺点是需要大量的计算。 </li>
</ul>

更多参考：
<a href="http://en.wikipedia.org/wiki/Cross-validation_(statistics)" target="_blank">http://en.wikipedia.org/wiki/Cross-validation_(statistics)</a>
<a href="http://www.cs.cmu.edu/~schneide/tut5/node42.html" target="_blank">http://www.cs.cmu.edu/~schneide/tut5/node42.html</a>

# 评估应用效果——提升（Lift）图 #

如果开展一次营销活动，根据以往的活动推算应有10%的响应率。在数据库中存储了10000名潜在客户。因此，按照正常答复率计算，预计将有 1000 名潜在客户响应营销活动。
但是，该项目的预算可能不足以向所有的10000名客户进行营销。因为预算只能承担向5000名客户的营销。业务部门有下列两种选择：
<ul>
	<li>随机选择 5000 名目标客户</li>
	<li>使用挖掘模型确定最有可能响应的5000名目标客户</li>
</ul>

</br>
如果随机选择5000名客户，按照正常答复率计算，估计只能收到500个答复。这正是提升图中的“随机线“所表示的情况。而如果使用挖掘模型来确定营销目标，则预计可以获得更高的答复率，因为他们锁定了最有可能答复的客户。这正是提升图中的“理想线”所表示的情况。
提升图是如何得到呢？
<ul>
	<li>“实际为正”率＝(C+D)/(A+B+C+D) </li>
	<li>LIFT=查准率/“实际为正”率＝(D/B+D)/(C+D/A+B+C+D) </li>
</ul>
