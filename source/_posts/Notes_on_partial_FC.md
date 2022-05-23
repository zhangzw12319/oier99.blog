---
title: Partial FC--Training 10 Million Identities on a Single Machine[阅读笔记]
author: Oier99
banner_img:
index_img: https://i.loli.net/2021/08/15/43dKpjCLtfSJ16v.png
date: 2021-08-14 22:03:18
categories:
- [论文阅读, 分类器]
tags:
- Model Parallel
comment: true
math: true
mathjax: true
mermaid: true
excerpt: 对于分类ID数量特别多的时候能节省计算量，减小显存开销有效的方法，多人推荐。用在Insight-face模型上
sticky: 20
---

# Partial FC--Training 10 Million Identities on a Single Machine[阅读笔记]

[TOC]

## Motivation

1. 传统的DataParallel模式，无法解决大数据集(包含几十万至千万ID, 千万至亿个训练样本)训练时，分类器的矩阵参数$W_{NK \times d}$爆显存的问题($N$是Batch数量，$K$是GPU个数，d是Feature Map的维度)
2. ModelParallel模式能够有效解决1中问题：通过将矩阵$W$按$N$的维度拆分成多个子矩阵放在不同GPU上即可。但是该模式无法解决$logits_{N \times C}$当$C$很大时爆显存的问题
3. 本文提出的解决方式：保留一个Batch中所有的Positive Class， 随机采样Negative Class，并证明采样率较低情况下，仍能保持performance几乎无损。

4. Related Work(只是听作者介绍，没看):

 - HF-softmax(Goodman, 2001)[^1] 通过对FeatureMap构建随机hash森林，每次检索最近的class center来获得active class subset
	缺点： ①class center 存储在RAM中 ②计算feature retrieval也要耗时

 - Softmax Dissection(He et al.2020)[^2] 将softmax分成了intra-class objective和inter-class objective两部分，并且通过减低intra-class objective的计算冗余

	缺点：①难以拓展到其他softmax based方法

## Theorem&Model

1. softmax公式
	$$
	\sigma (X, i) = \frac{e^{w_i^T X}}{\sum_{j=1}^C e^{w_j^T X}}
	$$
	分子可以在GPU-i上算，只要batch大小不会导致爆显存。分母的话每个GPU只需要提供一个scalar，代表一个求和。

2. Model Parallel 在第i块GPU上的算法：

<img src="https://i.loli.net/2021/08/15/dgfnUjzxpqQGVke.png" alt="image-20210717092711902" style="zoom:50%;" />

注解:

- Line 2, `allgather`是因为同时要使用DataParallel来训练模型
- Line7, `allreduce`是因为对参数$W$实行ModelParallel,要从不同GPU上reduce $\sum e^{logtits_i}$



3. 随机选取Negative Class的方法：

	<img src="https://i.loli.net/2021/08/15/MYaywVFGzf9IeEW.png" alt="image-20210717093753863" style="zoom:50%;" />
	<img src="https://i.loli.net/2021/08/15/1tEZPeDjrLW8Gwi.png" alt="image-20210717093818660" style="zoom:50%;" />

4. 

## Contribution

暂略(以后想到了再写)

## Evaluation

1. Training Dataset, Validation Dataset, Testing Dataset分别是啥？Backbone? 损失函数？优化器？参数设置？
	Training Dataset CASIA, MS1MV2, Celab-500k
	Testing Dataset LFW(CPLFW, CFLFW), CFP-FP, AgeDB30,
	Backbone: Resnet-50, 100
	Mini-batch size = 512, 8 x 2080Ti
	LR: 0.1起步，后面有衰减(不同数据集不一样)

	训练次数：CASIA： 32K ； MS！MV2 180K； Glint360K 600K.

2. 自身Ablation

	比较不同的sample rate, 以及all-sample 和只对negative class sample
	评价指标：Average Cos Diatnce，因为使用了CosFace和Arc Face的损失函数，度量`$x_i$` ,`$W_{y_i}$`间的余弦距离
	<img src="https://i.loli.net/2021/08/15/43dKpjCLtfSJ16v.png" alt="image-20210717094807189" style="zoom:50%;" />

	<img src="https://i.loli.net/2021/08/15/r8xdvhPjUKLzR7O.png" alt="image-20210717094939172" style="zoom:50%;" />
	评估在不同的分类数量情况下的内存使用情况
	![image-20210717095831255](https://i.loli.net/2021/08/15/ywXRMfK24xJtrHc.png)

3. 和其他同类方法比较

<img src="https://i.loli.net/2021/08/15/1GxVTFIYbv9m5s3.png" alt="image-20210717095513744" style="zoom:50%;" />

<img src="https://i.loli.net/2021/08/15/nfsvX9QTZkBRDqa.png" alt="image-20210717095601380" style="zoom:50%;" />

4. 和其他不同类方法比较(看总榜)
	<img src="https://i.loli.net/2021/08/15/vXkL96DZQta4wbH.png" alt="image-20210717095254291" style="zoom:50%;" />

5. 该文章的长处和不足
	长处：
	① 在**ID量**特别大的时候，到达十几万甚至百万时，开一个较大的batch-size也不用担心爆GPU显存
	② 扔掉大部分negative class确实很节约训练时间，而且loss损失不大

	不足:
	① 在ID较少的数据集上用处不大(比赛9万ID用不到，sample rate=1)
	②只是随机的扔掉负样本比较粗糙，能不能有一些Mining Hard Negative？(但是要保证时间成本，保证存储Hard Negative Center 不需要耗费太多内存等)



6. 自己感觉可以改进的地方
	①其实结合分布式原语操作(primitive)中的ReduceAll，想要得到$logits$只需要统计部分信息，比如Max, Sum等，所以不扔掉负样本也能做。但是可能有些特殊情况还是要用到完整的$logits$

## 其他

搜一搜知乎评论，CSDN博客，查一查OpenReview；这些讨论，质疑对我的思维启发非常大的



## 参考文献

[^1]: Goodman, J. 2001. Classes for fast maximum entropy training. In *IEEE International Conference on Acoustics, Speech,* *and Signal Processing. Proceedings (Cat. No.01CH37221)*, volume 1, 561–564.
[^2]: He, L.; Wang, Z.; Li, Y.; and Wang, S. 2020. Softmax Dissection: Towards Understanding Intra- and Inter-class Objective for Embedding Learning. In *AAAI Conference on* *Artifificial Intelligence*, 10957–10964.
