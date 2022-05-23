---
title: 一句话读论文:Panoptic-PHNet(CVPR2022)
index_img: https://s2.loli.net/2022/05/24/v7oqPuU2LfKQWFG.jpg
banner_img: https://s2.loli.net/2022/05/24/bYjlZzLXrH1PNAx.jpg
date: 2022-05-24 01:51:09
categories:
- [论文阅读, 点云, 全景分割, 2022]
tags: [一句话读论文系列, CVPR2022, 点云全景分割]
author: Yuki.N
comment: true
math: true
excerpt: NeRF首次闯入自动驾驶领域，而且要来就要来个大的。
---

#  PNF(CVPR 2022)

> 论文标题：Panoptic Neural Fields: A Semantic Object-Aware Neural Scene Representation(CVPR 2022)
> 论文地址：[https://arxiv.org/abs/2205.04334](https://arxiv.org/abs/2205.04334)
> 作者单位：Google Research, Georgia Tech, Simon Fraser University, Stanford University
> 代码地址：暂无
> 一句话读论文："We present Panoptic Neural Fields(PMF), and object-aware neural scene representation that decomposes a scene into a set of objects(things) and background(stuff)."

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=520 height=86 src="///music.163.com/outchain/player?type=2&id=22707001&auto=0&height=66"></iframe>

## **网络框架：**

![image-20220523191212464](https://s2.loli.net/2022/05/23/AiBE8Xg3cu5ql1w.png)

<center style="color:#C0C0C0;text-decoration:underline">图1 Overview of Panoptic Neural Field  </center>

![image-20220523191253241](https://s2.loli.net/2022/05/23/3rnZVSYfXNpMeib.png)

<center style="color:#C0C0C0;text-decoration:underline">图2 Dynamic Challenging 3D Scenes Description</center>



## **核心内容：**

大佬们请收下我的膝盖！！！
	
Motivation: 

- 把多用于室内场景的Nerf首次应用到室外自动驾驶场景中
- Nerf原先多用于View Synthesis ，图形学渲染，重建。本篇工作窥得大佬们的野心：想在室外自动驾驶场景中，把分类、语义分割、目标检测、目标追踪、全景分割、三维重建、深度估计、场景编辑与生成等一系列任务全部做到SOTA指标，从而让Nerf一统2D-3D视觉任务的天下。虽然本篇工作是初步的尝试，但是开辟了一个新的研究领域。
- 相比于之前在Nerf基础上各种incremental类型的工作，本篇工作提出一种室外场景通用类型的Nerf框架。主要分为stuff类别和thing类别，除了分别学习传统Nerf模型所需要的color, pose，density 等信息，还加入语义信息，最后将stuff类别与thing类别共同合成panoptic radiance field，用于各类下游任务。
- 在已有的语义分支+Nerf, Dynamics+Nerf等各种变体基础上，取消了共享的MLP网络，而是为每一种类别的物体instance设计小的MLP网络；此外在初始化上引入类别的先验信息，设计了category-specific meta-learned initialization

	本文的方法：在原版Nerf基础上，做如下变化

- Things类别：

	- 首先用RGB-only 3D Object Detector& Tracker 得到Bounding box track $T_k$(由一系列仿射变换矩阵组成)和语义类别$k$.
	- 对每个物体实例，用标准的Nerf网络提取特征，该网络是由time-invariant MLP组成(不是随时间变化而变化的RNN时序网络),得到包括color, pose, density等参数信息
	- 损失函数共同优化Nerf网络和$T_k$

- Stuff 类别：

	- 用单一的Nerf网络提取Stuff类别，此外还有网络分支学习每个Stuff pixel的语义类别

- Panoptic-Radiance Field

	- 对color,densiy等通道采取如下融合方式

	- $$
		c(x| \theta) = \mathbb{1}s(x)c_x(x|\theta) + \sum_kc_k(T^{-1}x|\theta)
		$$

- Render Panoptic-Radiance Fields

	- $$
		C(r|\theta) \sim \sum_{i=1}^Nw(t_i)f(\mathbf{r}(t_i)|\theta)
		$$

- Nerf中权重先验的获取

	- Bias initalization(设置stuff MLP的bias为-5，thing MLP的bias为0.1，因为真实室外场景中stuff volume大多数是空的，而thing volume大多数非空) 和 Meta-learn的方式(`FedAvg` 算法)

## **贡献点/创新性：**

- 见Motivation的第1-3条





## **实验结果：**

![image-20220523194617216](https://s2.loli.net/2022/05/23/xYOCDHST3kIguh9.png)<center style="color:#C0C0C0;text-decoration:underline">图5 实验结果1 </center>

![image-20220523194641296](https://s2.loli.net/2022/05/23/sowYT8tfqBILU1b.png)

<center style="color:#C0C0C0;text-decoration:underline">图6 实验结果2 </center>

![image-20220523194752533](https://s2.loli.net/2022/05/23/gkLWepDuo41ZQmO.png)

<center style="color:#C0C0C0;text-decoration:underline">图7 实验结果3 </center>

![image-20220523194819545](https://s2.loli.net/2022/05/23/xG91WXNegAr2Pj7.png)

<center style="color:#C0C0C0;text-decoration:underline">图8 实验结果4 </center>

![image-20220523194847881](https://s2.loli.net/2022/05/23/ZLzw3K8InV62dcv.png)

<center style="color:#C0C0C0;text-decoration:underline">图9 实验结果5 </center>

## **Related Work(可选, 后续再补充):**

- Nerfs
- Nerfs with Semantics
- Nerfs with dynamics
- Nerfs with object decompositions
- Conditional NeRFs
- MVS
- SLAM

## **你认为优点/不足/可以拓展改进的地方(可选):**

优点：

- 太多了吐槽不完

缺点：

- 虽然很大一统，但是整个框架挺复杂，目前只能在离线的训练和推理，不太容易直接应用在实时场景下。



## **其他笔记:**

- CVer 计算机视觉：https://zhuanlan.zhihu.com/p/513499887
