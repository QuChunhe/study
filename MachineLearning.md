[神经网络与深度学习 邱锡鹏](https://nndl.github.io/)


Conda (Anaconda)
```
source deactivate base
source activate base
```

numpy PyTorch  TensorRT mpi4py TensorFlow


```
conda list
conda -version
python --version
```

[Leo Breiman, Statistical Modeling: The Two Cultures](http://cda.psych.uiuc.edu/statistical_learning_course/breiman_two_cultures.pdf) 

https://www.itcodemonkey.com/article/15901.html

智能
* 抽象
* 演绎，学习已有经验和知识，并进一步的应用
* 归纳，通过特例，分析和总结经验
* 联想：将不相关的事件关联起来、
* 关联，
* 推理
* 类比，相关的事件和经验，能够进行关联和对比

人类的其他能力

* 本能，天生的或者经过反复训练具有的一些条件反射或者直觉。
* 记忆
* 尝试

[李沐的深度学习笔记来了](https://mp.weixin.qq.com/s?__biz=MzIyNjM2MzQyNg==&mid=2247623390&idx=1&sn=8b1df80bf7bc63ef240c5d8ba6ce9ba8&chksm=e87d3393df0aba858deafe2928d3fd5f95485e1d2d45485876efaf2a958aa5bd9e6a936fb98b&mpshare=1&scene=1&srcid=0804HXDZngMv97BJEXM5ZT6f&sharer_sharetime=1659585056484&sharer_shareid=6cf5f9bc7b3d07e703236236e2df3f84&exportkey=AXWqPjhZ3DQRsKl5A7mGi7I%3D&acctmode=0&pass_ticket=%2FfY4TB26JPF8DDrzCX37H4I3CK8FdSGChE92J%2FG34sOU5b6P4nl6JQ9TvfPeGuI0&wx_header=0#rd)

[TensorFlow Examples](https://github.com/aymericdamien/TensorFlow-Examples)





* 监督学习 Supervised Learning
* 无监督学习 Unsupervised Learning
* 强化学习 Reinforcement Learning

多数机器学习方法：human-designed representations and input features;
机器学习算法的作用主要是optimize weights，以便改善最终预测结果

[台湾大学教授李宏毅机器学习](https://www.bilibili.com/video/BV13B4y1E7yz?p=2&vd_source=3402e0cf5abe6a9fa6abe9997ddc0341)

Machine Learning = Looking for function


different types of functions
* Repression: the function outputs a scalar
* Classfication: Given options (classes), the function outputs the correct one.
* Structured Learning: create something with structure (image, document) 

训练过程training
1. Function with Unknown Parameters 写出具有未知参数的汉书
2. Define Loss from Training Data. 从训练数据定义损失函数 Loss is a function of parameters.
3. Optimization: 使用优化方法,使得损失函数最小化的参数



gradient descent: 

learning rate: hyperparameters 自己的定义的参数

* global minima
* local minima



All piecewise linear curves = constant + sum of a set of _/~

sigmoid function替换线性/

y= b + w*x1 (hard sigmoid)

y=b+\sum{ci * sigmoid(bi+wi*xi)}


batch
* 1 epoch = see all the batches once


Epoch（时期）：当一个完整的数据集通过了神经网络一次并且返回了一次，这个过程称为一次>epoch。（也就是说，所有训练样本在神经网络中都 进行了一次正向传播 和一次反向传播 ）再通俗一点，一个Epoch就是将所有训练样本训练一次的过程。

Batch（批 / 一批样本）：将整个训练样本分成若干个Batch。

Batch_Size（批大小）：每批样本的大小。

Iteration（一次迭代）：



# PyTorch

如何表示字符串
* One-hot [0,1,0,...]
* Embeding
   * word2vec
   * glove





```python
import torch
import numpy as np

torch.set_default_tensor_type(torch.DoubleTensor)

```
**中科院-统计学习基础**

All of Statistics - A Concise Course in Statistical Inference

样本空间/随机事件

随机变量

事件的概率-->随机变量的概率描述

随机变量X的累积分布函数F，cumulative distribution function: CDF


离散型随机变量的概率函数(probability function or probability mass function, pmf)概率质量函数

连续型随机变量的概率密度函数(probability density function,pdf)

uniform(a,b)

分位函数 quantile function

CDF的反函数

中位数或者中值 median

随机变量的变换



Discrete Uniform Distribution:X has a uniform distribution on {1, . . . , k}.

Bernoulli distribution written X ∼ Bernoulli(p).


Binomial random
variable and we write X ∼ Binomial(n, p).

X is a random variable; x denotes a particular value of the random variable; n and p
are parameters, that is, fixed real numbers. The parameter p is usually unknown
and must be estimated from data; that’s what statistical inference is all about.


X has a geometric distribution with parameter p ∈ (0, 1), written X ∼ Geom(p),

Think of X as the number of flips needed until the first head when flipping a
coin.

X has a Poisson distribution with parameter λ, written X ∼ Poisson(λ)

The Poisson is often used as a model for counts of rare events like radioactive
decay and traffic accidents.


X has a Normal (or Gaussian) distribution with
parameters μ and σ, denoted by X ∼ N(μ, σ2),

The Poisson is often used as a model for counts of rare events like radioactive
decay and traffic accidents.

X has an Exponential distribution with　parameter β, denoted by X ∼ Exp(β)．

joint mass　function

marginal mass function

marginal densities

多元分布  联合分布 边缘分布

条件独立

independent and identically distributed 独立同分布

The Law of Total Probability

Bayes’ Theorem

We call P(Ai) the prior probability of A and P(Ai|B) the posterior probability of A.



期望/均值：随机变量的平均值,一阶矩

大树定律：大量独立同分布样本的期望；The Rule of the Lazy Statistician

E(X)良好定义

期望的性质
* 线性运算
* 加分规则
* 乘法规则，相互独立的随机变量

平均数、中位数、众数（mode）

众数是出现次数最多的位置

期望、中位数和众数，高斯三者相等

The kth moment of X

方差：刻画随机变量围绕均值的散布程度

方差：两阶中心矩

standard deviation


sample mean（样本的均值），sample variance（样本的方差），确保无偏估计

协方差(Covariance)和相关系数




KL散度(Kullback-Leibler Divergence)是用来度量两个概率分布相似度的指标，

# 深度学习

人工神经元网络(ANN),简称神经网络.

激活函数（Activation Functions）的目标是，将神经网络非线性化。激活函数是连续的（continuous），且可导的（differential）。

常见的激活函数：sigmoid，tanh，relu。


sigmoid是平滑（smoothened）的阶梯函数（step function），可导（differentiable）。sigmoid可以将任何值转换为0~1概率，用于二分类


tanh,即双曲正切（hyperbolic tangent），类似于幅度增大sigmoid，将输入值转换为-1至1之间。tanh的导数取值范围在0至1之间，优于sigmoid的0至1/4，在一定程度上，减轻了梯度消失的问题。tanh的输出和输入能够保持非线性单调上升和下降关系，符合BP（back propagation）网络的梯度求解，容错性好，有界。


ReLU :即Rectified Linear Unit，整流线性单元，激活部分神经元，增加稀疏性，当x小于0时，输出值为0，当x大于0时，输出值为x.



https://www.jianshu.com/p/857d5859d2cc