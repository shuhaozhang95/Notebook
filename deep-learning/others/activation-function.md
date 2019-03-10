# Activation function

{% embed url="https://blog.csdn.net/woaidapaopao/article/details/77806273" %}

<table>
  <thead>
    <tr>
      <th style="text-align:center">&#x6FC0;&#x6D3B;&#x51FD;&#x6570;</th>
      <th style="text-align:left">&#x516C;&#x5F0F;/&#x56FE;&#x50CF;</th>
      <th style="text-align:left">&#x7F3A;&#x70B9;</th>
      <th style="text-align:left">&#x4F18;&#x70B9;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:center">Sigmoid</td>
      <td style="text-align:left">
        <p></p>
        <p></p>
        <p>
          <img src="../../.gitbook/assets/image (14).png" alt/>
        </p>
      </td>
      <td style="text-align:left">
        <p>1&#x3001;&#x4F1A;&#x6709;&#x68AF;&#x5EA6;&#x5F25;&#x6563;</p>
        <p></p>
        <p>2&#x3001;&#x4E0D;&#x662F;&#x5173;&#x4E8E;&#x539F;&#x70B9;&#x5BF9;&#x79F0;</p>
        <p></p>
        <p>3&#x3001;&#x8BA1;&#x7B97;exp&#x6BD4;&#x8F83;&#x8017;&#x65F6;</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:center">Softmax</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x5904;&#x7406;&#x591A;&#x7C7B;&#x522B;&#x7684;&#x5206;&#x7C7B;&#x95EE;&#x9898;&#xFF0C;&#x6620;&#x5C04;&#x5230;&#xFF08;0&#xFF0C;1&#xFF09;&#x8303;&#x56F4;&#xFF0C;&#x6240;&#x6709;&#x7684;&#x503C;&#x90FD;&#x4E3A;&#x6B63;&#x6570;&#x4E14;&#x52A0;&#x548C;&#x4E3A;1&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:center">Tanh</td>
      <td style="text-align:left">
        <img src="../../.gitbook/assets/tanh.jpg" alt/>
      </td>
      <td style="text-align:left">&#x68AF;&#x5EA6;&#x5F25;&#x6563;&#x6CA1;&#x6709;&#x89E3;&#x51B3;</td>
      <td
      style="text-align:left">1&#x3001;&#x89E3;&#x51B3;&#x4E86;&#x539F;&#x70B9;&#x5BF9;&#x79F0;&#x7684;&#x95EE;&#x9898;2&#x3001;&#x6BD4;Sigmoid&#x66F4;&#x5FEB;</td>
    </tr>
    <tr>
      <td style="text-align:center">ReLU</td>
      <td style="text-align:left">
        <img src="../../.gitbook/assets/relu.jpg" alt/>
      </td>
      <td style="text-align:left">&#x68AF;&#x5EA6;&#x5F25;&#x6563;&#x6CA1;&#x5B8C;&#x5168;&#x89E3;&#x51B3;&#xFF0C;&#x5728;&#xFF08;-&#xFF09;&#x90E8;&#x5206;&#x76F8;&#x5F53;&#x4E8E;&#x795E;&#x7ECF;&#x6B7B;&#x4EA1;&#x800C;&#x4E14;&#x4E0D;&#x4F1A;&#x590D;&#x6D3B;</td>
      <td
      style="text-align:left">1&#x3001;&#x89E3;&#x51B3;&#x4E86;&#x90E8;&#x5206;&#x68AF;&#x5EA6;&#x5F25;&#x6563;&#x95EE;&#x9898;2&#x3001;&#x6536;&#x655B;&#x901F;&#x5EA6;&#x66F4;&#x5FEB;</td>
    </tr>
    <tr>
      <td style="text-align:center">Leaky ReLU</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x89E3;&#x51B3;&#x4E86;&#x795E;&#x7ECF;&#x6B7B;&#x4EA1;&#x7684;&#x95EE;&#x9898;</td>
    </tr>
    <tr>
      <td style="text-align:center">Maxout</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x53C2;&#x6570;&#x6BD4;&#x8F83;&#x591A;&#xFF0C;&#x672C;&#x8D28;&#x4E0A;&#x662F;&#x5728;&#x8F93;&#x51FA;&#x7ED3;&#x679C;&#x4E0A;&#x53C8;&#x589E;&#x52A0;&#x4E86;&#x4E00;&#x5C42;</td>
      <td
      style="text-align:left">&#x514B;&#x670D;&#x4E86;ReLU&#x7684;&#x7F3A;&#x70B9;&#xFF0C;&#x6BD4;&#x8F83;&#x63D0;&#x5021;&#x4F7F;&#x7528;</td>
    </tr>
  </tbody>
</table>

面试问题：

_**Softmax与Cross entropy的关系**_

 一句话概括：**softmax**把分类输出标准化成概率分布，**cross-entropy（**交叉熵**）**刻画预测分类和真实结果之间的相似度。交叉熵损失函数是搭配softmax使用的损失函数。

![Cross Entropy](../../.gitbook/assets/image%20%285%29.png)

_**Sigmoid的求导：**_

$$\begin{aligned} f'(z) &= (\frac{1}{1+e^{-z}})'  \\ &= \frac{e^{-z}}{(1+e^{-z})^{2}}  \\ &= \frac{1+e^{-z}-1}{(1+e^{-z})^{2}}   \\ &= \frac{1}{(1+e^{-z})}(1-\frac{1}{(1+e^{-z})})  \\ &= f(z)(1-f(z)) \\ \end{aligned}$$ 



_**信息量：**_

假设XX是一个离散型随机变量，其取值集合为 $$X$$ ，概率分布函数为 $$p(x)=Pr(X=x),x∈\mathcal{X}$$ ，我们定义事件 $$X = x_{0}$$ 的信息量为：$$I(x_0)=-log(p(x_0))$$ 

可以理解为，一个事件发生的概率越大，则它所携带的信息量就越小，而当 $$p(x_{0})=1$$ 时，熵将等于0，也就是说该事件的发生不会导致任何信息量的增加。



_**熵：**_

熵其实是信息量的期望值，它是一个随机变量的确定性的度量。熵越大，变量的取值越不确定，反之就越确定。

对于一个随机变量X而言，它的所有可能取值的信息量的期望 $$E[I(x)]$$ 就称为熵。 

X的熵定义为：$$H(X)=E_p\log \frac{1}{p(x)}=-\sum\limits_{x∈X}p(x)\log p(x)$$

如果p\(x\)是连续型随机变量的pdf，则熵定义为： $$H(X)=-\int\limits_{x∈X}p(x)\log p(x)dx$$ 

 为了保证有效性，这里约定当 $$p(x)→0$$ 时,有 $$p(x)logp(x)→0 $$   
当X为0-1分布时，熵与概率p的关系如下图：   
![&#x8FD9;&#x91CC;&#x5199;&#x56FE;&#x7247;&#x63CF;&#x8FF0;](https://img-blog.csdn.net/20160302180818189)

可以看出，当两种取值的可能性相等时，不确定度最大（此时没有任何先验知识），这个结论可以推广到多种取值的情况。在图中也可以看出，当p=0或1时，熵为0，即此时X完全确定。

熵的单位随着公式中log运算的底数而变化，当底数为2时，单位为“比特”\(bit\)，底数为e时，单位为“奈特”。



_**相关熵（KL Divergence）：**_











_**交叉熵：**_

