# Gradient Descent

**梯度：**

在微积分里面，对多元函数的参数求∂偏导数，把求得的各个参数的偏导数以向量的形式写出来，就是梯度。比如函数 $$f(x,y)$$, 分别对x,y求偏导数，求得的梯度向量就是 $$(\frac{∂f}{∂x}, \frac{∂f}{∂y})^T$$, 简称 grad$$f(x,y)$$ 或者 $$▽f(x,y)$$ 。对于在点 $$ (x_0,y_0)$$ 的具体梯度向量就是 $$(\frac{∂f}{∂x_0}, \frac{∂f}{∂y_0})^T$$ .或者 $$▽f(x_0,y_0)$$，如果是3个参数的向量梯度，就是 $$(\frac{∂f}{∂x}, \frac{∂f}{∂y}, \frac{∂f}{∂z})^T$$ ,以此类推。

那么这个梯度向量求出来有什么意义呢？他的意义从几何意义上讲，就是函数变化增加最快的地方。具体来说，对于函数 $$ f(x,y)$$,在点 $$(x_0,y_0)$$，沿着梯度向量的方向就是 $$(\frac{∂f}{∂x_0}, \frac{∂f}{∂y_0})^T$$ 的方向是 $$f(x,y)$$ 增加最快的地方。或者说，沿着梯度向量的方向，更加容易找到函数的最大值。反过来说，沿着梯度向量相反的方向，也就是 $$-(\frac{∂f}{∂x_0}, \frac{∂f}{∂y_0})^T$$ 的方向，梯度减少最快，也就是更加容易找到函数的最小值。

梯度下降不一定能够找到全局的最优解，有可能是一个局部最优解。当然，如果损失函数是凸函数，梯度下降法得到的解就一定是全局最优解。

**梯度下降的几个概念：**

1. 步长/学习率（Learning rate）：步长决定了在梯度下降迭代的过程中，每一步沿梯度负方向前进的长度。

2.特征（feature）：指的是样本中输入部分，比如2个单特征的样本 $$（x^{(0)},y^{(0)}）,（x^{(1)},y^{(1)}）$$ ,则第一个样本特征为 $$x^{(0)}$$ ，第一个样本输出为 $$y^{(0)}$$ 。

3. 假设函数（hypothesis function）：在监督学习中，为了拟合输入样本，而使用的假设函数，记为 $$h_{\theta}(x)$$ 。比如对于单个特征的m个样本 $$（x^{(i)},y^{(i)}）(i=1,2,...m)$$ 可以采用拟合函数如下： $$h_{\theta}(x) = \theta_0+\theta_1x$$ 。

4. 损失函数（loss function）：为了评估模型拟合的好坏，通常用损失函数来度量拟合的程度。损失函数极小化，意味着拟合程度最好，对应的模型参数即为最优参数。在线性回归中，损失函数通常为样本输出和假设函数的差取平方。比如对于m个样本 $$（x_i,y_i）(i=1,2,...m)$$ ,采用线性回归，损失函数为：

             $$J(\theta_0, \theta_1) = \sum\limits_{i=1}^{m}(h_\theta(x_i) - y_i)^2$$ 

其中 $$x_{i}$$ 表示第i个样本特征， $$y_{i}$$ 表示第i个样本对应的输出， $$h_\theta(x_i)$$ 为假设函数。   

**算法过程：**

1）确定当前位置的损失函数的梯度，对于 $$θ $$ 向量,其梯度表达式如下：

　　　　　　　　 $$\frac{\partial}{\partial\mathbf\theta}J(\mathbf\theta)$$ 

2）用步长乘以损失函数的梯度，得到当前位置下降的距离.

3）确定 $$θ$$ 向量里面的每个值,梯度下降的距离都小于 $$ε$$ ，如果小于 $$ε$$ 则算法终止，当前 $$θ$$ 向量即为最终结果。否则进入步骤4.

4）更新 $$θ$$ 向量，其更新表达式如下。更新完毕后继续转入步骤1.

　　　　　　　　 $$\mathbf\theta= \mathbf\theta - \alpha\frac{\partial}{\partial\theta}J(\mathbf\theta)$$   
**算法调优：**

1. 算法的步长选择
2. 算法参数的初始值选择
3. 归一化

**Stochastic Gradient Descent**

SGD is useful in the situations:

* The dataset is too big to store all of it.
* The dataset is so big that it will take a long time to take an update.

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x4F18;&#x70B9;</th>
      <th style="text-align:left">&#x7F3A;&#x70B9;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x9891;&#x7E41;&#x7684;&#x66F4;&#x65B0;&#x53EF;&#x4EE5;&#x7ED9;&#x6211;&#x4EEC;&#x4E00;&#x4E2A;&#x6A21;&#x578B;&#x8868;&#x73B0;&#x548C;&#x6548;&#x7387;&#x63D0;&#x5347;&#x7684;&#x5373;&#x65F6;&#x53CD;&#x9988;&#x3002;</li>
        </ul>
      </td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x8FD9;&#x79CD;&#x65B9;&#x5F0F;&#x76F8;&#x6BD4;&#x5176;&#x4ED6;&#x6765;&#x8BF4;&#xFF0C;&#x8BA1;&#x7B97;&#x6D88;&#x8017;&#x66F4;&#x5927;&#xFF0C;&#x5728;&#x5927;&#x6570;&#x636E;&#x96C6;&#x4E0A;&#x82B1;&#x8D39;&#x7684;&#x8BAD;&#x7EC3;&#x65F6;&#x95F4;&#x66F4;&#x591A;&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x8F83;&#x9AD8;&#x7684;&#x6A21;&#x578B;&#x66F4;&#x65B0;&#x9891;&#x7387;&#x5728;&#x4E00;&#x4E9B;&#x95EE;&#x9898;&#x4E0A;&#x53EF;&#x4EE5;&#x5FEB;&#x901F;&#x7684;&#x5B66;&#x4E60;&#x3002;</li>
        </ul>
      </td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x9891;&#x7E41;&#x7684;&#x66F4;&#x65B0;&#x4EA7;&#x751F;&#x7684;&#x566A;&#x58F0;&#x53EF;&#x80FD;&#x5BFC;&#x81F4;&#x6A21;&#x578B;&#x53C2;&#x6570;&#x548C;&#x6A21;&#x578B;&#x8BEF;&#x5DEE;&#x6765;&#x56DE;&#x8DF3;&#x52A8;&#xFF08;&#x66F4;&#x5927;&#x7684;&#x65B9;&#x5DEE;&#xFF09;&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x8FD9;&#x79CD;&#x4F34;&#x6709;&#x566A;&#x58F0;&#x7684;&#x66F4;&#x65B0;&#x65B9;&#x5F0F;&#x80FD;&#x8BA9;&#x6A21;&#x578B;&#x907F;&#x514D;&#x5C40;&#x90E8;&#x6700;&#x4F18;&#xFF08;&#x6BD4;&#x5982;&#x8FC7;&#x65E9;&#x6536;&#x655B;&#xFF09;&#x3002;</li>
        </ul>
      </td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x8FD9;&#x79CD;&#x4F34;&#x6709;&#x566A;&#x58F0;&#x7684;&#x66F4;&#x65B0;&#x65B9;&#x5F0F;&#x4E5F;&#x80FD;&#x8BA9;&#x7B97;&#x6CD5;&#x96BE;&#x4EE5;&#x7A33;&#x5B9A;&#x7684;&#x6536;&#x655B;&#x4E8E;&#x4E00;&#x70B9;&#x3002;</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>\*\*\*\*

**Batch Gradient Descent**

* Compute the gradient by first summing over all the training data inputs.
* The do a gradient update.

批量梯度下降对训练集上每一个数据都计算误差，但只在所有训练数据计算完成后才更新模型。

对训练集上的一次训练过程称为一代（epoch）。因此，批量梯度下降是在每一个训练epoch之后更新模型。

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x4F18;&#x70B9;</th>
      <th style="text-align:left">&#x7F3A;&#x70B9;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x66F4;&#x5C11;&#x7684;&#x6A21;&#x578B;&#x66F4;&#x65B0;&#x610F;&#x5473;&#x7740;&#x6BD4;SGD&#x6709;&#x66F4;&#x9AD8;&#x7684;&#x8BA1;&#x7B97;&#x6548;&#x7387;&#x3002;</li>
        </ul>
      </td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x66F4;&#x7A33;&#x5B9A;&#x7684;&#x8BEF;&#x5DEE;&#x68AF;&#x5EA6;&#x53EF;&#x80FD;&#x5BFC;&#x81F4;&#x6A21;&#x578B;&#x8FC7;&#x65E9;&#x6536;&#x655B;&#x4E8E;&#x4E00;&#x4E2A;&#x4E0D;&#x662F;&#x6700;&#x4F18;&#x89E3;&#x7684;&#x53C2;&#x6570;&#x96C6;&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x5728;&#x4E00;&#x4E9B;&#x95EE;&#x9898;&#x4E0A;&#x53EF;&#x4EE5;&#x5F97;&#x5230;&#x66F4;&#x7A33;&#x5B9A;&#x7684;&#x8BEF;&#x5DEE;&#x68AF;&#x5EA6;&#x548C;&#x66F4;&#x7A33;&#x5B9A;&#x7684;&#x6536;&#x655B;&#x70B9;&#x3002;</li>
        </ul>
      </td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x6BCF;&#x4E00;&#x6B21;epoch&#x4E4B;&#x540E;&#x624D;&#x66F4;&#x65B0;&#x4F1A;&#x589E;&#x52A0;&#x4E00;&#x4E2A;&#x7D2F;&#x52A0;&#x6240;&#x6709;&#x8BAD;&#x7EC3;&#x6570;&#x636E;&#x8BEF;&#x5DEE;&#x7684;&#x590D;&#x6742;&#x8BA1;&#x7B97;&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x8BEF;&#x5DEE;&#x8BA1;&#x7B97;&#x548C;&#x6A21;&#x578B;&#x66F4;&#x65B0;&#x8FC7;&#x7A0B;&#x7684;&#x5206;&#x79BB;&#x6709;&#x5229;&#x4E8E;&#x5E76;&#x884C;&#x7B97;&#x6CD5;&#x7684;&#x5B9E;&#x73B0;&#x3002;</li>
        </ul>
      </td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x901A;&#x5E38;&#x6765;&#x8BF4;&#xFF0C;&#x6279;&#x91CF;&#x68AF;&#x5EA6;&#x4E0B;&#x964D;&#x7B97;&#x6CD5;&#x9700;&#x8981;&#x628A;&#x6240;&#x6709;&#x7684;&#x8BAD;&#x7EC3;&#x6570;&#x636E;&#x90FD;&#x5B58;&#x653E;&#x5728;&#x5185;&#x5B58;&#x4E2D;&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x5728;&#x5927;&#x6570;&#x636E;&#x96C6;&#x4E0A;&#xFF0C;&#x8BAD;&#x7EC3;&#x901F;&#x5EA6;&#x4F1A;&#x975E;&#x5E38;&#x6162;&#x3002;</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>\*\*\*\*

**Mini-Batch Gradient Descent**

小批量梯度下降把训练集划分为很多批，对每一批（batch）计算误差并更新参数。

可以选择对batch的梯度进行累加，或者取平均值。取平均值可以减少梯度的方差。

小批量梯度下降在随机梯度下降的鲁棒性和批量梯度下降的效率之间取得平衡。是如今深度学习领域最常见的实现方式。

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>&#x4F18;&#x70B9;</b>
      </th>
      <th style="text-align:left">&#x7F3A;&#x70B9;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x6BD4;&#x6279;&#x91CF;&#x68AF;&#x5EA6;&#x4E0B;&#x964D;&#x66F4;&#x5FEB;&#x7684;&#x66F4;&#x65B0;&#x9891;&#x7387;&#x6709;&#x5229;&#x4E8E;&#x66F4;&#x9C81;&#x68D2;&#x7684;&#x6536;&#x655B;&#xFF0C;&#x907F;&#x514D;&#x5C40;&#x90E8;&#x6700;&#x4F18;&#x3002;</li>
        </ul>
      </td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x5C0F;&#x6279;&#x91CF;&#x68AF;&#x5EA6;&#x4E0B;&#x964D;&#x7ED9;&#x7B97;&#x6CD5;&#x589E;&#x52A0;&#x4E86;&#x4E00;&#x4E2A;&#x8D85;&#x53C2;&#x6570;batch
            size&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x76F8;&#x6BD4;&#x968F;&#x673A;&#x68AF;&#x5EA6;&#x4E0B;&#x964D;&#x66F4;&#x5177;&#x8BA1;&#x7B97;&#x6548;&#x7387;&#x3002;</li>
        </ul>
      </td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x548C;&#x6279;&#x91CF;&#x68AF;&#x5EA6;&#x4E0B;&#x964D;&#x4E00;&#x6837;&#xFF0C;&#x6BCF;&#x4E00;&#x4E2A;batch&#x4E0A;&#x7684;&#x8BEF;&#x5DEE;&#x9700;&#x8981;&#x7D2F;&#x52A0;&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x4E0D;&#x9700;&#x8981;&#x628A;&#x6240;&#x6709;&#x6570;&#x636E;&#x653E;&#x5165;&#x5185;&#x5B58;&#x4E2D;&#x3002;</li>
        </ul>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>**怎么配置mini-batch梯度下降**

Mini-batch梯度下降对于深度学习大部分应用是最常用的方法。

Mini-batch sizes，简称为 “batch sizes”，是算法设计中需要调节的参数。比如对应于不同[GPU](https://www.baidu.com/s?wd=GPU&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)或[CPU](https://www.baidu.com/s?wd=CPU&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)硬件（32,64,128,256等）的内存要求。

batch size是学习过程中的“滑块”。

* 较小的值让学习过程收敛更快，但是产生更多噪声。
* 较大的值让学习过程收敛较慢，但是准确的估计误差梯度。

建议1：batch size的默认值最好是32。`batch size通常从1到几百之间选择，比如32是一个很好的默认值，超过10的值可以充分利用矩阵`_`矩阵相对于矩阵`_`向量的加速优势。`

建议2：调节batch size时，最好观察模型在不同batch size下的训练时间和验证误差的学习曲线

建议3：调整其他所有超参数之后再调整batch size和学习率

`batch size和学习率几乎不受其他超参数的影响，因此可以放到最后再优化。batch size确定之后，可以被视为固定值，从而去优化其他超参数（如果使用了动量超参数则例外）。`



**Online Gradient Descent**

SGD也是对每一个样本更新梯度，所以Online Gradient Descent 跟 SGD几乎一样。这里只是突出他具有Online learning的作用。

* Data points arrive in a stream.
* Compute approximate gradient by summing over a single datapoint.
* Then do a gradient update immediately for this datapoint.



**Line Search and Conjugate Gradient methods \(共轭梯度法\)**

* Higher order methods combine better search directions with line search to improve convergence. 
* For a quadratic surface, conjugate gradients is much faster than standard gradient descent.
* Efficient ways to exploit sparsity in the feature\(input\) vector $$x$$ to perform regression on very large datasets with very high dimensional $$x$$ .

共轭梯度法加入了Line Search来限制方向，避免梯度下降可能出去锯齿的情况。

![Red line: conjugate gradient ](../../.gitbook/assets/image%20%2811%29.png)



**Momentum Gradient Descent**

One simple idea to limit the zig-zag behaviour is to make an update in the average direction of the previous updates.

> _Moving Average_
>
> Consider a set of numbers $$x_{1},...,x_{t}$$. Then the average $$a_{t}$$ is given by 
>
> $$a_{t} = \frac{1}{t} \sum^{t}_{\tau=1}x_{\tau} = \frac{1}{t}(x_{t} +(t-1) a_{t-1}) = \epsilon_{t}x_{t} +\mu_{t}a_{t-1}$$ 
>
> for suitably chosen $$\epsilon_{t}$$ and $$0<\mu_{t}<1$$ . If $$\mu_{t}$$ is small then the more recent $$x$$ contribute more strongly to the moving average.

Momentum idea is to use a form of moving average to the updates:

这里的 $$\widetilde{g}_{k}$$ 是梯度 $$▽f(x_{k})$$, $$x_{k} $$ 就是我们的参数 $$\theta$$ \(或者矩阵W\)

$$\widetilde{g}_{k+1} = \mu_{k}\widetilde{g}_{k} - \epsilon g_{k}(x_{k})$$ 

$$x_{k+1} = x_{k} + \widetilde{g}_{k+1}$$ 

**Hence, Instead of using the update** $$-\epsilon g_{k}(x_{k})$$**, we use the moving average of the update** $$\widetilde{g}_{k+1}$$ **to form the new update.**

**另一种表达方式：**

![](https://www.zhihu.com/equation?tex=V_%7BdW%7D+%3D+%5Cbeta+V_%7BdW%7D%2B%281-%5Cbeta%29dW)

![](https://www.zhihu.com/equation?tex=V_%7Bdb%7D+%3D+%5Cbeta+V_%7Bdb%7D%2B%281-%5Cbeta%29db)

**优点：**

* Momentum can increase the speed of convergence since, for smooth objectives, as we get close to the minimum the gradient decreases and standard gradient descent starts to slow down. \(加速收敛\)
* If the learning rate is too large, standard gradient descent may oscillate\(摆动\), but momentum may reduce oscillations by going in the average direction. \(减少摆动，下降更为稳定\)
* However, the momentum parameter $$\mu$$ may need to be reduced with the iteration count to ensure convergence. \( $$\mu$$在这里调节moving average和前一个 $$\widetilde{g}_{k}$$ 带来的影响的平衡\) 
* Particularly useful when the gradient is noisy. \(因为算上了前一个梯度的方向的平均，一些noise的点影响会减少\)
* Momentum is also useful to avoid saddles\(鞍点，比如两峰之间的低洼部分\) since typically the momentum will carry you over the saddle .



**Nesterov's Accelerated Gradient**

This looks similar to momentum but has a slightly different update

$$\widetilde{g}_{k+1} = \mu_{k} \widetilde{g}_{k} - \epsilon g(x_{k} + \mu_{k} \widetilde{g}_{k})$$ 

That is, we use the gradient of the point we will move to, rather than the current point. 

**结论：在原始形式中，Nesterov Accelerated Gradient（NAG）算法相对于Momentum的改进在于，以“向前看”看到的梯度而不是当前位置梯度去更新。经过变换之后的等效形式中，NAG算法相对于Momentum多了一个本次梯度相对上次梯度的变化量，这个变化量本质上是对目标函数二阶导的近似。由于利用了二阶导的信息，NAG算法才会比Momentum具有更快的收敛速度。**

\*\*\*\*

**Higher Order Methods: 一般是指泰勒展开到了二阶**

**Newton's method**

Consider a function $$f(x)$$ that we wish to find the minimum of. A Taylor expansion up to second order gives：

$$f(x+\triangle) = f(x) +\triangle^{T} \nabla f + \frac{1}{2} \triangle^{T} H_{f} \triangle + O(|\triangle|^{3})$$ 

The matrix $$H_{f}$$ is the Hessian.  

Differentiating the right hand side with respect to $$\triangle$$ , we find that the right hand side has its lowest value when:

$$\nabla f = -H_{f} \triangle \Rightarrow  \triangle =  - H_{f}^{-1} \nabla f$$ 

Hence, an optimisation routine to minimise ****$$f$$ is given by the Newton update

$$x_{k+1} = x_{k} - \epsilon H_{f}^{-1} \nabla f$$ 

With this update, the change in the function is:

$$\triangle^{T} \nabla f + \frac{1}{2} \triangle^{T} H_{f} \triangle = \epsilon (-1 +\frac{\epsilon}{2}) \nabla f^{T} H_{f}^{-1} \nabla$$ 

For quadratic functions, Newton's method converges in one step \(for ****$$\epsilon =1$$ **\)**. More generally one uses a value ****$$\epsilon < 1$$ to avoid overshooting effects.

| **优点** | 缺点 |
| :--- | :--- |
| 牛顿法收敛更快。（通俗来说梯度下降法每次只从你当前所处位置选一个坡度最大的方向走一步，牛顿法在选择方向时，不仅会考虑坡度是否够大，还会考虑你走了一步之后，坡度是否会变得更大。所以，可以说牛顿法比梯度下降法看得更远一点，能更快地走到最底部。） | 牛顿法的每次迭代时间比梯度下降法要长 |
| A benefit of the Newton method over gradient descent is that the decrease in the objective function is invariant（不变） under a linear change of co-ordinates. The  change is independent of the coordinate system \(Up to linear transformations of the coordinates\)  | Storing the Hessian and solving the linear system $$H_{f}^{-1} \nabla f $$ is very expensive. |

\*\*\*\*

**自适应性梯度下降**

**Adagrad**

Adagrad is an algorithm for gradient-based optimization that does just this: It adapts the learning rate to the parameters, performing smaller updates \(i.e. low learning rates\) for parameters associated with frequently occurring features, and larger updates \(i.e. high learning rates\) for parameters associated with infrequent features.

For this reason, it is well-suited for dealing with sparse data.

Previously, we performed an update for all parameters $$\theta$$ at once as every parameter $$\theta_{i}$$ used the same learning rate $$η$$ . As Adagrad uses a different learning rate for every parameter $$\theta_{i}$$ at every time step $$t$$ , we first show Adagrad's per-parameter update, which we then vectorize.

In its update rule, Adagrad modifies the general learning rate $$η$$ at each time step $$t$$ for every parameter $$\theta_{i}$$ based on the past gradients that have been computed for $$\theta_{i}$$ :

$$\theta_{t+1, i} = \theta_{t, i} - \dfrac{\eta}{\sqrt{G_{t, ii} + \epsilon}} \cdot g_{t, i}$$ 

$$G_{t} \in \mathbb{R}^{d \times d}$$ here is a diagonal matrix where each diagonal element $$i$$ , $$i$$ is the sum of the squares of the gradients w.r.t. $$\theta_{i}$$ up to time step $$t$$ , while $$\epsilon$$ is a smoothing term that avoids division by zero \(usually on the order of $$1e-8$$ \). Interestingly, without the square root operation, the algorithm performs much worse.

As $$G_{t}$$ contains the sum of the squares of the past gradients w.r.t. to all parameters $$θ$$ along its diagonal, we can now vectorize our implementation by performing a matrix-vector product ⊙ between $$G_{t}$$ and $$g_{t}$$ :

$$\theta_{t+1} = \theta_{t} - \dfrac{\eta}{\sqrt{G_{t} + \epsilon}} \odot g_{t}$$ 

| Benefit | Weakness |
| :--- | :--- |
| it eliminates the need to manually tune the learning rate. Most implementations use a default value of 0.01 and leave it at that. | its accumulation of the squared gradients in the denominator: Since every added term is positive, the accumulated sum keeps growing during training. This in turn causes the learning rate to shrink and eventually become infinitesimally small, at which point the algorithm is no longer able to acquire additional knowledge. \(学习的变化幅度越来越小，因为要除以梯度的开方\) |

\*\*\*\*

**Adadelta**

 Adadelta is an extension of Adagrad that seeks to reduce its aggressive, monotonically decreasing learning rate. Instead of accumulating all past squared gradients, Adadelta restricts the window of accumulated past gradients to some fixed size $$w$$ ****.

**Adadelta是Adagrad的延伸，将 以往梯度的加和 控制在一个值内。**

\*\*\*\*

**Adam （**adaptive moment estimation**）**

Adam 算法和传统的随机梯度下降不同。随机梯度下降保持单一的学习率（即 alpha）更新所有的权重，学习率在训练过程中并不会改变。而 Adam 通过计算梯度的一阶矩估计和二阶矩估计而为不同的参数设计独立的自适应性学习率。

Adam 算法的提出者描述其为两种随机梯度下降扩展式的优点集合，即：

适应性梯度算法（AdaGrad）为每一个参数保留一个学习率以提升在稀疏梯度（即自然语言和计算机视觉问题）上的性能。

均方根传播（RMSProp）基于权重梯度最近量级的均值为每一个参数适应性地保留学习率。这意味着算法在非稳态和在线问题上有很有优秀的性能。

Adam 算法同时获得了 AdaGrad 和 RMSProp 算法的优点。Adam 不仅如 RMSProp 算法那样基于一阶矩均值计算适应性参数学习率，它同时还充分利用了梯度的二阶矩均值（即有偏方差/uncentered variance）。具体来说，算法计算了梯度的指数移动均值（exponential moving average），超参数 beta1 和 beta2 控制了这些移动均值的衰减率。

移动均值的初始值和 beta1、beta2 值接近于 1（推荐值），因此矩估计的偏差接近于 0。该偏差通过首先计算带偏差的估计而后计算偏差修正后的估计而得到提升。如果对具体的实现细节和推导过程感兴趣，可以继续阅读该第二部分和原论文。

Adaptive Moment Estimation \(Adam\) is another method that computes adaptive learning rates for each parameter. In addition to storing an exponentially decaying average of past squared gradients $$v_{t}$$ like Adadelta and RMSprop, Adam also keeps an exponentially decaying average of past gradients $$m_{t}$$ , similar to momentum. Whereas momentum can be seen as a ball running down a slope, Adam behaves like a heavy ball with friction, which thus prefers flat minima in the error surface. We compute the decaying averages of past and past squared gradients $$m_{t}$$ and $$v_{t}$$ respectively as follows:

\*\*\*\*$$\begin{align}  \begin{split}  m_t &= \beta_1 m_{t-1} + (1 - \beta_1) g_t \\  v_t &= \beta_2 v_{t-1} + (1 - \beta_2) g_t^2  \end{split}  \end{align}$$ ****

$$m_{t}$$ and $$v_{t}$$ are estimates of the first moment \(the mean\) and the second moment \(the uncentered variance\) of the gradients respectively, hence the name of the method. As $$m_{t}$$ and $$v_{t}$$ are initialized as vectors of 0's, the authors of Adam observe that they are biased towards zero, especially during the initial time steps, and especially when the decay rates are small \(i.e. $$\beta_{1}$$ and $$\beta_{2}$$ are close to 1\).

They counteract these biases by computing bias-corrected first and second moment estimates:

$$\begin{align}  \begin{split}  \hat{m}_t &= \dfrac{m_t}{1 - \beta^t_1} \\  \hat{v}_t &= \dfrac{v_t}{1 - \beta^t_2} \end{split}  \end{align}$$ 

They then use these to update the parameters just as we have seen in Adadelta and RMSprop, which yields the Adam update rule:

$$\theta_{t+1} = \theta_{t} - \dfrac{\eta}{\sqrt{\hat{v}_t} + \epsilon} \hat{m}_t$$ 

The authors propose default values of $$0.9$$ for $$\beta_{1}$$ , $$0.999$$ for $$\beta_{2}$$ , and $$10^{-8}$$ for $$\epsilon$$ . They show empirically that Adam works well in practice and compares favorably to other adaptive learning-method algorithms.

**在非凸优化问题上的优势：**

* 直截了当地实现
* 高效的计算
* 所需内存少
* 梯度对角缩放的不变性（第二部分将给予证明）
* 适合解决含大规模数据和参数的优化问题
* 适用于非稳态（non-stationary）目标
* 适用于解决包含很高噪声或稀疏梯度的问题
* 超参数可以很直观地解释，并且基本上只需极少量的调参

\*\*\*\*

\*\*\*\*

\*\*\*\*

\*\*\*\*

\*\*\*\*

\*\*\*\*

\*\*\*\*

