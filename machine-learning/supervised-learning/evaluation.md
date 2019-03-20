# Evaluation

{% embed url="https://blog.csdn.net/heyongluoyao8/article/details/49408319" %}

超参数的调优是一个相当复杂与繁琐的任务。在模型原型设计阶段，需要尝试不同的模型、不同的超参数意见不同的特征集，我们需要寻找一个最优的超参数，因此需要使用相关的搜索算法去寻找，如格搜索（grid search）、随机搜索（random search）以及启发式搜索（smart search）等。这些搜索算法是从超参数空间中寻找一个最优的值。

当模型使用离线数据训练好并满足要求后，就需要将模型使用新的在线数据进行上线测试，这就是所谓的在线测试。在线测试不同于离线测试，有着不同的测试方法以及评价指标。最常见的便是A/B testing，它是一种统计假设检验方法。不过，在进行A/B testing的时候，会遇到很多陷阱与挑战，具体会在本文后面进行详细介绍。另一个相对使用较小的在线测试方法是multiarmed bandits。在某些情况下，它比A/B testing的效果要好。后面会进行具体讲解。

#### 评价指标\(Evaluation metrics\) <a id="&#x8BC4;&#x4EF7;&#x6307;&#x6807;evaluation-metrics"></a>

评价指标是机器学习任务中非常重要的一环。不同的机器学习任务有着不同的评价指标，同时同一种机器学习任务也有着不同的评价指标，每个指标的着重点不一样。如分类（classification）、回归（regression）、排序（ranking）、聚类（clustering）、热门主题模型（topic modeling）、推荐（recommendation）等。并且很多指标可以对多种不同的机器学习模型进行评价，如精确率－召回率（precision-recall），可以用在分类、推荐、排序等中。像分类、回归、排序都是监督式机器学习，本文的重点便是监督式机器学习的一些评价指标。

**准确率\(Accuracy\)**

  准确率是指在分类中，使用测试集对模型进行分类，分类正确的记录个数占总记录个数的比例：

  $$accuracy = \frac{n_{correct}}{n_{total}}$$   
  准确率看起来非常简单。然而，准确率评价指标没有对不同类别进行区分，即其平等对待每个类别。但是这种评价有时是不够的，比如有时要看类别0与类别1下分类错误的各自个数，因为不同类别下分类错误的代价不同，即对不同类别的偏向不同，比如有句话为“宁可错杀一万，不可放过一千“就是这个道理，例如在病患诊断中，诊断患有癌症实际上却未患癌症（False Positive）与诊断未患有癌症的实际上却患有癌症（False Negative）的这两种情况的重要性不一样。。另一个原因是，可能数据分布不平衡，即有的类别下的样本过多，有的类别下的样本个数过少，两类个数相差较大。这样，样本占大部分的类别主导了准确率的计算，为了解决这个问题，对准确率进行改进，得到平均准确率。

**平均准确率\(Average Per-class Accuracy\)**

  为了应对每个类别下样本的个数不一样的情况，对准确率进行变种，计算每个类别下的准确率，然后再计算它们的平均值。举例，类别0的准确率为80%，类别1下的准确率为97.5%，那么平均准确率为\(80%+97.5%\)/2=88.75%。因为每个类别下类别的样本个数不一样，即计算每个类别的准确率时，分母不一样，则平均准确率不等于准确率，如果每个类别下的样本个数一样，则平均准确率与准确率相等。   
  平均准确率也有自己的缺点，比如，如果存在某个类别，类别的样本个数很少，那么使用测试集进行测试时（如k-fold cross validation），可能造成该类别准确率的方差过大，意味着该类别的准确率可靠性不强。

**对数损失函数\(Log-loss\) = logistic loss**

  在分类输出中，若输出不再是0-1，而是实数值，即属于每个类别的概率，那么可以使用Log-loss对分类结果进行评价。这个输出概率表示该记录所属的其对应的类别的置信度。比如如果样本本属于类别0，但是分类器则输出其属于类别1的概率为0.51，那么这种情况认为分类器出错了。该概率接近了分类器的分类的边界概率0.5。Log-loss是一个软的分类准确率度量方法，使用概率来表示其所属的类别的置信度。Log-loss具体的数学表达式为： 

$$log\_loss=-\frac{1}{N}\sum_{i=1}^{N}y_i log p_i + (1-y_i)log(1-p_i)$$ 

* **cross entropy和KL-divergence作为目标函数效果是一样的，从数学上来说相差一个常数。**
* **logistic loss 是cross entropy的一个特例**

#### 1. cross entropy和KL-divergence <a id="1-cross-entropy&#x548C;kl-divergence"></a>

假设两个概率分布 $$p(x)$$ 和 $$q(x)$$ ， $$H(p,q)$$ 为cross entropy， $$D_{KL}(p|q)$$ 为 KL divergence。

**交叉熵的定义：** $$H(p,q)=-\sum_xp(x) \log {q(x)}$$ 

**KL divergence的定义：** $$D_{KL}(p|q)=\sum _xp(x)\log  \frac{ p(x)}  {q(x)}$$ 

**推导：**

 ****$$\begin{align}  D_{KL}(p|q) & = \sum _xp(x)\log  \frac{ p(x)}  {q(x)} \\  & = \sum_x(p(x)\log p(x)-p(x)\log q(x))\\   & =-H(p)-\sum_xp(x) \log q(x)\\  & = -H(p)+H(p,q) \\  \end{align}$$ 

也就是说，cross entropy也可以定义为： ****$$H(p,q)=D_{KL}(p|q)+H(p)$$ 

**直观来说，由于p\(x\)是已知的分布，H\(p\)是个常数，cross entropy和KL divergence之间相差一个常数。**

#### 2. logistic loss 和cross entropy <a id="2-logistic-loss-&#x548C;cross-entropy"></a>

假设 $$p \in \{y,1-y\}$$ ， $$q \in \{ \hat y,1-\hat y \}$$ ， cross entropy可以写为logistic loss：

$$H(p,q)=-\sum_xp(x) \log {q(x)}=-y\log\hat y-(1-y)\log(1-\hat y)$$ 



**精确率-召回率\(Precision-Recall\)**

  精确率-召回率其实是两个评价指标。但是它们一般都是同时使用。精确率是指分类器分类正确的正样本的个数占该分类器所有分类为正样本个数的比例。召回率是指分类器分类正确的正样本个数占所有的正样本个数的比例。

> 实际上非常简单，**精确率**是针对我们**预测结果**而言的，它表示的是预测为正的样本中有多少是真正的正样本。那么预测为正就有两种可能了，一种就是把正类预测为正类\(TP\)，另一种就是把负类预测为正类\(FP\)，也就是  
> ![P  = \frac{TP}{TP+FP}](https://www.zhihu.com/equation?tex=P++%3D+%5Cfrac%7BTP%7D%7BTP%2BFP%7D)  
> 而**召回率**是针对我们原来的**样本**而言的，它表示的是样本中的正例有多少被预测正确了。那也有两种可能，一种是把原来的正类预测成正类\(TP\)，另一种就是把原来的正类预测为负类\(FN\)。  
> ![R = \frac{TP}{TP+FN}](https://www.zhihu.com/equation?tex=R+%3D+%5Cfrac%7BTP%7D%7BTP%2BFN%7D)

其实就是分母不同，一个分母是预测为正的样本数，另一个是原来样本中所有的正样本数。  
  


**F1-score：**

  F1-score为精确率与召回率的调和平均值，它的值更接近于Precision与Recall中较小的值。即：

$$F1=\frac{2*precision*recall}{precision+recall}$$ 



**AUC\(Area under the Curve\(Receiver Operating Characteristic, ROC\)\)**

  AUC的全称是Area under the Curve，即曲线下的面积，这条曲线便是ROC曲线，全称为the Receiver Operating Characteristic曲线，它最开始使用是上世纪50年代的电信号分析中，在1978年的“Basic Principles of ROC Analysis ”开始流行起来。ROC曲线描述分类器的True Positive Rate（TPR，分类器分类正确的正样本个数占总正样本个数的比例）与False Positive Rate（FPR，分类器分类错误的负样本个数占总负样本个数的比例）之间的变化关系。

一般来说，如果ROC是光滑的，那么基本可以判断没有太大的overfitting（比如图中0.2到0.4可能就有问题，但是样本太少了），这个时候调模型可以只看AUC，面积越大一般认为模型越好。

![](../../.gitbook/assets/image%20%2826%29.png)

_**注意： AUC只是表示曲线下的面积 也有AUC of precision-Recall**_

再说PRC， precision recall curve。和ROC一样，先看平滑不平滑（蓝线明显好些），在看谁上谁下（同一测试集上），一般来说，上面的比下面的好（绿线比红线好）。F1（计算公式略）当P和R接近就也越大，一般会画连接\(0,0\)和\(1,1\)的线，线和PRC重合的地方的F1是这条线最大的F1（光滑的情况下），此时的F1对于PRC就好象AUC对于ROC一样。**一个数字比一条线更方便调模型。**  
  


![](../../.gitbook/assets/image%20%289%29.png)

ROC和PR曲线可以用于衡量样本不平衡的情况。当Precision和recall的值差异很大时，你就不太能通过F1 Score来衡量了。



**混淆矩阵\(Confusion Matrix\)**

  混淆矩阵是对分类的结果进行详细描述的一个表，无论是分类正确还是错误，并且对不同的类别进行了区分，对于二分类则是一个2\*2的矩阵，对于n分类则是n\*n的矩阵。对于二分类，第一行是真实类别为“Positive”的记录个数（样本个数），第二行则是真实类别为“Negative”的记录个数，第一列是预测值为“Positive”的记录个数，第二列则是预测值为“Negative”的记录个数。如下表所示：

|  | Predicted as Positive | Predicted as Negative |
| :--- | :--- | :--- |
| Labeled as Positive | True Positive\(TP\) | False Negative\(FN\) |
| Labeled as Negative | False Positive\(FP\) | True Negative\(TN\) |

如上表，可以将结果分为四类：   
\* 真正\(True Positive, TP\)：被模型分类正确的正样本；   
\* 假负\(False Negative, FN\)：被模型分类错误的正样本；   
\* 假正\(False Positive, FP\)：被模型分类的负样本；   
\* 真负\(True Negative, TN\)：被模型分类正确的负样本；

进一步可以推出这些指标：

* 真正率\(True Positive Rate, TPR\)，又名灵敏度\(Sensitivity\)：分类正确的正样本个数占整个正样本个数的比例，即： $$TPR = \frac{TP}{TP+FN}$$ 
* 假负率\(False Negative Rate, FNR\)：分类错误的正样本的个数占正样本的个数的比例，即： $$FNR = \frac{FN}{TP+FN}$$ 
* 假正率\(False Positive Rate, FPR\)：分类错误的负样本个数占整个负样本个数的比例，即： $$FPR = \frac{FP}{FP+TN}$$ 
* 真负率\(True Negative Rate, TNR\)：分类正确的负样本的个数占负样本的个数的比例，即： $$TNR = \frac{TN}{FP+TN}$$ 

进一步，由混淆矩阵可以计算以下评价指标：准确率，精确率，召回率，F1-Score, ROC曲线





**回归评价指标**

  与分类不同的是，回归是对连续的实数值进行预测，即输出值是连续的实数值，而分类中是离散值。例如，给你历史股票价格，公司与市场的一些信息，需要你去预测将来一段时间内股票的价格走势。那么这个任务便是回归任务。对于回归模型的评价指标主要有以下几种：   
\* RMSE   
  回归模型中最常用的评价模型便是RMSE（root mean square error，平方根误差），其又被称为RMSD（root mean square deviation），其定义如下： $$RMSE = \sqrt{\frac{\sum_{i=0}^n(y_i-\hat{y_i})^2}{n}}$$ 

* Quantiles of Errors 

    为了改进RMSE的缺点，提高评价指标的鲁棒性，使用误差的分位数来代替，如中位数来代替平均数。假设100个数，最大的数再怎么改变，中位数也不会变，因此其对异常点具有鲁棒性。 

    在现实数据中，往往会存在异常点，并且模型可能对异常点拟合得并不好，因此提高评价指标的鲁棒性至关重要，于是可以使用中位数来替代平均数，如MAPE： 

其中， $$y_{i}$$ 是第i个样本的真实值， $$\hat{y_i}$$ 是第i个样本的预测值，n是样本的个数。该评价指标使用的便是欧式距离。 RMSE虽然广为使用，但是其存在一些缺点，因为它是使用平均误差，而平均值对异常点（outliers）较敏感，如果回归器对某个点的回归值很不理性，那么它的误差则较大，从而会对RMSE的值有较大影响，即平均值是非鲁棒的。

$$MAPE=median(|y_i-\hat{y_i}|/y_i)$$ 

MAPE是一个相对误差的中位数，当然也可以使用别的分位数。

* “Almost Crrect” Predictions 

    有时我们可以使用相对误差不超过设定的值来计算平均误差，如当 $$|y_i-\hat{y_i}|/y_i$$ 超过100%（具体的值要根据问题的实际情况）则认为其是一个异常点，，从而剔除这个异常点，将异常点剔除之后，再计算平均误差或者中位数误差来对模型进行评价。

  
**排序评价指标**

  排序任务指对对象集按照与输入的相关性进行排序并返回排序结果的过程。举例，我们在使用搜索引擎（如google，baidu）的时候，我们输入一个关键词或多个关键词，那么系统将按照相关性得分返回检索结果的页面。此时搜索引擎便是一个排序器。其实，排序也可以说是一个二分类问题。即将对象池中的对象分为与查询词相关的正类与不相关的负类。并且每一个对象都有一个得分，即其属于正类的置信度，然后按照这个置信度将正类进行排序并返回。   
  另一个与排序相关的例子便是个性化推荐引擎。个性化推荐引擎便是根据用户的历史行为信息或者元信息计算出每个用户当前有兴趣的项目，并为每个项目赋一个兴趣值，最好按照这个兴趣值进行排序，返回top n兴趣项目。 

$$precision = \frac{happy\ correct\ answers}{total\ items\ returned\ by\ ranker}$$ 

$$recall = \frac{happy\ correct\ answers}{total\ relevant\ items}$$ 

当我们改变top k中的k值时，便可以得到不同的精确率与召回率，那么我们可以通过改变k值而得到精确率曲线和召回率曲线。与ROC曲线一样，我们也需要一个定量的指标对其ROC曲线进行描述而来评价其对应的模型进行评价。可取多个k值，然后计算其评价的精确率与召回率。













