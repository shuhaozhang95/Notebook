# Expectation Maximisation

EM算法是由隐变量的最大似然估计法。

对于Exponential family模型，一般都有以下特征

* Concave function 凸函数
* Maximum may be closed-form
* if not, numerical optimisation is still generally straightforward. \(gradient descent\)

对于Latent variable model, $$p(x| \theta_{x}, \theta_{y}) = \int p(x|y, \theta_{x}) p(y|\theta_{y}) dy$$ 

* Usually no closed form optimum
* often multiple local maxima
* Direct numerical optimisation may be possible but infrequently easy

对于最大似然估计，

