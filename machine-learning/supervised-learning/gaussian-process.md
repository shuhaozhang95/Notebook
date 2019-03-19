# Gaussian Process

高斯过程：描述的是连续的随机过程，其中任意的点满足高斯分布。可以用Mean function和Co-variance function来决定一段GP。GP上的任意多个点满足多元高斯分布。即把一列X输入到GP中，我们可以确定一个多元高斯分布。

在实际应用中，我们一般用高斯过程回归。

mean function 一般设置为0，因为Mean function与X没啥关系。covariance function就是核方法。主要用来描述X中各维度的相关性（非线性关系）

一般核函数都是 半正定的 检验半正定的方法：

 $$X^{T}AX \geqslant 0 $$ 为半正定

$$X^{T}AX > 0$$ 为正定

  几种常见的核方法 性质 （平稳/不平稳） 

|  |  |
| :--- | :--- |
|  |  |

_**高斯过程回归预测**_



_**高斯过程回归优化**_

