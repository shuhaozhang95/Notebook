# RNN/LSTM/GRU

_**RNN原理：**_

`在普通的全连接网络或CNN中，每层神经元的信号只能向上一层传播，样本的处理在各个时刻独立，因此又被成为前向神经网络(Feed-forward+Neural+Networks)。而在RNN中，神经元的输出可以在下一个时间戳直接作用到自身，即第i层神经元在m时刻的输入，除了（i-1）层神经元在该时刻的输出外，还包括其自身在（m-1）时刻的输出。所以叫循环神经网络` 

_**RNN、LSTM、GRU区别**_

`RNN引入了循环的概念，但是在实际过程中却出现了初始信息随时间消失的问题，即长期依赖（Long-Term Dependencies）问题，所以引入了LSTM。 LSTM：因为LSTM有进有出且当前的cell informaton是通过input gate控制之后叠加的，RNN是叠乘，因此LSTM可以防止梯度消失或者爆炸。推导forget gate，input gate，cell state， hidden information等因为LSTM有进有出且当前的cell informaton是通过input gate控制之后叠加的，RNN是叠乘，因此LSTM可以防止梯度消失或者爆炸的变化是关键。`

`GRU是LSTM的变体，将忘记门和输入们合成了一个单一的更新门。`

_**LSTM防止梯度弥散和爆炸**_

LSTM用加和的方式取代了乘积，使得很难出现梯度弥散。但是相应的更大的几率会出现梯度爆炸，但是可以通过给梯度加门限解决这一问题.



_**RNN**_

我们使用下标 ![t](https://www.zhihu.com/equation?tex=t) 表示输入时序序列的不同位置，用 ![\boldsymbol h\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+h_t) 表示在时刻 ![t](https://www.zhihu.com/equation?tex=t) 的系统隐层状态向量，用 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 表示时刻 ![t](https://www.zhihu.com/equation?tex=t) 的输入。 ![t](https://www.zhihu.com/equation?tex=t) 时刻的隐层状态向量 ![\boldsymbol h\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+h_t) 依赖于当前词 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 和前一时刻的隐层状态向量 ![\boldsymbol h\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+h_%7Bt-1%7D) ：

![](https://www.zhihu.com/equation?tex=%5Cboldsymbol+h_t+%3A%3D+%5Cboldsymbol+f%28%5Cboldsymbol+x_t%2C+%5Cboldsymbol+h_%7Bt-1%7D%29+%5C%2C%2C+%5C%5C)

其中 ![\boldsymbol f](https://www.zhihu.com/equation?tex=%5Cboldsymbol+f) 是一个非线性映射函数。一种通常的做法是计算 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 和 ![\boldsymbol h\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+h_%7Bt-1%7D) 的线性变换后经过一个非线性激活函数，例如

![](https://www.zhihu.com/equation?tex=%5Cboldsymbol+h_t+%3A%3D+%5Cmathrm%7Btanh%7D%28%5Cboldsymbol+W_%7Bxh%7D%5Cboldsymbol+x_t+%2B+%5Cboldsymbol+W_%7Bhh%7D%5Cboldsymbol+h_%7Bt-1%7D%29+%5C%2C%2C+%5C%5C)

其中 ![\boldsymbol W\_{xh}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+W_%7Bxh%7D) 和 ![\boldsymbol W\_{hh}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+W_%7Bhh%7D) 是可学习的参数矩阵，激活函数tanh独立地应用到其输入的每个元素。

![](../../.gitbook/assets/image%20%2823%29.png)



_**LSTM**_

LSTM（Long Short-Term Memory）由Hochreiter和Schmidhuber提出，其数学上的形式化表示如下:

![](https://www.zhihu.com/equation?tex=%5Cbegin%7Beqnarray%7D+%5Cboldsymbol+i_t+%26%3A%3D%26+%5Cmathrm%7Bsigm%7D%28%5Cboldsymbol+W_%7Bxi%7D%5Cboldsymbol+x_t+%2B+%5Cboldsymbol+W_%7Bhi%7D%5Cboldsymbol+h_%7Bt-1%7D%29+%5C%2C%2C+%5C%5C+%5Cboldsymbol+f_t+%26%3A%3D%26+%5Cmathrm%7Bsigm%7D%28%5Cboldsymbol+W_%7Bxf%7D%5Cboldsymbol++x_t+%2B+%5Cboldsymbol+W_%7Bhf%7D%5Cboldsymbol+h_%7Bt-1%7D%29+%5C%2C%2C+%5C%5C+%5Cboldsymbol+o_t+%26%3A%3D%26+%5Cmathrm%7Bsigm%7D%28%5Cboldsymbol+W_%7Bxo%7D%5Cboldsymbol+x_t+%2B+%5Cboldsymbol+W_%7Bho%7D%5Cboldsymbol+h_%7Bt-1%7D%29+%5C%2C%2C+%5C%5C+%5Ctilde%7B%5Cboldsymbol+c%7D_t+%26%3A%3D%26+%5Cmathrm%7Btanh%7D%28%5Cboldsymbol+W_%7Bxc%7D%5Cboldsymbol+x_t+%2B+%5Cboldsymbol+W_%7Bhc%7D%5Cboldsymbol+h_%7Bt-1%7D%29+%5C%2C%2C+%5C%5C+%5Cboldsymbol+c_t+%26%3A%3D%26+%5Cboldsymbol+f_t+%5Codot+%5Cboldsymbol+c_%7Bt-1%7D+%2B+%5Cboldsymbol+i_t+%5Codot+%5Ctilde%7B%5Cboldsymbol+c%7D_t+%5C%2C%2C+%5C%5C+%5Cboldsymbol+h_t+%26%3A%3D%26+%5Cboldsymbol+o_t+%5Codot+%5Cmathrm%7Btanh%7D%28%5Cboldsymbol+c_t%29+%5C%2C.++%5Cend%7Beqnarray%7D+%5C%5C)

其中 ![\odot](https://www.zhihu.com/equation?tex=%5Codot) 代表逐元素相乘，sigm代表sigmoid函数

![](https://www.zhihu.com/equation?tex=%5Cmathrm%7Bsigm%7D%28z%29%3A%3D%5Cfrac%7B1%7D%7B1%2B%5Cexp%28-z%29%7D+%5C%2C.+%5C%5C)

简化后，

![](../../.gitbook/assets/image%20%281%29.png)

![](../../.gitbook/assets/image%20%288%29.png)

* **输出门** ![o\_{t-1}](https://www.zhihu.com/equation?tex=o_%7Bt-1%7D)：输出门的目的是从细胞状态 ![\boldsymbol c\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_%7Bt-1%7D) 产生隐层单元 ![\boldsymbol h\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+h_%7Bt-1%7D) 。并不是 ![\boldsymbol c\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_%7Bt-1%7D) 中的全部信息都和隐层单元 ![\boldsymbol h\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+h_%7Bt-1%7D) 有关， ![\boldsymbol c\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_%7Bt-1%7D) 可能包含了很多对 ![\boldsymbol h\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+h_%7Bt-1%7D) 无用的信息。因此， ![o\_t](https://www.zhihu.com/equation?tex=o_t) 的作用就是判断 ![\boldsymbol c\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_%7Bt-1%7D) 中哪些部分是对 ![\boldsymbol h\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+h_%7Bt-1%7D) 有用的，哪些部分是无用的。
* **输入门** ![i\_t](https://www.zhihu.com/equation?tex=i_t)。![i\_t](https://www.zhihu.com/equation?tex=i_t) 控制当前词 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 的信息融入细胞状态 ![\boldsymbol c\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_t) 。在理解一句话时，当前词 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 可能对整句话的意思很重要，也可能并不重要。输入门的目的就是判断当前词 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 对全局的重要性。当 ![i\_t](https://www.zhihu.com/equation?tex=i_t) 开关打开的时候，网络将不考虑当前输入 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 。
* **遗忘门** ![f\_t](https://www.zhihu.com/equation?tex=f_t): ![f\_t](https://www.zhihu.com/equation?tex=f_t) 控制上一时刻细胞状态 ![\boldsymbol c\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_%7Bt-1%7D) 的信息融入细胞状态 ![\boldsymbol c\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_t) 。在理解一句话时，当前词 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 可能继续延续上文的意思继续描述，也可能从当前词 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 开始描述新的内容，与上文无关。和输入门 ![i\_t](https://www.zhihu.com/equation?tex=i_t) 相反， ![f\_t](https://www.zhihu.com/equation?tex=f_t) 不对当前词 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 的重要性作判断，而判断的是上一时刻的细胞状态 ![\boldsymbol c\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_%7Bt-1%7D) 对计算当前细胞状态 ![\boldsymbol c\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_t) 的重要性。当 ![f\_t](https://www.zhihu.com/equation?tex=f_t) 开关打开的时候，网络将不考虑上一时刻的细胞状态 ![\boldsymbol c\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_%7Bt-1%7D) 。
* **细胞状态** ![\boldsymbol c\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_t) ： ![\boldsymbol c\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_t) 综合了当前词 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 和前一时刻细胞状态 ![\boldsymbol c\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_%7Bt-1%7D) 的信息。这和ResNet中的残差逼近思想十分相似，通过从 ![\boldsymbol c\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_%7Bt-1%7D) 到 ![\boldsymbol c\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_t) 的“短路连接”，梯度得已有效地反向传播。当 ![f\_t](https://www.zhihu.com/equation?tex=f_t) 处于闭合状态时， ![\boldsymbol c\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_t) 的梯度可以直接沿着最下面这条短路线传递到 ![\boldsymbol c\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+c_%7Bt-1%7D) ，不受参数 ![\boldsymbol W\_{xh}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+W_%7Bxh%7D) 和 ![\boldsymbol W\_{hh}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+W_%7Bhh%7D) 的影响，这是LSTM能有效地缓解梯度消失现象的关键所在。

_\*\*\*\*_

_**GRU**_

GRU是另一种十分主流的RNN衍生物。 RNN和LSTM都是在设计网络结构用于缓解梯度消失问题，只不过是网络结构有所不同。GRU在数学上的形式化表示如下：

![](https://www.zhihu.com/equation?tex=%5Cbegin%7Beqnarray%7D+%5Cboldsymbol+z_t+%26%3A%3D%26+%5Cmathrm%7Bsigm%7D%28%5Cboldsymbol+W_%7Bxz%7D%5Cboldsymbol+x_t+%2B+%5Cboldsymbol+W_%7Bhz%7D%5Cboldsymbol++h_%7Bt-1%7D%29%5C%2C%2C+%5C%5C+%5Cboldsymbol+r_t+%26%3A%3D%26+%5Cmathrm%7Bsigm%7D%28%5Cboldsymbol+W_%7Bxr%7D%5Cboldsymbol+x_t+%2B+%5Cboldsymbol+W_%7Bhr%7D%5Cboldsymbol+h_%7Bt-1%7D%29%5C%2C%2C+%5C%5C+%5Ctilde%7B%5Cboldsymbol+h%7D_t+%26%3A%3D%26+%5Cmathrm%7Btanh%7D%28%5Cboldsymbol+W_%7Bxh%7D%5Cboldsymbol+x_t+%2B+%5Cboldsymbol+r_t%5Codot%28%5Cboldsymbol+W_%7Bhh%7D%5Cboldsymbol+h_%7Bt-1%7D%29%29%5C%2C%2C+%5C%5C+%5Cboldsymbol+h_t+%26%3A%3D%26+%28%5Cboldsymbol+1-%5Cboldsymbol+z_t%29%5Codot+%5Ctilde%7B%5Cboldsymbol+h%7D_t+%2B+%5Cboldsymbol+z_t+%5Codot+%5Cboldsymbol+h_%7Bt-1%7D+%5C%2C.+%5Cend%7Beqnarray%7D+%5C%5C)

简化后：

![](../../.gitbook/assets/image%20%2819%29.png)

![](../../.gitbook/assets/image%20%283%29.png)

_\*\*\*\*_

* **重置门** ![r\_t](https://www.zhihu.com/equation?tex=r_t) ： ![r\_t](https://www.zhihu.com/equation?tex=r_t) 用于控制前一时刻隐层单元 ![\boldsymbol h\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+h_%7Bt-1%7D) 对当前词 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 的影响。如果 ![\boldsymbol h\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+h_%7Bt-1%7D) 对 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 不重要， 即从当前词 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 开始表述了新的意思，与上文无关。那么开关 ![r\_t](https://www.zhihu.com/equation?tex=r_t) 可以打开，使得 ![\boldsymbol h\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+h_%7Bt-1%7D)对 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 不产生影响。
* **更新门** ![z\_t](https://www.zhihu.com/equation?tex=z_t) ： ![z\_t](https://www.zhihu.com/equation?tex=z_t) 用于决定是否忽略当前词 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 。类似于LSTM中的输入门 ![i\_t](https://www.zhihu.com/equation?tex=i_t) ， ![z\_t](https://www.zhihu.com/equation?tex=z_t) 可以判断当前词 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) 对整体意思的表达是否重要。当 ![z\_t](https://www.zhihu.com/equation?tex=z_t) 开关接通下面的支路时，我们将忽略当前词 ![\boldsymbol x\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+x_t) ，同时构成了从 ![\boldsymbol h\_{t-1}](https://www.zhihu.com/equation?tex=%5Cboldsymbol+h_%7Bt-1%7D) 到 ![\boldsymbol h\_t](https://www.zhihu.com/equation?tex=%5Cboldsymbol+h_t) 的短路连接，这使得梯度得已有效地反向传播。和LSTM相同，这种短路机制有效地缓解了梯度消失现象，这个机制于highway networks十分相似。

_\*\*\*\*_

_\*\*\*\*_

