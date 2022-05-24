---
title: 论文十问:DeepFusion(CVPR2022)
date: 2022-05-24 02:25:12
index_img: https://s2.loli.net/2022/05/24/ISACMOZynhfdwYv.jpg
banner_img: https://s2.loli.net/2022/05/24/eq9zvxbYNaPl3mL.png
categories:
- [论文阅读, 点云, 多模态融合, 2022]
tags: [论文十问系列, CVPR2022, 多模态，点云目标检测]
author: Yuki.N
comment: true
math: true
mermaid: true
excerpt: 数据增强与多模态融合历来是提升模型表现性能的两大重要手段。但是在自动驾驶场景下，LiDAR点云模态与RGB图像模态分别进行数据增强后会破坏两者间原有的几何对应关系，造成特征网络无法有效学习到一致的区域，从而造成性能损失。本文着力解决二者的inconsistency问题。
---

# DeepFusion(CVPR 2022)

> 论文标题：DeepFusion: Lidar-Camera Deep Fusion for Multi-Modal 3D Object Detection<br>
> 论文地址：[https://arxiv.org/abs/2203.08195](https://arxiv.org/abs/2203.08195)<br>
> 作者单位：Johns Hopkins University, Google<br>
> 代码地址：[https://github.com/tensorflow/lingvo](https://github.com/tensorflow/lingvo)<br>
> 一句话读论文：This study points out the key role of transformed feature alignment process that plays in multi-modal fusion module, and thus proposes InverseAug and LearnableAlign module to overcome incosistency between data augmentation and multi-modal fusion.

## Q1

论文试图解决什么问题？

本工作试图解决RGB图像-LiDAR点云网络，由于图像和点云分别进行数据增强操作(如随机旋转)，而导致模态特征之间的对应关系被破坏，使得多模态学习带来的增益被削弱的问题。

## Q2

这是否是一个新的问题？

这是一个比较有意思的，也很实用的新问题
1.因为大规模LiDAR点云数据需要大量的数据增强操作利于刷榜，如果多模态与之有冲突，那么提点效果会被大幅降低。
2.2020年前的多模态融合多是RGB图像-点云伪图像(环形投影，BeV, 透视投影等)的融合，本质是2D-2D网络间的融合。而2021年开始有更多3D-2D网络的多模态模型，因此在这个背景下考虑数据增强和特征对齐的冲突问题，还是比较有意思的

## Q3

这篇文章要验证一个什么科学假设？

1.特征对齐对多模态发挥效果很重要(参考Table1,9) -> 提出InverseAug
\2. 深层网络的特征向量在不同模态间对齐，对模型学习语义信息有利 -> 提出基于注意力机制的融合方式

## Q4

有哪些相关研究？如何归类？谁是这一课题在领域内值得关注的研究员？

\1. Input-Level Decoration:
在原始数据层面,利用图形学中地仿射变换与投影，将LiDAR点与Pixel对应。相关工作有：
PointPainting(CVPR 2021),
PointAugmentation(CVPR 2021),
PMF(ICCV 2021)

\2. Mid-Level Fusion:
在网络结构层面，对每一层的特征向量隐式融合。相关工作有：
Deep Continuous Fusion(ECCV 2018)
EP-Net(CVPR 2018),
4D-Net(ICCV 2021),
Cross view Transformer for real-time Map-view Semantic Segmentation(CVPR 2022)
TransFusion(CVPR 2022)等

## Q5

论文中提到的解决方案之关键是什么？

\1. InverseAug: 把图像和点云分支的数据增强操作取逆，再用仿射变换投影。

\2. LearnableAlign: 比较常见的Attention的融合方式

## Q6

论文中的实验是如何设计的？

略………………

## Q7

用于定量评估的数据集是什么？代码有没有开源？

Waymo 。开源。

## Q8

论文中的实验及结果有没有很好地支持需要验证的科学假设？

有，比较好。
1.实验效果比较solid: 在各大主流目标检测方法上，提升了6-8%左右(LEVEL 2)。
2.可视化结果也很好地验证科学猜想。

## Q9

这篇论文到底有什么贡献？

同时考虑多模态融合与数据增强之间的协同作用，并且从原始数据和网络结构两个层面，提出简单有效的方法，较好地解决冲突并验证猜想。
Motivation有新意，实验效果比较solid, 通用价值大。

## Q10

下一步呢？有什么工作可以继续深入？

\1. 对于不可逆的数据增强操作，比如用于图像的RandomCrop, RandomErasing, 必然造成图像与点云在几何层面无法对应。原文中只能忽略这些增强操作，或者等对齐模块后单独加入不可逆的数据增强操作。

\2. 如实例分割、全景分割任务中，有一些对于实例的数据增强操作，如从其他场景中随机复制一些实例点到另外的场景，那么图像中是否需要对应生成一些假的物体pixel呢？若存在遮挡关系又如何处理？

\3. 方法相对简单一些，后续工作或许能继续深入挖掘。
