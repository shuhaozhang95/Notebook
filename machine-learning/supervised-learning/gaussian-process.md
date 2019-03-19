# Gaussian Process

高斯过程：描述的是连续的随机过程，其中任意的点满足高斯分布。可以用Mean function和Co-variance function来决定一段GP。GP上的任意多个点满足多元高斯分布。即把一列X输入到GP中，我们可以确定一个多元高斯分布。

在实际应用中，我们一般用高斯过程回归。

mean function 一般设置为0，因为Mean function与X没啥关系。covariance function就是核方法。主要用来描述X中各维度的相关性（非线性关系）

一般核函数都是 半正定的 检验半正定的方法：

 $$X^{T}AX \geqslant 0 $$ 为半正定

$$X^{T}AX > 0$$ 为正定

  几种常见的核方法 性质 

（平稳/不平稳）暂时没有搜到如何评价核函数是否平稳（可能跟X的变化有关？不容易产生无穷极值为平稳？Y依照X的变化比较平稳？） 

| Kernel function | formula |  |
| :--- | :--- | :--- |
| Linear Kernel | $$k(x,y) = x^{T}y + c$$  | Simplest kernel function. Using a linear kernel are often equivalent to non-kernel counterparts. KPCA with linear kernel is the same as standard PCA. |
| Polynomial Kernel | $$k(x,y) = (\alpha x^{T}y + c)^d$$  | The Polynomial kernel is a non-stationary kernel. Polynomial kernels are well suited for problems where all the training data is normalized. |
| Gaussian Kernel | $$k(x,y) = \exp(- \frac{\lVert x-y \rVert ^{2}}{2 \sigma^{2}})$$  | The Gaussian kernel is an example of radial basis function kernel. |
| Exponential Kernel \(RBF kernel\) | $$k(x,y) = \exp (- \frac{\lVert x-y \rVert}{ 2\sigma^{2}})$$  | The exponential kernel is closely related to the Gaussian Kernel, with only the square of the norm left out. |
| Matern Kernel | $$C_{v}(d) = \sigma^{2} \frac{2^{1-\nu}}{\Gamma(\nu)}(\sqrt{2\nu} \frac{d}{\rho})^{\nu} K_{\nu} (\sqrt{2\nu} \frac{d}{\rho})$$  |  where ![\Gamma ](https://wikimedia.org/api/rest_v1/media/math/render/svg/4cfde86a3f7ec967af9955d0988592f0693d2b19) is the [gamma function](https://en.wikipedia.org/wiki/Gamma_function), ![K\_{\nu }](https://wikimedia.org/api/rest_v1/media/math/render/svg/f151831e9842e5daee3a71075a17102d10f1cf7e) is the modified [Bessel function](https://en.wikipedia.org/wiki/Bessel_function) of the second kind, and ρ and ν are non-negative [parameters](https://en.wikipedia.org/wiki/Parameter) of the covariance. |
| Laplacian Kernel | $$k(x,y) = \exp (- \frac{\lVert x-y \rVert}{\sigma})$$  | The Laplace Kernel is completely equivalent to the exponential kernel, except for being less sensitive for changes in the sigma parameter. Being equivalent, it is also a radial basis function kernel. |
| ANOVA Kernel | $$k(x,y) = \sum_{k=1}^{n} \exp(- \sigma (x^{k}-y^{k})^2)^{d}$$  |  It is said to [perform well in multidimensional regression problems](http://www.nicta.com.au/research/research_publications?sq_content_src=%2BdXJsPWh0dHBzJTNBJTJGJTJGcHVibGljYXRpb25zLmluc2lkZS5uaWN0YS5jb20uYXUlMkZzZWFyY2glMkZmdWxsdGV4dCUzRmlkJTNEMjYxJmFsbD0x) \(Hofmann, 2008\). |
| Sigmoid Kernel | $$k(x,y) = \tanh (\alpha x ^{T}y +c)$$  | Sigmoid Kernel and as the Multilayer Perceptron \(MLP\) kernel. It is interesting to note that a SVM model using a sigmoid kernel function is equivalent to a two-layer, perceptron neural network. |
| Rational Quadratic Kernel | $$k(x,y) = 1- \frac{\lVert x-y \rVert^{2}}{\lVert x-y \rVert^{2}+c}$$  | The Rational Quadratic kernel is less computationally intensive than the Gaussian kernel and can be used as an alternative when using the Gaussian becomes too expensive. |
| Multiquadric Kernel | $$k(x,y) = \sqrt{ \lVert x-y \rVert^{2} +c^{2}}$$  | The Multiquadric kernel can be used in the same situations as the Rational Quadratic kernel. As is the case with the Sigmoid kernel, it is also an example of an non-positive definite kernel. |
| Inverse Multiquadric Kernel | $$k(x,y) = \frac{1}{\sqrt{\lVert x-y \rVert^{2} + c^{2}}}$$  | The Inverse Multi Quadric kernel. As with the Gaussian kernel, it results in a kernel matrix with full rank \(Micchelli, 1986\) and thus forms a infinite dimension feature space. |
| Power Kernel | $$k(x,y) = - \lVert x-y \rVert^{d}$$  | The Power kernel is also known as the \(unrectified\) triangular kernel. It is an example of scale-invariant kernel \(Sahbi and Fleuret, 2004\) and is also only conditionally positive definite. |
| Log Kernel | $$k(x,y) = -\log (\lVert x-y \rVert^d +1)$$  | The Log kernel seems to be particularly interesting for images, but is only conditionally positive definite. |
| Chi-Square Kernel | $$k(x,y) = 1- \sum_{i=1}^{n} \frac{(x_{i} -y_{i} )^{2}}{\frac{1}{2} (x_{i}+y_{i})}$$  |  The Chi-Square kernel comes from the [Chi-Square distribution](http://en.wikipedia.org/wiki/Chi-square_distribution). |
| Generalized T-student Kernel  | $$k(x,y) = \frac{1}{1+\lVert x-y \rVert^d}$$  | The Generalized T-Student Kernel has been proven to be a Mercel Kernel, thus having a positive semi-definite Kernel matrix \(Boughorbel, 2004\). |
| Bayesian Kernel | $$k(x,y) = \sum^{N}_{l=1} k_{l}(x_{l}, y_{l}) \\$$  | where $$k_{l}(a,b) = \sum_{c\in {0;1}} P(Y=c|X_{l}=a) P(Y=c|X_{l} =b)$$  |

_**高斯过程回归预测**_ 



_**高斯过程回归优化**_

