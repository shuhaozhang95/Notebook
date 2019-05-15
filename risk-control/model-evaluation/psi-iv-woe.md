# PSI, IV, WOE, KS, GINI, LIFT

**PSI 模型稳定度指标** （PSI一般作为一个衡量模型稳定性的指标）

一般在模型测试中，PSI&gt;0.2 我们认为模型不太稳定。

稳定度指标\(population stability index ,PSI\)可衡量测试样本及模型开发样本评分的的分布差异，为最常见的模型稳定度评估指针。其实PSI表示的就是按分数分档后，针对不同样本，或者不同时间的样本，population分布是否有变化，就是看各个分数区间内人数占总人数的占比是否有显著变化。

![](../../.gitbook/assets/image%20%2854%29.png)

**PSI实际应用范例：**

1）样本外测试

针对不同的样本测试一下模型稳定度，比如训练集与测试集，也能看出模型的训练情况，我理解是看出模型的方差情况。

2）时间外测试

测试基准日与建模基准日相隔越远，测试样本的风险特征和建模样本的差异可能就越大，因此PSI值通常较高。至此也可以看出模型建的时间太长了，是不是需要重新用新样本建模了。

PSI与KL divergence的关系：（其实PSI也是一种描述分布差异的指标）

$$
\begin{aligned}
\sum_{10}^{i-1}(A_{i}-E_{i})* \log(A_{i}/E_{i}) 
&= \sum_{10}^{i-1}(A_{i} * \log(A_{i}/E_{i})+ E_{i}*\log(E_{i}/A_{i}))\\
&=\sum_{10}^{i-1}(A_{*}*\log(A_{i}/E_{i}))+\sum_{10}^{i-1}E_{i}*\log(E_{i}/A_{i})
\end{aligned}
$$

根据以上公式我们可以发现PSI其实是（实际分布与预期分布的KL）+（预期分布与实际分布的KL）

可以理解成是A和E的KL散度的对称化处理。

**WOE \(Weight of Evidence\) 证据权重**

要对一个变量进行WOE编码，需要对这个变量进行分组处理\(离散化，分箱\)。

分组后，对于第i组的WOE计算公式为：

![img](https://img-blog.csdn.net/20160302153928222)

其中，

Pyi是第i组中响应客户（风险模型中的违约客户）占所有样本中所有响应客户（违约用户）的比例。

Pni是第i组中未响应客户（未违约客户）占所有未响应客户（未违约客户）的比例。

经过简单变换，

![img](https://img-blog.csdn.net/20160302154019081)

我们也可以理解成，WOE表示的是这个组的违约用户与非违约用户的比例 与 所有样本中该比值的差异。

所以呢，WOE越大，表示这种差异越大，那么这个分组里的样本响应的可能性就越大。

_延伸：_

为什么可以WOE？

一般我们对变量离散化以后都会做WOE。或者类别变量Dummy化。

主要原因是我们很难知道离散后的变量各组之间的数量关系。

WOE可以解决组与组之间数量值未知的关系。主要与逻辑回归有关。

![img](https://pic1.zhimg.com/80/v2-f238f0ac063dcff201ee0acb57fb037c_hd.jpg)

我们把逻辑回归右边的变量X WOE化处理，是因为左边需要拟合的就是这种形式，这种处理可以衡量组与组之间的数量关系。所以也可以说明，WOE化一般是不能用在其他算法上的（不包括树模型）。

WOE的好处？

1. 容易解释
2. 变量变少了，容易调整
3. 可以区分哪些组是负向的，哪些是正向的

**IV （Information Value）信息量**

IV表示一个变量的预测能力，可以用来挑选变量。尽可能的挑选IV大的变量。

$$
IV_{i} = (P_{y_{i}}-P_{n_{i}}) * WOE_{i}
$$

最后IV即是各分组的IV相加：

$$
IV = \sum^{n}_{i}IV_{i}
$$

**模型区分度指标（KS，GINI）**

KS（Kolmogorov-Smirnov）用于模型风险区分能力进行评估，是用于区分正负样本分隔程度的评价指标

KS的取值范围是\[0,1\]，通常来说，KS的值越大，表明正负样本的区分程度越好。但并非越高越好。

征信模型中，最期望得到的信用分数分布是正态分布。对于正负样本而言，也都是期望正态分布。如果KS过大超过0.9，则认为正负样本分的过开，是极端的分布情况。

PS：_KS所代表的是模型的分隔能力，并不代表分隔的样本是准确的。正负样本完全分错，KS值也可能很高。_

KS的计算方法与ROC相似。

1. 根据模型的输出概率，从大到小排列
2. 比如说设置10%的阈值，计算出不同的TPR = TP/\(TP+FN\) , FPR=FP/\(FP+FN\)
3. 我们以每10%（也可以是别的阈值）为横坐标，TPR和FPR为纵坐标，可以得到两条K-S曲线。那么KS值就是K-S曲线中两条曲线之间的最大间隔距离。KS = max\(TPR-FPR\)

   ![&#xE8;&#xBF;&#x99;&#xE9;&#x87;&#x8C;&#xE5;&#x86;&#x99;&#xE5;&#x9B;&#xBE;&#xE7;&#x89;&#x87;&#xE6;&#x8F;&#x8F;&#xE8;&#xBF;&#xB0;](https://img-blog.csdn.net/20171012171557401?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzQyMTYyOQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

**风控情景下的GINI系数**

1. 计算每个评分区间的好坏账户数
2. 计算每个评分区间的（累计好账户数/总好账户数）的比率（good%）以及 （累计坏账户数/总坏帐户数）的比率（bad%）
3. 计算好账户占比和坏帐户占比得出下图的曲线。即绘制一条（good%/bad%）的曲线。
4. 计算出图中阴影部分的面积，阴影面积占直角三角形的ABC的面积的百分比，就是GINI系数。

![&#xE8;&#xBF;&#x99;&#xE9;&#x87;&#x8C;&#xE5;&#x86;&#x99;&#xE5;&#x9B;&#xBE;&#xE7;&#x89;&#x87;&#xE6;&#x8F;&#x8F;&#xE8;&#xBF;&#xB0;](https://img-blog.csdn.net/20171012171836445?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzQyMTYyOQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

**累计提升曲线LIFT**

LIFT曲线衡量的是，与不利模型相比，模型的预测能力“变好”了多少，LIFT（提升指数）越大，模型的运行效果越好。实际上它强调的是投入与产出比。

$$
LIFT = \frac{\frac{TP}{TP+FP}}{\frac{TP+FN}{TP+FP+TN+FN}} = \frac{PRE}{正例占比}
$$

PRE为正确率。

$$
PRE =\frac{TP}{TP+FP}
$$

**Lift指标可以这样理解：**在不使用模型的情况下，我们用先验概率估计正例的比例，即上式子分母部分，以此作为正例的命中率；利用模型后，我们不需要从整个样本中来挑选正例，只需要从我们预测为正例的那个样本的子集 ![TP+FP](https://www.zhihu.com/equation?tex=TP%2BFP) 中挑选正例，这时正例的命中率为 ![PRE](https://www.zhihu.com/equation?tex=PRE) ，后者除以前者即可得提升值**Lift。**

LIFT曲线

先引入depth的概念。

$$
depth = \frac{TP+FP}{TP+FP+TN+FN}
$$

所以depth代表的是预测为正例的样本占整个样本的比例

一般要求，在尽量大的 ![depth](https://www.zhihu.com/equation?tex=depth) 下得到尽量大的 ![Lift](https://www.zhihu.com/equation?tex=Lift)，所以 ![Lift](https://www.zhihu.com/equation?tex=Lift) 曲线的右半部分应该尽量陡峭。

