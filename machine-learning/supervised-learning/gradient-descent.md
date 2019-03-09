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



**Higher Order Methods:**

Conjugate Gradient methods \(共轭梯度法\)





Newton

Adam

