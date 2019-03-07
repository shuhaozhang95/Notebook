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



dropout， regularization， batch normalizatin，但是要注意dropout只在训练的时候用，让一部分神经元随机失活。

Batch normalization是为了让输出都是单位高斯激活，方法是在连接和激活函数之间加入BatchNorm层，计算每个特征的均值和方差进行规则化。

### 

