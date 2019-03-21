# Support Vector Machine

## The representer theorem

Given a set of paired observation $$(x_{1}, y_{1}),..., (x_{n}, y_{n})$$ \(regression or classification\). Find the function $$f^{*}$$ in the RKHS $$\mathcal{H}$$ which satisfies:

$$f^{*} = \arg \min_{f \in \mathcal{H}} J(f)$$ 

where $$J(f) = L_{y}(f(x_{1}),...,f(x_{n}))+ \Omega (\lVert f \rVert^{2}_{\mathcal{H}})$$, $$\Omega$$ is non-decreasing. $$y$$ is the vector of $$y_{i}$$, Loss $$L$$ depends on $$x_{i}$$only via $$f(x_{i})$$ .

* Classification: $$L_{y} (f(x_{1}), ...,f(x_{n})) = \sum^{n}_{i=1} \mathcal{I}_{y_{i} f(x_{i}) \le 0 }$$ 
* Regression: $$L_{y}(f(x_{1}),...,f(x_{n})) = \sum^{n}_{i=1} (y_{i} - f(x_{i}))^{2}$$ 

Hence, The representer theorem: a solution to 

$$min_{f\in \mathcal{H}} \left [ L_{y}(f(x_{i}),...,f(x_{n}))+ \Omega (\lVert f \rVert)^{2}_{\mathcal{H}} \right ]$$ 

takes the form 

$$f^{*} = \sum^{n}_{i=1} \alpha_{i} k(x_{i}, \cdot)$$ 

if $$\Omega$$ is strictly increasing, the solution must have this form. 

## Convex optimization

### Convex set Definition

> C is convex if for all $$x_{1}, x_{2} \in C$$ and any $$0 \le \theta \le 1$$ we have $$\theta x_{1} + (1-\theta)x_{2} \in C$$ , i.e. every point on the line between $$x_{1}$$ and $$x_{2}$$ lies in $$C$$.

### Convex function Definition

> A function $$f$$ is **convex** if its domain $$domf$$ is a convex set and if $$\forall x,y \in dom f$$, and any $$0 \le \theta \le 1$$, $$f(\theta x + (1-\theta)y) \le \theta f(x) +(1-\theta)f(y)$$. The function is **strictly convex** if the inequality is strict for $$x \neq y$$  .

Generic Optimisation problem on $$x \in \mathcal{R}^{n}$$ ,

$$minimize \quad f_{0}(x) \\subject \ to \quad f_{i}(x) \le 0 \quad i=1,...,m (5)\\\quad \quad \quad \quad\quad \ h_{i}(x) = 0 \quad i=1,...,p$$ 

$$p^{*}$$ the optimal value of \(5\), $$\mathcal{D}$$ assumed nonempty, where

$$D:= \bigcap^{m}_{i=0} domf_{i} \cap \bigcap^{p}_{i=1} domh_{i} \\ (dom f_{i} = subset\ of \ \mathcal{R}^{n} \ where \ f_{i} \ defined.)$$  

Ideally we would want an unconstrained problem, Hence, we have

$$minimize \quad f_{0}(x) + \sum^{m}_{i=1} I\_(f_{i}(x)) +\sum^{p}_{i=1} I_{0}(h_{i}(x))$$ 

where $$I\_(u) = \left\{ \begin{aligned} 0 & = u \le 0 \\ \infty & = u>0 \\  \end{aligned} \right.$$  and $$I_{0}(u)$$ is the indicator of 0. 

然后我们引出拉格朗日

The _**Lagrangian L**_: $$\mathcal{R}^{n} \times \mathcal{R}^{m} \times \mathcal{R}^{p} \to \mathcal{R}$$ is a lower bound on the original problem:

$$L(x, \lambda, \nu): = f_{0}(x) +\sum^{m}_{i=1} \underbrace{\lambda_{i}f_{i}(x)}_{\le I\_({f_{i}(x)})} + \sum^{p}_{i=1} \underbrace{\nu_{i}h_{i}(x)}_{\le I_{0}(h_{i}(x))}$$ 

and has domain $$domL:= \mathcal{D} \times \mathcal{R}^{m} \times \mathcal{R}^{p}.$$ The vectors $$\lambda$$ and $$\nu$$ are called _**lagrange multipliers**_ or _**dual variables**_. To ensure a lower bound, we require $$\lambda \succeq 0$$ .

为了找到Lagrangian的解法，我们引出_**Largrange dual function**_

The _**Lagrange dual function**_: minimize Lagrangian 

when 

## Support vector classification

{% embed url="http://www.gatsby.ucl.ac.uk/~gretton/coursefiles/Slides5A.pdf" %}



