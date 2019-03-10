# Backpropagation

Backpropagation（要能推倒） 

后向传播是在求解损失函数L对参数w求导时候用到的方法，目的是通过**链式法则**对参数进行一层一层的求导。这里重点强调：要将参数进行随机初始化而不是全部置0，否则所有隐层的数值都会与输入相关，这称为对称失效。 

**大致过程**是:

首先前向传导计算出所有节点的激活值和输出值，

![](../../.gitbook/assets/image%20%282%29.png)

计算整体损失函数：

![](../../.gitbook/assets/image%20%284%29.png)

然后针对第L层的每个节点计算出残差（这里是因为UFLDL中说的是残差，本质就是整体损失函数对每一层激活值Z的导数），所以要对W求导只要再乘上激活函数对W的导数即可

![](../../.gitbook/assets/image%20%286%29.png)

![](../../.gitbook/assets/image%20%289%29.png)


