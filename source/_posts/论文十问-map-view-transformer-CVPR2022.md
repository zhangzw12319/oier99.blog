---
title: 论文十问:Map-view Transformer(CVPR2022)
date: 2022-05-24 03:05:27
categories:
- [论文阅读, 点云, 多模态融合, 2022]
tags: [一句话读论文系列, CVPR2022, 点云全景分割]
author: Yuki.N
comment: true
math: true
mermaid: true
excerpt: 巧妙利用地图信息做自动驾驶场景下RV和BeV的融合。

---

> 论文标题：Cross-view Transformers for real-time Map-view Semantic Segmentation(CVPR 2022)
> 论文地址：[https://arxiv.org/abs/2205.02833](https://arxiv.org/abs/2205.02833)
> 作者单位：The Chinese University of Hong Kong
> 代码地址：[https://github.com/bradyz/ cross_view_transformers](https://github.com/bradyz/ cross_view_transformers)
> 一句话读论文：Our architecture implicitly learns a mapping from individual camera views into a canonical map-view representation using a camera-aware cross-view attention mechanism.
# Cross-view Transformers for real-time Map-view Semantic Segmentation(CVPR 2022)[2]

## Q1

论文试图解决什么问题？

做图像特征与地图特征的融合("model geometry and relationships between different view and a canonical map representation")

## Q2

这是否是一个新的问题？

利用地图信息作为query，参与语义分割网络的跨视图融合，是一个有新意的做法

## Q3

这篇文章要验证一个什么科学假设？

## Q4

有哪些相关研究？如何归类？谁是这一课题在领域内值得关注的研究员？

做俯视图语义分割，已有方法大致可归为如下两类(包含其存在的问题)
Image-based depth estimation are error-prone.
Depth-based projections are a fairly inflexible and rigid bottleneck to map between views.

附一份知乎笔记连接：https://zhuanlan.zhihu.com/p/511477453

## Q5

论文中提到的解决方案之关键是什么？

通过cross-view transoformer来做Camera View到Map View的融合。相比于已有方法基于显式地几何关系地映射，这种融合的方式是一种隐式函数的映射("learn any geometric transformation implicitly and directly from data")。此外，transformer需要positional embedding来区分不同空间位置的特征。本文因此设计了camera-aware和map-view两类positional embedding。

## Q6

论文中的实验是如何设计的？

## Q7

用于定量评估的数据集是什么？代码有没有开源？

nuScenes, 已经开源

## Q8

论文中的实验及结果有没有很好地支持需要验证的科学假设？

在俯视图的语义分割中是SOTA(37.5% mIoU), 和基于深度估计与投影等已有方法相比comaprable。但是整个赛道与图像语义分割与3D语义分割结果相比(70-80mIoU)，整体后面还有挖掘空间

## Q9

这篇论文到底有什么贡献？

1）利用了地图信息，这是一个比较有新意的setting.
2）注意力系数计算方式比较有新意，可以参考拓展

## Q10

下一步呢？有什么工作可以继续深入？

