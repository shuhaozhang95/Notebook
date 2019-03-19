# LDA

概率主题模型：隐含狄利克雷分布（Latent Dirichlet Allocation，简称LDA）

理解LDA，可以分为下述5个步骤：

1. 一个函数：gamma函数
2. 四个分布：二项分布、多项分布、beta分布、Dirichlet分布
3. 一个概念和一个理念：共轭先验和贝叶斯框架
4. 两个模型：pLSA、LDA（在本文[第4 部分](http://blog.csdn.net/v_july_v/article/details/41209515#t14)阐述）
5. 一个采样：Gibbs采样

LDA是一种主题模型，它可以将**文档集 中每篇文档的主题以概率分布的形式给出**，从而通过分析一些文档**抽取出它们的主题（分布）出来**后，便可以根据**主题（分布）进行主题聚类或文本分类**。同时，它是一种典型的词袋模型，即一篇文档是由一组词构成，词与词之间没有先后顺序的关系。

此外，**一篇文档可以包含多个主题，文档中每一个词都由其中的一个主题生成。**

反过来，当我们看到一篇文章后，往往喜欢推测这篇文章是如何生成的，我们可能会认为作者先确定这篇文章的几个主题，然后围绕这几个主题遣词造句，表达成文。

所以，LDA就是要干这事：**根据给定的一篇文档，反推其主题分布**。

**人类是根据上述文档生成过程写成了各种各样的文章，现在某小撮人想让计算机利用LDA干一件事：你计算机给我推测分析网络上各篇文章分别都写了些啥主题，且各篇文章中各个主题出现的概率大小（主题分布）是啥**。

在LDA模型中，一篇文档生成的方式如下：

1. 从狄利克雷分布 $$\alpha$$ 中取样生成文档 $$i$$ 的主题分布 $$\theta_{i}$$ 
2. 从主题的多项式分布 $$\theta_{i}$$ 中取样生成文档 $$i$$ 第 $$j$$ 个词的主题 $$z_{i,j}$$ 
3.  从狄利克雷分布 $$\beta$$ 中取样生成主题 $$z_{i,j}$$ 对应的词语分布 $$\phi_{z_{i,j}}$$ 
4.  从词语的多项式分布 $$\phi_{z_{i,j}}$$ 中采样最终生成词语 $$w_{i,j}$$ 

其中，类似**Beta分布是二项式分布的共轭先验概率分布，而狄利克雷分布（Dirichlet分布）是多项式分布的共轭先验概率分布。**

什么又是共轭呢？

轭的意思是束缚、控制，共轭从字面上理解，则是共同约束，或互相约束。

**在贝叶斯概率理论中，如果后验概率P\(θ\|x\)和先验概率p\(θ\)满足同样的分布律，那么，先验分布和后验分布被叫做共轭分布，同时，先验分布叫做似然函数的共轭先验分布**。

                                         **先验分布**![](https://img-blog.csdn.net/20141110214925523) **+ 样本信息**![](https://img-blog.csdn.net/20141110211153578) ****![](https://img-blog.csdn.net/20141110190250086) **后验分布**![](https://img-blog.csdn.net/20141110215058639)

![](../../.gitbook/assets/image%20%2836%29.png)

 针对于这种**观测到的数据符合多项分布，参数的先验分布和后验分布都是Dirichlet 分布**的情况，**就是Dirichlet-Multinomial 共轭**。换言之，至此已经证明了Dirichlet分布的确就是多项式分布的共轭先验概率分布。

![](../../.gitbook/assets/image%20%282%29.png)

为了方便描述，首先定义一些变量：

* ![](https://img-blog.csdn.net/20141118232053295)表示词，![](https://img-blog.csdn.net/20141118232219439)表示所有单词的个数（固定值）
* ![](https://img-blog.csdn.net/20141118232105500)表示主题，![](https://img-blog.csdn.net/20141118232243400)是主题的个数（预先给定，固定值）
* ![](https://img-blog.csdn.net/20141118232121329)表示语料库，其中的![](https://img-blog.csdn.net/20141118232236677)是语料库中的文档数（固定值）
* ![](https://img-blog.csdn.net/20141118232113406)表示文档，其中的![](https://img-blog.csdn.net/20141118232228453)表示一个文档中的词数（随机变量）

LDA模型中一篇文档生成的方式是怎样的：

1. 按照先验概率 $$p(d_{i})$$ 选择一篇文档 $$d_{i}$$ 
2. 从狄利克雷分布（即Dirichlet分布） $$\alpha$$ 中取样生成文档 $$d_{i}$$ 的主题分布 $$\theta_{i}$$ ，换言之，主题分布 $$\theta_{i}$$ 由超参数为 $$\alpha$$ 的Dirichlet分布生成 
3. 从主题的多项式分布 $$\theta_{i}$$ 中取样生成文档 $$d_{i}$$ 第 j 个词的主题 $$z_{i,j}$$ 
4. 从狄利克雷分布（即Dirichlet分布） $$\beta$$ 中取样生成主题对应的词语分布 $$\phi_{z_{i,j}}$$ ，换言之，词语分布 $$\phi_{z_{i,j}}$$ 由参数为 $$\beta$$ 的Dirichlet分布生成
5. 从词语的多项式分布中采样最终生成词语 $$w_{i,j}$$ ”

**那PLSA跟LDA的区别在于什么地方呢？区别就在于：**

PLSA中，主题分布和词分布是唯一确定的，能明确的指出主题分布可能就是{教育：0.5，经济：0.3，交通：0.2}，词分布可能就是{大学：0.5，老师：0.3，课程：0.2}。但在LDA中，主题分布和词分布不再唯一确定不变，即无法确切给出。例如主题分布可能是{教育：0.5，经济：0.3，交通：0.2}，也可能是{教育：0.6，经济：0.2，交通：0.2}，到底是哪个我们不再确定（即不知道），因为它是随机的可变化的。但再怎么变化，也依然服从一定的分布，即主题分布跟词分布由Dirichlet先验随机确定。

-----------------------------------------------

1. 假定语料库中共有M篇文章，每篇文章下的Topic的主题分布是一个从参数为的Dirichlet先验分布中采样得到的Multinomial分布，每个Topic下的词分布是一个从参数为的Dirichlet先验分布中采样得到的Multinomial分布。
2. 对于某篇文章中的第n个词，首先从该文章中出现的每个主题的Multinomial分布（主题分布）中选择或采样一个主题，然后再在这个主题对应的词的Multinomial分布（词分布）中选择或采样一个词。不断重复这个随机生成过程，直到M篇文章全部生成完成。

综上，M 篇文档会对应于 M 个独立的 Dirichlet-Multinomial 共轭结构，K 个 topic 会对应于 K 个独立的 Dirichlet-Multinomial 共轭结构。

* 其中，![](https://img-blog.csdn.net/20141117160438989)→θ→z 表示生成文档中的所有词对应的主题，显然 ![](https://img-blog.csdn.net/20141117160438989)→θ 对应的是Dirichlet 分布，θ→z 对应的是 Multinomial 分布，所以整体是一个 Dirichlet-Multinomial 共轭结构，如下图所示：

![](../../.gitbook/assets/image%20%285%29.png)

* 类似的，![](https://img-blog.csdn.net/20141117160531515)→φ→w，容易看出， 此时β→φ对应的是 Dirichlet 分布， φ→w 对应的是 Multinomial 分布， 所以整体也是一个Dirichlet-Multinomial 共轭结构，如下图所示：

![](../../.gitbook/assets/image%20%2828%29.png)

 在LDA这个估计主题分布、词分布的过程中，它们的先验分布（即Dirichlet分布）事先由人为给定，那么LDA就是要去求它们的后验分布（LDA中可用gibbs采样去求解它们的后验分布，得到期望![](https://img-blog.csdn.net/20141122141624588)、![](https://img-blog.csdn.net/20141122141643109)）！



_**Gibbs Sampling**_

**Gibbs sampling** is one MCMC. technique suitable for the task. The idea in **Gibbs sampling** is to generate posterior **samples**. by sweeping through each variable \(or block of variables\) to **sample** from its conditional. distribution with the remaining variables fixed to their current values.

证明Gibbs Sampling可以收敛到目标分布：

即证明Gibbs Sampling满足Detailed Balance. 即满足 $$p(x)T(x \rightarrow x') = p(x') T(x' \rightarrow x)$$ 

The transition probabilities are given by: $$T(x \rightarrow x') = \pi_{i} p(x_{i}'| x_{\backslash i}) $$ , where $$\pi_{i}$$ is the probability of choosing to update the $$i $$ th variable. \(to handle rotation updates instead of random ones, we need to consider transitions due to one full sweep\).

Then we have:

 $$T(x \rightarrow x') p(x) = \pi_{i} p(x_{i}' | x_{\backslash i}) \underbrace{ p(x_{i} | x_{\backslash i}) p(x_{\backslash i})}_{p(x)}$$ 

and 

$$T(x' \rightarrow x) p(x') = \pi_{i} p(x_{i} | x'_{\backslash i}) \underbrace{ p(x_{i} | x'_{\backslash i}) p(x'_{\backslash i})}_{p(x')}$$ 

But $$x'_{\backslash i } = x_{\backslash i}$$ so detailed balance holds.



给定一个文档集合，w是可以观察到的已知变量，![](https://img-blog.csdn.net/20141117160438989)和![](https://img-blog.csdn.net/20141117160531515)是根据经验给定的先验参数，其他的变量z，θ和φ都是未知的隐含变量，需要根据观察到的变量来学习估计的。根据LDA的图模型，可以写出所有变量的联合分布：

![](../../.gitbook/assets/image%20%287%29.png)

 注：上述公式中及下文中，![](https://img-blog.csdn.net/20141121011305243)等价上文中定义的![](https://img-blog.csdn.net/20141117160518098)，![](https://img-blog.csdn.net/20141121011310969)等价于上文中定义的![](https://img-blog.csdn.net/20141117160656067)，![](https://img-blog.csdn.net/20141121011424772)等价于上文中定义的![](https://img-blog.csdn.net/20141117160613962)， $$\theta_{m}$$ 等价于上文中定义的![](https://img-blog.csdn.net/20141117160452327)。

 因为![](https://img-blog.csdn.net/20141117160438989)产生主题分布θ，主题分布θ确定具体主题，且![](https://img-blog.csdn.net/20141117160531515)产生词分布φ、词分布φ确定具体词，所以上述式子等价于下述式子所表达的**联合概率分布**![](https://img-blog.csdn.net/20141121101528765)：

![](../../.gitbook/assets/image%20%2810%29.png)

 其中，**第一项因子**![](https://img-blog.csdn.net/20141121101735203)**表示的是根据确定的主题**![](https://img-blog.csdn.net/20141121102832253)**和词分布的先验分布参数**![](https://img-blog.csdn.net/20141117160531515)**采样词的过程，第二项因子**![](https://img-blog.csdn.net/20141121101731716)**是根据主题分布的先验分布参数**![](https://img-blog.csdn.net/20141117160438989)**采样主题的过程，这两项因子是需要计算的两个未知参数**。

![](../../.gitbook/assets/image%20%289%29.png)

 接下来，**有了联合分布**![](https://img-blog.csdn.net/20141121101528765)**，咱们便可以通过联合分布来计算在给定可观测变量 w 下的隐变量 z 的条件分布（后验分布）**![](https://img-blog.csdn.net/20141124000913687)**来进行贝叶斯分析**。

![](../../.gitbook/assets/image%20%2833%29.png)

 最后一步，便是根据Markov链的状态![](https://img-blog.csdn.net/20141121103415953)获取主题分布的参数Θ和词分布的参数Φ。

即通过对一个主题中的词抽样，不断循环这个过程，最后收敛之后，取出来的每个主题词分布就是后验。最后我们就得到了 收敛的 $$\theta_{mk} $$ , $$\varphi_{kt}$$。我们可以把Gibbs Sampling N个迭代完的结果取平均来做参数估计，这样的话模型质量更高。

然后topic-word矩阵就是我们要的频率矩阵，也就是LDA模型。

有了LDA模型，对于新来的文档，我们可以对该文档做topic语义分布的计算。基本上inference的过程跟training的过程十分相似。对于新的文档，我们只要认为Gibbs Sampling公式中的 $$\theta_{kt} $$ 是不变的，是由训练语料得到的模型提供的，所以采样过程中我们只用统计该文档中topic分布就可以了

LDA inference:

1. 随机初始化，对当前文档中的每个词 $$w$$ , 随机赋一个Topic的编号 $$z$$ .
2. 重新扫描当前文档，按照Gibbs Sampling的公司，对每个词 $$w$$ ，重新采样它的topic.
3. 重复以上过程知道Gibbs Sampling收敛
4. 统计文档中的topic分布，这分布就是新文档的topic分布。



LDA如何调参：

LDA中的主要超参数有alpha, beta, K topic个数。其中alpha, beta可以是向量。

alpha 是 选择为 50/ k, 其中k是你选择的topic数，beta一般选为0.01吧，，这都是经验值，貌似效果比较好，收敛比较快一点



LDA中topic个数的确定是一个困难的问题。当各个topic之间的相似度的最小的时候，就可以算是找到了合适的topic个数。参考[一种基于密度的自适应最优LDA模型选择方法](https://link.zhihu.com/?target=http%3A//mcg.ict.ac.cn/download/pdf/paper/2008/32.%25E4%25B8%2580%25E7%25A7%258D%25E5%259F%25BA%25E4%25BA%258E%25E5%25AF%2586%25E5%25BA%25A6%25E7%259A%2584%25E8%2587%25AA%25E9%2580%2582%25E5%25BA%2594%25E6%259C%2580%25E4%25BC%2598LDA%25E6%25A8%25A1%25E5%259E%258B%25E9%2580%2589%25E6%258B%25A9%25E6%2596%25B9%25E6%25B3%2595.pdf) ，简略过程如下：

1. 选取初始K值，得到初始模型，计算各topic之间的相似度
2. 增加或减少K的值，重新训练得到模型，再次计算topic之间的相似度
3. 重复第二步直到得到最优的K



正如分类问题用Accuracy来评价，LDA也自己评价标准叫Perplexity。Perplexity（混乱）可以粗略的理解为“对于一篇文章，我们的LDA模型有多**不确定**它是属于某个topic的”。topic越多，Perplexity越小，但是越容易overfitting。我们利用Model Selection找到Perplexity又好，topic个数又少的topic数量。可以画出Perplexity vs num of topics曲线，找到满足要求的点。  
  












