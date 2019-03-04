# Linear/ Logistic Regression

**Linear Regression:**

**y**是一列有n个观测值的观测变量，或者直接说因变量以便于理解，

**X**是由多列特征组成的特征空间，假设有p列特征，简单理解就是有p个自变量，每个特征都有n个值，这与y是对应的：

![y=\left\( \begin{array}{ccc} y\_1 \\ y\_2 \\ \vdots \\ y\_n\\ \end{array} \right\) \quad,\quad X= \left\( \begin{array}{ccc} X\_1^T \\ X\_2^T \\ \vdots\\ X\_n^T \\ \end{array} \right\) = \left\( \begin{array}{ccc} 1 &amp; x\_{11} &amp; \cdots &amp; x\_{1p}\\ 1 &amp; x\_{21} &amp; \cdots &amp; x\_{2p}\\ \vdots &amp; \vdots &amp; \ddots &amp; \vdots\\ 1 &amp; x\_{n1} &amp; \cdots &amp; x\_{np}\\ \end{array} \right\)\\](https://www.zhihu.com/equation?tex=y%3D%5Cleft%28+%5Cbegin%7Barray%7D%7Bccc%7D+y_1+%5C%5C+y_2+%5C%5C+%5Cvdots+%5C%5C+y_n%5C%5C+%5Cend%7Barray%7D+%5Cright%29+%5Cquad%2C%5Cquad+X%3D+%5Cleft%28+%5Cbegin%7Barray%7D%7Bccc%7D+X_1%5ET+%5C%5C+X_2%5ET+%5C%5C+%5Cvdots%5C%5C+X_n%5ET+%5C%5C+%5Cend%7Barray%7D+%5Cright%29+%3D+%5Cleft%28+%5Cbegin%7Barray%7D%7Bccc%7D+1+%26+x_%7B11%7D+%26+%5Ccdots+%26+x_%7B1p%7D%5C%5C+1+%26+x_%7B21%7D+%26+%5Ccdots+%26+x_%7B2p%7D%5C%5C+%5Cvdots+%26+%5Cvdots+%26+%5Cddots+%26+%5Cvdots%5C%5C+1+%26+x_%7Bn1%7D+%26+%5Ccdots+%26+x_%7Bnp%7D%5C%5C+%5Cend%7Barray%7D+%5Cright%29%5C%5C)

**β**是系数向量，**ε**是干扰项（disturbance term），或称错误项（error term）：

![&#x3B2;=\left\( \begin{array}{ccc} &#x3B2;\_0 \\ &#x3B2;\_1\\&#x3B2;\_2 \\ \vdots \\ &#x3B2;\_p\\ \end{array} \right\)\quad,\quad &#x3B5;=\left\( \begin{array}{ccc} &#x3B5;\_1 \\ &#x3B5;\_2 \\ \vdots \\ &#x3B5;\_n\\ \end{array} \right\)\\](https://www.zhihu.com/equation?tex=%CE%B2%3D%5Cleft%28+%5Cbegin%7Barray%7D%7Bccc%7D+%CE%B2_0+%5C%5C+%CE%B2_1%5C%5C%CE%B2_2+%5C%5C+%5Cvdots+%5C%5C+%CE%B2_p%5C%5C+%5Cend%7Barray%7D+%5Cright%29%5Cquad%2C%5Cquad+%CE%B5%3D%5Cleft%28+%5Cbegin%7Barray%7D%7Bccc%7D+%CE%B5_1+%5C%5C+%CE%B5_2+%5C%5C+%5Cvdots+%5C%5C+%CE%B5_n%5C%5C+%5Cend%7Barray%7D+%5Cright%29%5C%5C)

最后我们得到的第i个y（观测值）是这样的：

![y\_i=&#x3B2;\_01+&#x3B2;\_1x\_{i1}+\cdots+&#x3B2;\_px\_{ip}+&#x3B5;\_i \(i=1,\cdots,n,&#x3B2;\_0&#x4E3A;&#x622A;&#x8DDD;\)\\](https://www.zhihu.com/equation?tex=y_i%3D%CE%B2_01%2B%CE%B2_1x_%7Bi1%7D%2B%5Ccdots%2B%CE%B2_px_%7Bip%7D%2B%CE%B5_i+%28i%3D1%2C%5Ccdots%2Cn%2C%CE%B2_0%E4%B8%BA%E6%88%AA%E8%B7%9D%29%5C%5C)

**所以，线性回归的公式是这样子的：**

![y=X&#x3B2;+&#x3B5; \\](https://www.zhihu.com/equation?tex=y%3DX%CE%B2%2B%CE%B5+%5C%5C)

前面说过，线性回归的过程就是要**找到最优的模型来描述数据**。这里就产生了两个问题：

* 如何定义“最优”？
* 如何寻找“最优”？

想要评价一个模型的优良，就需要一个**度量标准**。对于回归问题，最常用的度量标准就是[**均方差（MSE，Mean Squared Error）**](http://link.zhihu.com/?target=https%3A//en.wikipedia.org/wiki/Mean_squared_error)，均方差是指预测值和实际值之间的平均方差。平均方差越小，说明测试值和实际值之间的差距越小，即模型性能更优。

在线性回归的式子中y和X是给定的，而β和ε是不确定的，也就是说，**找到最优的β和ε，就找到了最优的模型**。

综合以上结论，可以用如下式子描述：

![\(&#x3B2;^\*,&#x3B5;^\*\)=argmin \sum\_{i=1}^m\(f\(x\_i\)-y\_i\)^2 \\](https://www.zhihu.com/equation?tex=%28%CE%B2%5E%2A%2C%CE%B5%5E%2A%29%3Dargmin+%5Csum_%7Bi%3D1%7D%5Em%28f%28x_i%29-y_i%29%5E2+%5C%5C)

其中， ![&#x3B2;^\*](https://www.zhihu.com/equation?tex=%CE%B2%5E%2A) 和 ![&#x3B5;^\*](https://www.zhihu.com/equation?tex=%CE%B5%5E%2A) 是要求的最优参数，右部是最小化均方差。

明确了我们的目标，接下来就是该如何去寻找这两个量呢？最常用的是参数估计方法是[**最小二乘法（Least Square Method）**](http://link.zhihu.com/?target=https%3A//zh.wikipedia.org/wiki/%25E6%259C%2580%25E5%25B0%258F%25E4%25BA%258C%25E4%25B9%2598%25E6%25B3%2595), 最小二乘法试图找到一条直线，使得样本点和直线的[欧氏距离](http://link.zhihu.com/?target=https%3A//zh.wikipedia.org/zh-hans/%25E6%25AC%25A7%25E5%2587%25A0%25E9%2587%258C%25E5%25BE%2597%25E8%25B7%259D%25E7%25A6%25BB)之和最小。这个寻找的过程简单描述就是：根据凸函数的性质，求其关于β和ε的二阶导的零点。

对于large scale data，我们也可以采用Gradient Descent的方法来进行优化。

**Logistic Regression:**

逻辑回归 即在 线性回归的基础上 加入了一个 link function。或者说是套了一个非线性变换，Sigmoid函数，从而使输出变量由线性转换成非线性。

![](../../.gitbook/assets/image%20%285%29.png)

这里的g-1（）就是sigmoid函数。也叫对数几率函数 **（Logistic Function）**。

![](../../.gitbook/assets/image%20%286%29.png)

优化方法采用的是最大似然估计（Maximum Likelihood Estimation）。



面试题：

1. Linear regression与Logistic Regression不同：

```text
1）线性回归要求变量服从正态分布，logistic回归对变量分布没有要求。

2）线性回归要求因变量（y）是连续性数值变量，而logistic回归要求因变量是分类型变量。

3）线性回归要求自变量(x)和因变量呈线性关系，而logistic回归不要求自变量和因变量呈线性关系

4）logistic回归是分析因变量取某个值的概率与自变量的关系，而线性回归是直接分析因变量与自变量的关系

总之, logistic回归与线性回归实际上有很多相同之处，最大的区别就在于他们的因变量不同，其他的基本都差不多，
正是因为如此，这两种回归可以归于同一个家族，即广义线性模型（generalized linear model）。
这一家族中的模型形式基本上都差不多，不同的就是因变量不同，如果是连续的，就是多重线性回归，
如果是二项分布，就是logistic回归。logistic回归的因变量可以是二分类的，也可以是多分类的，
但是二分类的更为常用，也更加容易解释。所以实际中最为常用的就是二分类的logistic回归。
```

2. 线性回归的前提：

```text
线性回归需要满足四个前提假设
1. Linearity 线性
应变量和每个自变量都是线性关系。
2. Indpendence 独立性
对于所有的观测值，它们的误差项相互之间是独立的。
3. Normality 正态性
误差项服从正态分布。
4. Equal-variance 等方差
所有的误差项具有同样方差。
这四个假设的首字母，合起来就是LINE，这样很好记。

其实除了LINE条件外，多元线性回归还需要满足一个条件：自变量X之间不存在完全多重共线性。

线性回归使用普通最小二乘法（OLS）进行参数估计，上述LINE假定条件也称为OLS假定，用数学语言来说OLS假定就是：

OLS假定1：数据矩阵X列满秩（不存在完全多重共线性）；
OLS假定2：随机误差项ε的总体均值为0，即 E[ε]=0 ​；换句话说就是除了解释变量X之外，放在随机干扰项中的其他因素对于因变量Y的影响总体上有正有负，但均值为0（正态性）；
OLS假定3：随机误差项ε与自变量X不相关；
OLS假定4：随机误差项ε同方差且互不相关，即​ E[εε^T]=σ^2I （无自相关、等方差性）；
OLS假定5：随机误差项满足正态分布（正态性）。

由于OLS估计量 \hat\beta 本身就是一个随机变量，需要对其估计值的优劣性进行判断。
判断​的准则有无偏性、有效性和一致性等准则。上面的假定条件正是由这些准则导出的。
```

