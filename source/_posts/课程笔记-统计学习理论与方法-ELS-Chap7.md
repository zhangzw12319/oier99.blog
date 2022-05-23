---
title: 课程笔记-统计学习理论与方法-ELS-Chap7
date: 2021-11-11 00:32:57
index_img: https://i.loli.net/2021/09/30/tfhTo6NrOJKRikm.jpg
banner_img: https://i.loli.net/2021/09/30/tfhTo6NrOJKRikm.jpg
categories: 
- [课程笔记, 统计学习理论与方法]
- [教材笔记, Elements of Statistical Learning]
tags: [课程笔记, 教材笔记, 统计学习理论与方法, ELS]
author: oier99
comment: true
math: true
mermaid: true
excerpt: 整理了三遍，前前后后大概一共花了20个小时左右吧，虽然离完美还差很多，但形成了一套自己的东西。
---

# 课程笔记：统计学习理论与方法（ELS_Chap7）

📚书籍：《Elements of Statistical Learning》Chap 7



## 两个概念

1. 模型选择(Model Selection):  模型由参数控制的，模型选择既包括模型类型选择，也包括参数的控制。后面讲贝叶斯信息准则时(BIC)会讲到。
2. 模型评估(Model Assessment):  给定一个模型，评估其训练误差(In-sample Error)，测试误差(Extra-sample Error)，泛化误差(Generalization Error)。评估训练误差与测试误差之间的差距Bound.

两者都是侧重对模型的泛化误差进行评估，而非模型的训练误差。泛化误差是整个统计学习中最核心的关注问题。


## 训练误差与泛化误差

训练误差： 
$$
\overline{\text{err}} = \frac{1}{N} \sum_{i=1}^N L(y_i, \hat{f}(x_i))
$$
泛化误差：
$$
\text{Err}(y_i, \hat{f}(x_i)) = E_{(X,Y) \sim \tau}(L(y_i, \hat{f}(x_i)) |\tau)
$$
其中损失函数通常是:

- 均方误差$$L = (y_i - \hat{f}(x_i))^2 $$
- 对数极大似然函数【用于多分类】(严格来说这不算损失函数，但是极大似然最大等价于加符号最小，所以可以写成相同形式):$$L = -2\cdot[\sum_{k=1}^K I(G=k)\log(\hat{\Pr}(\hat{G}=k)] $$.其中$$I(G=k)$$相当于真实标签(Ground Truth).
- 对数极大似然的特殊情况【0-1分类】： $$L = I(G=1)\log(\hat{\Pr}) + (1-I(G=1))\log(1-\hat{\Pr})$$

{% note primary%}

📢注意，我们算误差时的Ground Truth(GT) $$y$$并不一定是真实的标签，因为获取数据的过程中无法避免有噪声存在(就比如用精密物理仪器测量的结果总会有无法避免的系统误差)。我们的损失函数是让模型的估计值$$\hat{f}$$和GT算误差，不是和$$f(x)$$算误差。

{% endnote %}

## Bias-variance 分解

假设：$$\{(x_i,y_i)\}$$ 是从某个数据分布中采样得到的某个数据集$$\tau$$。数据的真实分布是$$y = f(x) + \epsilon$$，数据的真实标签是$$f(x)$$，但是我们获取数据集时总会有噪声$$\epsilon$$干扰。通常假设噪声服从均值为0的某个高斯分布。$$\epsilon \sim N(0, \sigma_{\epsilon}^2)$$



考察在$$X=x_0$$一点上的单点泛化误差，其中求期望操作$$E$$是对所有的数据集$$\tau$$求的期望(Expectation over all the dataset $$\tau$$).<a name="t1">也就是说在这里，$\hat{f}(x_0)$也是随机变量，它的随机性来源于可能选取不同的数据集$\tau$ ；而$f(x_0)$的随机性只来源于$\epsilon$，二者独立无关联</a>。
$$
\begin{align*}
E(L(Y, \hat{f}(X))|X=x_0, Y=y_0 )&= (y_0 - f(x_0)) \,\,\,\text{(这里采用均方误差分析，其他同理)}\\
&= E(f(x_0) - \hat{f}(x_0) + \epsilon)^2 \\
&= E(f(x_0) - \hat{f}(x_0))^2 + E(\epsilon)^2 + 2E(f(x_0) - \hat{f}(x_0))E(\epsilon)\,\,\,\text{($\epsilon$ 与 $f(x_0) - \hat{f(x_0)}$ 独立)} \\
&=  E(f(x_0) - \hat{f}(x_0))^2 + \sigma_{\epsilon}^2 + 0 \\
&= E(f(x_0) - E\hat{f}(x_0) + E\hat{f}(x_0) - \hat{f}(x_0))^2 + \sigma_{\epsilon}^2 \\
&= E(f(x_0) - E\hat{f}(x_0))^2 + E(\hat{f}(x_0) - \hat{f}(x_0))^2 + 2E(f(x_0) - E\hat{f}(x_0))\cdot 0 + \sigma_{\epsilon}^2\\
&= E(f(x_0) - E\hat{f}(x_0))^2 + E(\hat{f}(x_0) - \hat{f}(x_0))^2  + \sigma_{\epsilon}^2 \\
&= \text{bias}^2 + \text{variance} + \sigma_{\epsilon}^2
\end{align*}
$$



{% note info %}

关于期望与方差的常用性质，请参见这篇[博客](https://www.oier99.cn/2021/11/10/随笔-期望与方差的性质/).

{% endnote%}



### KNN的例子

KNN的模型是$$\hat{f}(x_0) = \frac{1}{K}\sum_{i=1}^K y_i,\, x_i \in n_K(x_0)$$.
$$
\begin{align*}
\hat{f}(x_0) &= \frac{1}{K}\sum_{i=1}^K y_i \\
&= \frac{1}{K} \sum_{i=1}^K(f(x_i) + \epsilon_i ) \\
&\approx \frac{1}{K} \sum_{i=1}^K(f(x_0) + \epsilon_i ) \\
&= f(x_0) + \frac{1}{K} \sum_{i=1}^K \epsilon_i
\end{align*}
$$
为了计算方差方便， 在理论推导这里做了一个重要近似：因为KNN取的是K个近邻点来插值估计，所以假设认为他们的“本源”$$f(x_i) \approx f(x_0)$$.这样，KNN的方差可以如下计算:
$$
\begin{align*}
\text{Var}(\hat{f}(x_0)) &= \text{Var} \frac{1}{K} \sum_{i=1}^K \epsilon_i \\
&= \frac{1}{K^2} \text{Var}\sum_{i=1}^K \epsilon_i \\
&= \frac{1}{K^2} \sum_{i=1}^K \text{Var}(\epsilon_i) \\
&= \frac{1}{K^2} \sum_{i=1}^K \sigma_{\epsilon}^2 \\
&= \frac{1}{K} \sigma_{\epsilon}^2
\end{align*}
$$
故泛化误差拆分为:
$$
Err(y_0, \hat{f}(x_0)) \approx \sigma_{\epsilon}^2 + E(f(x_0) - \frac{1}{K}\sum_{i=1}^K y_i )^2 + \frac{1}{K} \sigma_{\epsilon}^2
$$
可以看出$$K$$越小，模型复杂度越大，方差越大，bias应该会越小。

### 线性回归的例子

对于线性回归函数$$\hat{f}(x) = \hat{\beta}^T x $$, 解最小二乘误差下的最佳近似参数是$$\hat{\beta} = (X^TX)^{-1}X^Ty$$

故$$\hat{f}(x) = y^T X(X^TX)^{-1}x = x^T X(X^TX)^-1X^Ty = h(x)y$$.可以看出$$\hat{f}(x)$$的随机性来源于y，即来源于$$\epsilon$$ .（这与[刚才](#t1)说法不矛盾。因为之前对$$\hat{f}$$的分析是抽象的符号，而这里是对线性回归具体公式分析）
$$
\text{var}(\hat{f}(x_0)) = ||h(x_0)||^2 \sigma_{\epsilon}^2
$$
故
$$
Err(y_0, \hat{f}(x_0)) = \sigma_{\epsilon}^2 + E(f(x_0) - \hat{\beta}^Tx_0 )^2 + ||h(x_0)||^2 \sigma_{\epsilon}^2
$$


训练误差:
$$
\frac{1}{N}\sum_{i=1}^N Err(y_0, \hat{f}(x_0)) = \sigma_{\epsilon}^2 + \sum_{i=1}^NE(f(x_0) - \hat{\beta}^Tx_0 )^2 + \frac{p}{N}\sigma_{\epsilon}^2
$$
可以看出模型复杂度由数据量$$N$$和参数量$$p$$共同控制。

{% note primary %}

（这部分的推导需要用到矩阵的迹的性质）

$$\text{tr}(ABC) = \text{tr}(BCA) = \text{tr}(CAB)$$

$$\sum_{i}(x_i y_i) = x^Ty = \text{tr} (xy^T)$$

{%endnote%}



## 乐观度

乐观度(Optimisim)的概念主要是为了比较模型训练误差与泛化误差之间的差距，或者如何用训练误差去估计泛化误差。

直接计算训练误差和泛化误差的差有困难，因为模型输入$$x$$都不固定。所以可以采用重采样的技术，原先训练集$$(x,y)$$,是训练时采样得到的标签，记为$$y$$；重采样是对相同的$$x$$, 再次采样$$y^{\text{New}}$$。
$$
\text{Err}_{in}(y_i, \hat{f}(x_i)) = \frac{1}{N}\sum_{i=1}^N E_{Y^{\text{new}}}[L(Y_i^{\text{New}}, \hat{f}(x_i))]
$$

$$
\overline{err} = \frac{1}{N} \sum_{i=1}^N L(y, \hat{f}(x_i))
$$



结论
$$
\begin{align*}
	w &= E_y(op) \\
	&= \frac{2}{N}\text{Cov}(y, \hat{y})
\end{align*}
$$
证明过程后续再补。



若$$\hat{y}$$是由参数量为$$d$$线性回归得到的估计，那么
$$
\text{Cov}(y, \hat{y}) = d \sigma_{\epsilon}^2
$$
可得到
$$
E_y(\text{Err}_{in}) = E_y(\overline{\text{err}}) + 2\cdot\frac{d}{N} \sigma_{\epsilon}^2
$$


## 有效参数量

$$
\hat{y} = Sy
$$

有效参数数量(Effective Number of Parameters):
$$
\text{df}(S) = \text{tr}(S)
$$
对于线性回归，有如下关系：
$$
\sum_{i=1} ^N \text{Cov}(y_i, \hat{y}_i) = \text{df}(\hat{y}) \cdot  \sigma_{\epsilon}^2
$$

## 贝叶斯信息量（BIC）

题外话：前面的部分主要讲述的模型评价(Model Assesment)部分，贝叶斯信息量主要讲述的是模型选择的部分

BIC for 极大似然回归
$$
BIC = -2 \cdot loglik + (\log N) \cdot d
$$
BIC under Gaussian Model
$$
BIC = \frac{N}{\sigma_{\epsilon}^2}[\overline{\text{err}}+ (\log N)\cdot \frac{d}{N} \sigma_{\epsilon}^2]
$$
他的Motivation是源自贝叶斯派的思想(下面手抄草稿，由于过程有点难，整理后还有很多错误比如符号上下标对不上)

![1](https://i.loli.net/2021/11/10/9qVUZlvD2MgstSo.jpg)

![2](https://i.loli.net/2021/11/10/yYAO547q1Nf39cM.jpg)

![3](https://i.loli.net/2021/11/10/uskaSvyOilJT8mU.jpg)



## 交叉验证(以后有空再补)

