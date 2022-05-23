---
title: 一句话读论文_Panoptic-PHNet_CVPR2022
index_img: https://s2.loli.net/2022/05/24/v7oqPuU2LfKQWFG.jpg
banner_img: https://s2.loli.net/2022/05/24/bYjlZzLXrH1PNAx.jpg
date: 2022-05-24 01:51:09
categories:
- [论文阅读, 点云, 全景分割, 2022]
tags: [一句话读论文系列, CVPR2022, 点云全景分割]
author: Yuki.N
comment: true
math: true
mermaid: true
excerpt: 这是一句话读论文系列的模板
---

> 论文标题：Panoptic Neural Fields: A Semantic Object-Aware Neural Scene Representation(CVPR 2022)
> 论文地址：[https://arxiv.org/abs/2205.04334](https://arxiv.org/abs/2205.04334)
> 作者单位：Google Research, Georgia Tech, Simon Fraser University, Stanford University
> 代码地址：暂无
> 一句话读论文："We present Panoptic Neural Fields(PMF), and object-aware neural scene representation that decomposes a scene into a set of objects(things) and background(stuff)."

# 阅读模板

## 这是一个二级目录


这是一段公式

$$
\begin{align}f(x_i^p, x_j^p) &= \exp\{u(x_i^p)^Tv(x_j^p) \} \\​\alpha_{i,j}^p &= \frac{f(x_i^p, x_j^p)}{\sum_{\forall j}f(x_i^p, x_j^p) }\end{align}
$$

这是一段代码

```python
if "__name__"=="__main":
	print("Hello world!")
```




{% mermaid %}
classDiagram

Class01 <|-- AveryLongClass : Cool
Class03 *-- Class04
Class05 o-- Class06
Class07 .. Class08
Class09 --> C2 : Where am i?
Class09 --* C3
Class09 --|> Class07
Class07 : equals()
Class07 : Object[] elementData
Class01 : size()
Class01 : int chimp
Class01 : int gorilla
Class08 <--> C2: Cool
{% endmermaid %}

{% mermaid %}
gantt
dateFormat  YYYY-MM-DD
title Adding GANTT diagram to mermaid

section A section
Completed task            :done,    des1, 2014-01-06,2014-01-08
Active task               :active,  des2, 2014-01-09, 3d
Future task               :         des3, after des2, 5d
Future task2               :         des4, after des3, 5d
{% endmermaid %}

{% note warning %}

这是一段`warning`

{% endnote %}



这是一段{% label warning @行内`warning`标签 %}



