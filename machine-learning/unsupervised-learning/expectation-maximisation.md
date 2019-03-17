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

对于最大似然估计， 我们一般都是想要最大化似然函数 $$p(x|\theta)$$ 

log-likelihood:

 $$l(\theta) = \log p(x|\theta) = \log \int p(x,y|\theta) dy \\  = \log \int q(y) \frac{p(x,y|\theta)}{q(y)} dy  \geqslant \int q(y) \log \frac{p(x,y|\theta)}{q(y)} dy \\ =\int q(y) \log \frac{p(y|x,\theta)p(x|\theta)}{q(y)} dy  \\= \int q(y) \log p(x|\theta) dy + \int q(y) \log \frac{p(y|x,\theta)}{q(y)} dy  = l(\theta) - KL[q(y)||p(y|x, \theta)]$$ 

这里我们可以发现 log-likelihood有可以提升的空间，就是使得KL为0。

所以在EM算法中，刚开始初始化我们对隐变量参数先随机赋值

E步我们更新隐变量的分布即 $$q(y) = p(y|x,\theta) = \frac{p(x,y|\theta)}{p(x|\theta)} \propto p(x, y|\theta)$$ 

M步即通过对log likelihood的 $$\theta$$ 求导



更进一步，有些时候，我们的 $$p(x,y|\theta) $$ 是intractable的，即不属于指数镞或不存在共轭的关系，那么我们无法直接写出联合分布的形式。那么我们就会通过Approximate Inference的方式来进行近似。因为在我们的E步无法完全使得KL等于0，所以我们的目标转换成尽可能的减少KL的值。这里我们会把 $$q(y)= \prod_{i}^N q_{i}(y_{i})$$ ，然后在通过多次循环E步来更新完所有的 $$q(y)$$ 后再进行M步。



