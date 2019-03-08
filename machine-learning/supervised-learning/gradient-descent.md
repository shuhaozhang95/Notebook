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



**Mini-Batch Gradient Descent**





**Online Gradient Descent**

SGD也是对每一个样本更新梯度，所以Online Gradient Descent 跟 SGD几乎一样。这里只是突出他具有Online learning的作用。

* Data points arrive in a stream.
* Compute approximate gradient by summing over a single datapoint.
* Then do a gradient update immediately for this datapoint.

Newton

Adam

