# Word2Vec

{% embed url="https://zhuanlan.zhihu.com/p/29364112" %}

### word2vec 是word embedding 最好的工具吗？

| 优点 | 缺点 |
| :--- | :--- |
| 训练速度快（只有输入层和输出层） | 没有考虑语序，这里会有训练效果损失 |
| 易用，多种包中都有集成。 |  |
| 提速trick（Sigmoid，一次计算，词典Hash存储，层次Softmax） |  |

### word2vec 训练结果的差异主要来自什么因素？

### 2.1 语料影响最大

语料的场景，比如微博的语料和新闻语料训练的结果差别很大。因为微博属于个人发帖，比较随意。而新闻比较官方正式，另外新闻句式相对复杂。为什么会出现这种情况呢？因为 word2vec 的原理就是 一个词预测 前后词 或者 前后词 预测 当前词，使得概率最大化。

**2.1.1 相似的句子，相同部位的词 会相似。**

比如 句子1 w1 w2 w3 w4 X w5 w6 w7.

句子2 w1 w2 w3 w5 Y w5 w6 w7.

因为 X 的向量 受 w1 w2 w3 w4 w5 w6 w7 向量影响决定， Y也是受这几个词影响决定。

所以 X Y 是相似的。

**2.1.2 挨着近的词，也是相似的。**

比如 句子 w1 w2 w3 w4 X Y w5 w6 w7.  
这样 X Y 都是受到 来自 w1 w2 w3 w4 w5 w6 w7 向量影响决定。

所以X Y是相似的。

所以，微博和新闻的句子的整体分布是不一样的。 这里影响 结论 2.1.1.

其次，新闻长文多，句式复杂，微博短文多，这里影响结论2.1.2.

### 2.2 算法参数的影响。

算法参数对总体效果影响不大。相对来说，比较重要的参数有以下：

**2.2.1 降采样\(sub sampling\)**

降采样越低，对高频词越不利，对低频词有利。可以这么理解，本来高频词 词被迭代50次，低频词迭代10次，如果采样频率降低一半，高频词失去了25次迭代，而低频词只失去了5次。一般设置成le-5。个人觉得，降采样有类似tf-idf的功能，降低高频词对上下文影响的权重。

**2.2. 2 语言模型**

skip-gram 和cbow,之前有对比，切词效果偏重各不相同。  
从效果来看，感觉cbow对词频低的词更有利。这是因为 cbow是基于周围词来预测某个词，虽然这个词词频低，但是他是基于 周围词训练的基础上，通过算法来得到这个词的向量。通过周围词的影响，周围词训练的充分，这个词就会收益。

**2.2. 3 窗口大小**

窗口大小影响 词 和前后多少个词的关系，和语料中语句长度有关，建议可以统计一下语料中，句子长度的分布，再来设置window大小。一般设置成8。

从cbow的网络结构可以看出，模型输入的单词数量是不定长的，那在构造训练样本的时候应该如何选取预测单词附近的多少个单词作为输入呢？Mikolov认为_**离预测单词近的词语比那些远的单词更相关**_，所以采用了_**随机窗口大小的方式**_来选取，每次在区间\[1, window\]随机一个数值K，然后在预测单词的前后各选取k个单词作为输入。

window是可选参数大小，window增大可以使向量学习更充分，但同时也增加了训练的复杂度。

**2.2. 4 min-count**

最小词频训练阀值，这个根据训练语料大小设置，只有词频超过这个阀值的词才能被训练。

根据经验，如果切词效果不好，会切错一些词，比如 “在深圳”，毕竟切错的是少数情况，使得这种错词词频不高，可以通过设置相对大一点的 min-count 过滤掉切错的词。

**2.2. 5 向量维度**

如果词量大，训练得到的词向量还要做语义层面的叠加，比如 句子 的向量表示 用 词的向量叠加，为了有区分度，语义空间应该要设置大一些，所以维度要偏大。一般 情况下200维够用。

**2.2. 6 其他参数**

比如学习率 可以根据需要调。

### 3 word2vec 影响速度的因素有哪些？

### 3.1 语言模型：cbow 比skip-gram 更快

为什么 cbow更快，很重要的一个原因，cbow是基于周围词来预测这个单词本身 。而skip-gram是基于本身词去预测周围词。 那么，cbow只要 把窗口内的其他词相加一次作为输入来预测 一个单词。不管窗口多大，只需要一次运算。而skip-gram直接受窗口影响，窗口越大，需要预测的周围词越多。在训练中，通过调整窗口大小明显感觉到训练速度受到很大影响。

### 3.2 迭代次数

影响训练次数，语料不够的情况下，可以调大迭代次数。spark 版本有bug，迭代次数超过1，训练得到的词向量维度值超大。

### 3.3 线程数

单机版（google word2vec\)可以通过设置多线程跑,集群版（spark mllib）可以设置多个 partitions.但是从经验来看，在集群上设置partitions 过多，会影响训练的效果。

### 3.4 其他参数

采样频率 影响词的训练频率  
min-count 最小词频 影响 训练词的数量  
Window大小 影响 skip-gram 的 预测次数。  
向量维度 维度决定了训练过程中计算的维度

_**exp运算打表**_

计算softmax的时候需要求e的x次方，一轮迭代中指数运算至少需要上亿级别的指数运算，由于sigmod函数是个长“S”型的函数，可以通过对中间部分的x查表来取代多次指数运算。

### 4 怎样评估word2vec训练的好坏？

### 4.1 词聚类

可以采用 kmeans 聚类，看聚类簇的分布

### 4.2 词cos 相关性

查找cos相近的词

### 4.3 Analogy对比

a:b 与 c:d的cos距离 \(man-king woman-queen \)

### 4.4 使用tnse，pca等降维可视化展示



**Skip-gram与CBOW的比较**

skip gram的训练时间更长，但是对于一些出现频率不高的词，在CBOW中的学习效果就不日skipgram。反正mikolov自己说的skip准确率比CBOW高。。。



_**当用Word2vec处理长文本问题时：**_

序列数据不能过长，过长会导致**偏移现象**，训练的词向量会变差。其实就是用户注意力的问题，用时髦的话说就是attention。现在attention在lstm里混得风生水起。我当时拿到用户log后，先根据session进行数据切割，如果一个session过长，我会进行限制，只允许最大一个长度。尽量保证一个序列的主题\(attention\)基本一致。这一块还有很多可以优化，session的切分好像也有相关算法。数据没清洗干净，后期也很恼火。

当长文本都运用word2vec转换以后，需要对一段长文本的向量 进行一些聚类的运算，去除一些异常值，离群点。在进行下一步的运算。
