# Overfitting/Parameter Adjustment

防止过拟合的方法 过拟合的原因是算法的学习能力过强；一些假设条件（如样本独立同分布）可能是不成立的；训练样本过少不能对整个空间进行分布估计。

* Drop out
* Regularisation
* Batch Normalisation
* Early Stop
* Cross Validation
* Batch size
* learning rate
* Feature selection/ Feature reduction（降维）
* Increase data set size \(resample, add noise\)

_**Regularisation**_

L1 regularisation一般来增强稀疏性，可以用来筛选feature。L2的话主要是防止过拟合，增加泛化能力。

![](../../.gitbook/assets/image%20%2830%29.png)

左边的l1，右边的l2， l1在作图只要不是特殊情况下与正方形的边相切，一定是与某个顶点优先相交，那必然存在横纵坐标轴中的一个系数为0，起到对变量的筛选的作用。 l2的时候，其实就可以看作是上面这个蓝色的圆，在这个圆的限制下，点可以是圆上的任意一点，所以q＝2的时候也叫做岭回归，岭回归是起不到压缩变量的作用的，在这个图里也是可以看出来的。



dropout， regularization， batch normalizatin，但是要注意dropout只在训练的时候用，让一部分神经元随机失活。

Batch normalization是为了让输出都是单位高斯激活，方法是在连接和激活函数之间加入BatchNorm层，计算每个特征的均值和方差进行规则化。

### 

