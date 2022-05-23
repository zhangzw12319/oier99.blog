---
title: 随笔：那些在CV里用腻了的话术与说辞
date: 2021-10-09 22:00:53
index_img: https://i.loli.net/2021/09/25/Y6W8Ie54P1onyvA.jpg
banner_img: https://i.loli.net/2021/09/25/NGX9KzhdUfDwCx3.jpg
categories:
- [随笔]
tags: [CV, 话术]
author: oier99
comment: true
math: true
mermaid: true
excerpt: 究其根源，深度学习是一个黑盒子(Black Box)，缺乏一套能够解释清楚深度神经网络的运作机理的数学理论……很多搞深度学习应用的大多follow这样的研究路线：通过紧跟研究”热点“，读paper参会看别人提出了哪些模型，然后想到一个”灵感“，提出一套自己魔改的结构，抱着试一试的心态做实验发现work了，再来解释一通，就去投稿发paper。
---

# 随笔：那些在CV里用腻了的话术与说辞

究其根源，深度学习是一个黑盒子(Black Box)，缺乏一套能够解释清楚深度神经网络的运作机理的数学理论，比如，能否解释深度网络究竟从海量数据中学到了什么，深度网络的反向传播过程的收敛条件，训练深度模型为什么花费那么长时间，究竟有多少时间是对学习真正有用的。由于缺乏理论支撑，很多搞深度学习应用的(如CV, NLP)大多follow这样的研究路线：通过紧跟研究”热点“，读paper参会看别人提出了哪些模型，然后想到一个”灵感“，提出一套自己魔改的结构，抱着试一试的心态做实验发现work了，再来解释一通，就去投稿发paper。所以很多paper(尤其搞CV/NLP + DL)都是从性能结果反向解释自己的神经网络结构，并且很多解释是基于经验和直觉的。
    
读多了后，发现有一些话术是比较Common的技巧，就是很多工作都愿意用上这些技巧来提点，写作时用上相似的话术去讲故事，总觉一下就觉得比较有意思。以后有空会继续补充。

1. Multi-Resolution/Hierarchical/Pyramid Sturcture/Extract Feature at diferent scales
2. 不同层次/级别的特征如何融合：Feature Fusion
3. 分类问题/多模态问题/迁移学习问题: Intra-class variance & Inter-class Variance(最小化类内XXX，最大化类间XXX,以保留判别性信息)
4. Global Part + Local Part 的多分支设计
5. Local Discriminative Part
6. 粗粒度+细粒度(Coarse + Fine的设计)
7. Grouping操作，把相似的归纳到一起(比如聚类，相似度打分)，分类做loss
8. Feature Alignment, Domain Alignment, Pixel Alignment；各种Alignment
9. Meta Learning + 各种领域；就近年会议review情况来看，元学习快被用烂了(烂大街的感觉)，基本是所有reviewer都觉得没啥可用的。把他作为主要创新点容易被喷novelty不够。

(未完待续…)
