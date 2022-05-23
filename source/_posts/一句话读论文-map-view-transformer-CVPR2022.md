---
title: 一句话读论文:Map-view Transformer(CVPR2022)
date: 2022-05-24 02:55:31
index_img: https://s2.loli.net/2022/05/24/RPvkg6bLVEoyd2h.jpg
banner_img: https://s2.loli.net/2022/05/24/RPvkg6bLVEoyd2h.jpg
categories:
- [论文阅读, 点云, 多模态融合, 2022]
tags: [一句话读论文系列, CVPR2022, 点云全景分割]
author: Yuki.N
comment: true
math: true
mermaid: true
excerpt: 巧妙利用地图信息做自动驾驶场景下RV和BeV的融合
---

> 论文标题：Cross-view Transformers for real-time Map-view Semantic Segmentation(CVPR 2022)<br>
> 论文地址：[https://arxiv.org/abs/2205.02833](https://arxiv.org/abs/2205.02833)<br>
> 作者单位：The Chinese University of Hong Kong<br>
> 代码地址：[https://github.com/bradyz/ cross_view_transformers<br>](https://github.com/bradyz/ cross_view_transformers)
> 一句话读论文：Our architecture implicitly learns a mapping from individual camera views into a canonical map-view representation using a camera-aware cross-view attention mechanism. 

# Cross-view Transformers for real-time Map-view Semantic Segmentation(CVPR 2022)[1]


## 网络框架：

![image-20220523111833587](https://s2.loli.net/2022/05/24/okSpGdcwzAjVeiu.png)

## **核心内容：**

​	Motivation: 想做图像特征与地图特征的融合("model geometry and relationships between different view and a canonical map representation")

​	已有方法的问题：

- Image-based depth estimation are error-prone.
- Depth-based projections are a fairly inflexible and rigid bottleneck to map between views.

​	本文的思路：

​	是通过cross-view transoformer来做Map View 到Camera View的融合。相比于已有方法基于显式地几何关系地映射，这种融合的方式是一种隐式函数的映射("learn any geometric transformation implicitly and directly from data")。此外，transformer需要positional embedding来区分不同空间位置的特征。

​	注意力系数的计算方式比较巧妙：
$$
x^{(I)} \simeq K_k R_k(x^{(W)} - t_k)
$$
​	上述公式展示了世界坐标系$x^{(W)}$与相机坐标系$x^{(I)}$的映射关系，其中$t_k$是车辆在行驶时的平移，$K_k$与$R_k$分别是相机内参矩阵和外参旋转矩阵(相机位姿相对于LiDAR传感器位姿)。
$$
sim_k(x^{(I)}, x^{(W)}) = \frac{(R_K^{-1}K_K^{-1}x^{(I)})\cdot (x^{(W)} - t_k)}{\Vert (R_K^{-1}K_K^{-1}x^{(I)})\Vert \Vert (x^{(W)} - t_k)\Vert}
$$
​	这样将3D坐标点和2D图像对应的坐标联系起来，计算其相似度系数。由于本文中没有3D LiDAR点云数据参与，所以从地图中只能获得xy坐标的信息，无法获得高度(深度)信息。所以这里用的是经过MLP后提取点特征代替了直接使用坐标。

> 几何意义：The uprojected image coordinate $d_{k,i} = R_k^{-1} K_k^{-1 }x_i^{(I)} $ for each image coordinate $x_i^{(I)}$ described a direction vector from the origin $t_k$ of camera $k$ to the image plane at depth 1.
>
> 代码实现：1)We encode this direction vector $ d_{k,i} $ using an MLP(shared across k views) into a D-dimensional positional embedding $\delta_{k,i} \in \mathbb{R}^D$... We combine this positional embedding with image features $\phi_{k,i}$ in the keys of our cross-view attention mechanism.
>
> 2)$x^{W}$ 从地图获得，没有高度信息怎么办：We start with a learned positional encoding $c^{(0)}\in \mathbb{R}^{w \times h \times D}$. We build the map-view representation up over multiple iterations in our transformer... Each positional embedding is better able to project the map-view coordinates into a proxy of the 3D environment.

基于上述几何映射的注意力系数计算方式，论文做如下改动作为实际的计算方法：

$$
sim(\delta_{k,i}, \phi_{k,i}, c_j^{n}, \tau_k) = \frac{(\delta_{k,i}+ \phi_{k,i})\cdot(c_j^{(n)} - \tau_k)}{\Vert \delta_{k,i}+ \phi_{k,i} \Vert \Vert c_j^{(n)} - \tau_k \Vert }
$$



​	 $\delta_{k,j}$表示图像的Camera-view positional embedding; $\phi_{k,i} = MLP[d_{k,i}]=MLP[(R_K^{-1}K_K^{-1}x^{(I)})]$表示经过MLP映射后的$D$维向量。相比于原始的计算方式，这里把positional embedding和图像feature加在一起参与运算。$c_j^{(n)}$和$\tau_k$意义和原始公式相同，不同之处是他们也是经过Transforemr和MLP映射到$D$维向量。

## **实验结果：**

![image-20220523135309538](https://s2.loli.net/2022/05/23/sk2fGHMORJ8UjWX.png)



![image-20220523135440759](https://s2.loli.net/2022/05/23/wdDPYJWxlhzFv8s.png)

![image-20220523135515717](https://s2.loli.net/2022/05/23/Y84bdTZ75nNxlJ2.png)

![image-20220523140115644](https://s2.loli.net/2022/05/23/z4uAlfWCjPGHJ7v.png)



## **Related Work(可选):**

- 

## **你认为优点/不足/可以拓展改进的地方(可选):**

优点：

- 利用了地图信息，这是一个比较有新意的setting.
- 提出的transformer不是简单的高维特征计算cos复杂度。从理论上来说，本文是巧妙利用三维点与二维相机视角存在的仿射变换的关系构建的计算方法。原始公式中只需要坐标信息 ，然后在此基础上拓展了图像和地图的positional embedding以及各自的特征信息(如transformer得到的特征向量，图像颜色，点云的极坐标信息等)，可拓展性强。

不足：

- 本文中没有用到LiDAR点云数据。讲道理从LiDAR数据中可以直接获得准确的高度信息，为什么不用呢(是为了提高模型推理速度，避免使用点云数据?)。这样的话从地图中经过多层transformer来估计特征向量的方式总觉得有瑕疵。
- 实验评测在语义分割上做的，但是做的是俯视图语义分割而不是3D语义分割。实际应用中3D语义分割和2D图像语义分割比俯视图语义分割实用很多。俯视图语义分割的重要性有待商榷。此外实验结果虽然和传统方法comparable证明这种利用transformer的新技术路线是有用的，但是30多的mIoU和现在3D语义分割中78的mIoU相比仍然逊色很多。

可以拓展改进的地方：

- 后面利用这套同样的idea，去做一做3D语义分割或2D图像分割。这样能挖掘一个更有意思的课题，我从地图中学习到的信息对CameraView和3D点云分割能起到什么帮助？

