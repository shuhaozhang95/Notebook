# Scored Card Model

按照借贷用户的借贷时间，评分卡模型可以划分为以下三种：

* 贷前：申请评分卡（Application score card），又称为A卡
* 贷中：行为评分卡（Behavior score card），又称为B卡
* 贷后：催收评分卡（Collection score card），又称为C卡

一个用户总的评分等于基准分加上对客户各个属性的评分。

评分卡模型的大致结构：

![img](https://pic4.zhimg.com/80/v2-db979466aa6abc3f74b917b21b88a76f_hd.jpg)

分箱的定义：

* 对连续变量进行分段离散化；
* 将多状态的离散变量进行合并，减少离散变量的状态数。

变量分箱的方法：

![img](https://pic4.zhimg.com/80/v2-31cba8dc3a08bf93a79f0c1c24291c37_hd.jpg)

**1. 无监督分箱**

无监督的分箱主要包括以下几类：

\(1\) 等频分箱：把自变量按从小到大的顺序排列，根据自变量的个数等分为k部分，每部分作为一个分箱。

\(2\) 等距分箱：把自变量按从小到大的顺序排列，将自变量的取值范围分为k个等距的区间，每个区间作为一个分箱。

\(3\) 聚类分箱：用k-means聚类法将自变量聚为k类，但在聚类过程中需要保证分箱的有序性。

由于无监督分箱仅仅考虑了各个变量自身的数据结构，并没有考虑自变量与目标变量之间的关系，因此无监督分箱不一定会带来模型性能的提升。

**2. 有监督分箱**

包括 Split 分箱和 Merge 分箱

1. Split 分箱是一种自上而下\(即基于分裂\)的数据分段方法。如下图所示，Split 分箱和决策树比较相似，切分点的选择指标主要有 entropy，gini 指数和 IV 值等。
2. Merge 分箱，是一种自底向上\(即基于合并\)的数据离散化方法。如下图所示为Merge 分箱的示意图，Merge 分箱常见的类型为Chimerge分箱。
3. Chimerge 分箱是目前最流行的分箱方式之一，其基本思想是如果两个相邻的区间具有类似的类分布，则这两个区间合并；否则，它们应保持分开。Chimerge通常采用卡方值来衡量两相邻区间的类分布情况。

Chimerge的具体算法如下：

1. 输入：分箱的最大区间数 ![n](https://www.zhihu.com/equation?tex=n)
2. 初始化
3. 连续值按升序排列，离散值先转化为坏客户的比率，然后再按升序排列；
4. 为了减少计算量，对于状态数大于某一阈值 \(建议为100\) 的变量，利用等频分箱进行粗分箱。
5. 若有缺失值，则缺失值单独作为一个分箱。
6. 合并区间
7. 计算每一对相邻区间的卡方值；
8. 将卡方值最小的一对区间合并

![X^2 = \sum\_{i=1}^2 \sum\_{j=1}^2\frac{\(A\_{ij} - E\_{ij}\)^2}{E\_{ij}} \\](https://www.zhihu.com/equation?tex=X^2+%3D+\sum_{i%3D1}^2+\sum_{j%3D1}^2\frac{%28A_{ij}+-+E_{ij}%29^2}{E_{ij}}+\\) ![A\_{ij}](https://www.zhihu.com/equation?tex=A_{ij})：第 i 区间第 j 类的实例数量 ![E\_{ij}](https://www.zhihu.com/equation?tex=E_{ij}) ： ![E\_{ij} = \frac{N\_i }{N}\times C\_j](https://www.zhihu.com/equation?tex=E_{ij}+%3D+\frac{N_i+}{N}\times+C_j) ， ![N](https://www.zhihu.com/equation?tex=N) 是合并区间的样本数， ![N\_i](https://www.zhihu.com/equation?tex=N_i) 是第 ![i](https://www.zhihu.com/equation?tex=i) 组的样本数， ![C\_j](https://www.zhihu.com/equation?tex=C_j) 是第 ![j](https://www.zhihu.com/equation?tex=j) 类样本在合并区间的样本数。

* 重复以上两个步骤，直到分箱数量不大于 ![n](https://www.zhihu.com/equation?tex=n)

单变量的筛选基于变量预测能力，常用方法：

* **基于IV值的变量筛选**
* **基于stepwise的变量筛选**
* **基于特征重要度的变量筛选：RF, GBDT…**
* **基于LASSO正则化的变量筛选**

变量相关性分析

**1 变量两两相关性分析**

对于自变量 ![X\_1, X\_2](https://www.zhihu.com/equation?tex=X_1%2C+X_2)，如果存在常数 ![c\_0,c\_1,c\_2](https://www.zhihu.com/equation?tex=c_0%2Cc_1%2Cc_2) 使得以下线性等式近似成立: ![c\_1X\_1 + c\_2X\_2 \approx c\_0 \\](https://www.zhihu.com/equation?tex=c_1X_1+%2B+c_2X_2+\approx+c_0+\\) 称自变量 ![X\_1, X\_2](https://www.zhihu.com/equation?tex=X_1%2C+X_2) 具有较强的线性相关性。

两变量间的线性相关性可以利用皮尔森相关系数来衡量。系数的取值为 ![\[-1.0,1.0\]](https://www.zhihu.com/equation?tex=[-1.0%2C1.0]) ，相关系数越接近0的说明两变量线性相关性越弱，越接近1或-1两变量线性相关性越强。 ![r\_{X,Y}=\frac{cov\(X,Y\)}{\sigma\_X\sigma\_Y}=\frac{E\(\(X-\bar X\)\(Y-\bar Y\)\)}{\sqrt{\sum\limits\_{i=1}^n\(X\_i-\bar X\)^2} \sqrt{ \sum\limits\_{i=1}^n\(Y\_i-\bar Y\)^2}} = \frac{E\(XY\)-E\(X\)\(Y\)}{\sqrt{E\(X^2\)-E^2\(X\)}\sqrt{E\(Y^2\)-E^2\(Y\)}} \\](https://www.zhihu.com/equation?tex=r_{X%2CY}%3D\frac{cov%28X%2CY%29}{\sigma_X\sigma_Y}%3D\frac{E%28%28X-\bar+X%29%28Y-\bar+Y%29%29}{\sqrt{\sum\limits_{i%3D1}^n%28X_i-\bar+X%29^2}+\sqrt{+\sum\limits_{i%3D1}^n%28Y_i-\bar+Y%29^2}}+%3D+\frac{E%28XY%29-E%28X%29%28Y%29}{\sqrt{E%28X^2%29-E^2%28X%29}\sqrt{E%28Y^2%29-E^2%28Y%29}}+\\) 当两变量间的相关系数大于阈值时（一般阈值设为 0.7 或 0.4），剔除IV值较低的变量，或分箱严重不均衡的变量。

**2 变量的多重共线性分析**

对于自变量 ![X\_1, X\_2, \cdots , X\_n](https://www.zhihu.com/equation?tex=X_1%2C+X_2%2C+\cdots+%2C+X_n) ，如果存在常数 ![c\_0,c\_1,c\_2, \cdots, c\_n](https://www.zhihu.com/equation?tex=c_0%2Cc_1%2Cc_2%2C+\cdots%2C+c_n) 使得以下线性等式近似成立: ![c\_1X\_1 + c\_2X\_2 + \cdots + c\_nX\_n \approx c\_0 \\](https://www.zhihu.com/equation?tex=c_1X_1+%2B+c_2X_2+%2B+\cdots+%2B+c_nX_n+\approx+c_0+\\) 称自变量 ![X\_1, X\_2, \cdots , X\_n](https://www.zhihu.com/equation?tex=X_1%2C+X_2%2C+\cdots+%2C+X_n)具有较强的多重共线性。

通常用 VIF 值来衡量一个变量和其他变量的多重共线性： ![VIF\_i = \frac{1}{1-R^2\_i} \\](https://www.zhihu.com/equation?tex=VIF_i+%3D+\frac{1}{1-R^2_i}+\\) 其中 ![R\_i](https://www.zhihu.com/equation?tex=R_i) 为 ![X\_i](https://www.zhihu.com/equation?tex=X_i) 与其他自变量的复相关系数。 ![R\_i = \frac {\sum{\(X\_i-\bar X\_i\)\(\hat X\_i - \bar X\_i\)}} {\sqrt {\sum{\(X\_i-\bar X\_i\)^2}\sum{\(\hat X\_i-\bar X\_i\)^2}}} \\](https://www.zhihu.com/equation?tex=R_i+%3D+\frac+{\sum{%28X_i-\bar+X_i%29%28\hat+X_i+-+\bar+X_i%29}}+{\sqrt+{\sum{%28X_i-\bar+X_i%29^2}\sum{%28\hat+X_i-\bar+X_i%29^2}}}+\\) 其中： ![\hat X\_i](https://www.zhihu.com/equation?tex=\hat+X_i) 为其他变量的线性表示![\hat X\_i = \theta\_0+\theta\_1X\_1+\cdots +\theta\_{i-1}X\_{i-1}+\theta\_{i+1}X\_{i+1}+\cdots](https://www.zhihu.com/equation?tex=\hat+X_i+%3D+\theta_0%2B\theta_1X_1%2B\cdots+%2B\theta_{i-1}X_{i-1}%2B\theta_{i%2B1}X_{i%2B1}%2B\cdots)

![\bar X\_i](https://www.zhihu.com/equation?tex=\bar+X_i) 为变量 ![X\_i](https://www.zhihu.com/equation?tex=X_i) 的均值

当某个变量的 VIF 大于阈值时（一般阈值设为10 或 7），需要逐一剔除解释变量。当剔除掉 ![X\_k](https://www.zhihu.com/equation?tex=X_k)时发现VIF低于阈值，从 ![{X\_k&#xFF0C;X\_i}](https://www.zhihu.com/equation?tex={X_k，X_i}) 中剔除IV值较低的一个。

## 转化为评分卡

我们将客户违约的概率表示为p，则正常的概率为1-p。由逻辑回归的基本原理可得： ![p= \frac{1}{1 + e^{-\theta^Tx}} \\](https://www.zhihu.com/equation?tex=p%3D+\frac{1}{1+%2B+e^{-\theta^Tx}}+\\) 整理以上公式： ![\text{log}\(\frac{p}{1-p}\) = \theta^Tx \\](https://www.zhihu.com/equation?tex=\text{log}%28\frac{p}{1-p}%29+%3D+\theta^Tx+\\) 我们可以定义比率来表示客户违约的相对概率： ![\text{odds} = \frac{p}{1-p} \\](https://www.zhihu.com/equation?tex=\text{odds}+%3D+\frac{p}{1-p}+\\) 将 ![\text{odds}](https://www.zhihu.com/equation?tex=\text{odds}) 带入可得： ![\text{log}\( \text{odds}\) = \theta^Tx \\](https://www.zhihu.com/equation?tex=\text{log}%28+\text{odds}%29+%3D+\theta^Tx+\\) 评分卡的分值可以定义为比率对数的线性表达来，即： ![Score = A -B \times \text{log}\( \text{odds}\) \\](https://www.zhihu.com/equation?tex=Score+%3D+A+-B+\times+\text{log}%28+\text{odds}%29+\\) 其中A与B是常数，B前面的负号可以使得违约概率越低，得分越高。通常情况下，即高分值代表低风险，低分值代表高风险。

A、B的值可以通过将两个已知或假设的分值带入计算得到。通常情况下，需要设定两个假设：

* 某个特定的违约概率下的预期评分，即比率 ![\text{odds}](https://www.zhihu.com/equation?tex=\text{odds}) 为![&#x3B8;\_0](https://www.zhihu.com/equation?tex=θ_0)时的分数为 ![P\_0](https://www.zhihu.com/equation?tex=P_0)
* 该违约概率翻倍的评分（PDO）

根据以上的分析，则 ![\text{odds}](https://www.zhihu.com/equation?tex=\text{odds}) 为 ![2&#x3B8;\_0](https://www.zhihu.com/equation?tex=2θ_0) 时的分数为 ![P\_0-PDO](https://www.zhihu.com/equation?tex=P_0-PDO) ，代入以上线性表达式，可得： ![P\_0 = A-B\times \text{log}\(\theta\_0\) \ P\_0 - PDO = A-B\times \text{log}\(2\theta\_0\) \\](https://www.zhihu.com/equation?tex=P_0+%3D+A-B\times+\text{log}%28\theta_0%29+\+P_0+-+PDO+%3D+A-B\times+\text{log}%282\theta_0%29+\\) 解该方程组，可得： ![B = \frac{PDO}{ \text{log}2} \ A = P\_0 + B\* \text{log}\(\theta\_0\) \\](https://www.zhihu.com/equation?tex=B+%3D+\frac{PDO}{+\text{log}2}+\+A+%3D+P_0+%2B+B*+\text{log}%28\theta_0%29+\\) 在实际的应用中，我们会计算出每个变量的各分箱对应的分值。新用户产生时，对应到每个分箱的值，将这些值相加，最后加上初始基础分，得到最终的结果。 ![Score= A-B\{\theta\_0 + \theta\_1x\_1+\cdots+\theta\_nx\_n \} \\](https://www.zhihu.com/equation?tex=Score%3D+A-B\{\theta_0+%2B+\theta_1x_1%2B\cdots%2B\theta_nx_n+\}+\\) 式中：变量 ![x\_1&#x2026;x\_n](https://www.zhihu.com/equation?tex=x_1…x_n) 是出现在最终模型的入模变量。由于所有的入模变量都进行了WOE编码，可以将这些自变量中的每一个都写 ![\(\theta\_i w\_{ij} \) \delta\_{ij}](https://www.zhihu.com/equation?tex=%28\theta_i+w_{ij}+%29+\delta_{ij})的形式： ![Score= A- B\left\{ \begin{array}{ccc} \theta\_0\ +\(\theta\_1w\_{11}\)\delta\_{11}+\(\theta\_1w\_{12}\)\delta\_{12}+\cdots\ \cdots \+\(\theta\_nw\_{n1}\)\delta\_{n1}+\(\theta\_nw\_{n2}\)\delta\_{n2}+\cdots\end{array} \right\}](https://www.zhihu.com/equation?tex=Score%3D+A-+B\left\{+\begin{array}{ccc}+\theta_0\+%2B%28\theta_1w_{11}%29\delta_{11}%2B%28\theta_1w_{12}%29\delta_{12}%2B\cdots\+\cdots+\\%2B%28\theta_nw_{n1}%29\delta_{n1}%2B%28\theta_nw_{n2}%29\delta_{n2}%2B\cdots\end{array}+\right\}) 其中，![A-B&#x3B8;\_0](https://www.zhihu.com/equation?tex=A-Bθ_0) 为基础分数，![&#x3B8;\_i](https://www.zhihu.com/equation?tex=θ_i) 为逻辑回归中第 ![i](https://www.zhihu.com/equation?tex=i) 个自变量的系数， ![w\_{ij}](https://www.zhihu.com/equation?tex=w_{ij}) 为第 ![i](https://www.zhihu.com/equation?tex=i) 个变量的第 ![j](https://www.zhihu.com/equation?tex=j) 个分箱的WOE值， ![&#x3B4;\_{ij}](https://www.zhihu.com/equation?tex=δ_{ij}) 是0，1逻辑变量，当 ![&#x3B4;\_{ij} = 1](https://www.zhihu.com/equation?tex=δ_{ij}+%3D+1) 代表自变量 ![i](https://www.zhihu.com/equation?tex=i) 取第 ![j](https://www.zhihu.com/equation?tex=j) 个分箱，当 ![&#x3B4;\_{ij} = 0](https://www.zhihu.com/equation?tex=δ_{ij}+%3D+0) 代表自变量 ![i](https://www.zhihu.com/equation?tex=i) 不取第 ![j](https://www.zhihu.com/equation?tex=j) 个分箱。

最终得到评分卡模型：

![img](https://pic2.zhimg.com/80/v2-fec98ff9de65d835a5be217f01f678a5_hd.jpg)

从以上公式中，我们发现每个分箱的评分都可以表示为 ![-B\(\theta\_i w\_{ij} \) ](https://www.zhihu.com/equation?tex=-B%28\theta_i+w_{ij}+%29+) ，也就是说影响每个分箱的因素包括三部分，分别为参数 ![B](https://www.zhihu.com/equation?tex=B) ，变量系数 ![\theta\_i](https://www.zhihu.com/equation?tex=\theta_i) ，和对应分箱的WOE编码 ![w\_{ij}](https://www.zhihu.com/equation?tex=w_{ij}) 。

