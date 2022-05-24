---
title: LaTeX讲解系列：常用数学符号大全
date: 2022-05-24 13:33:34
index_img: https://s2.loli.net/2022/05/24/v7oqPuU2LfKQWFG.jpg
banner_img: https://s2.loli.net/2022/05/24/bYjlZzLXrH1PNAx.jpg
categories:
- [LaTex学习]
tags: [LaTex]
author: Oier99
comment: true
math: true
mermaid: true
excerpt: 最详尽的常用LaTex数学符号整理在这里！
---



# LaTex 讲解系列：常用数学符号大全

{%note primary%}

本文整理过程中着重参考了：

https://www.cnblogs.com/yalphait/articles/8685586.html（LaTex 命令符号大全）

https://blog.csdn.net/u012684062/article/details/78398191 （LaTex 所有常用数学符号整理）

这两份非常全面，非常感谢！尤其第一份大佬的，还介绍了不同符号在数学，物理计算机等不同学科中用法(比如方程组中用希腊小写字母，向量用粗体小写，矩阵用粗体大写等)，还有很多美观排版的建议与事例，强烈安利阅读一番！

除此之外整合了其他网站提到的常用的公式命令，一并列在最后[参考资料](#参考资料)中。

{% endnote %}

## 不同的数学模式

### 重音符号

| $\hat{a}$  `\hat{a}`     | $\check{a}$  `\check{a}` | $\tilde{a}$  `\tilde{a}`         |
| ---------------------------- | ---------------------------- | ------------------------------------ |
| $\grave{a}$  `\grave{a}` | $\dot{a}$  `\dot{a}`     | $\ddot{a}$  `\ddot{a}`           |
| $\bar{a}$  `\bar{a}`     | $\vec{a}$  `\vac{a}`     | $\widehat{A}$  `\widehat{A}`     |
| $\acute{a}$  `\acute{a}` | $\breve{a}$ ` \breve{a}` | $\widetilde{A}$  `\widetilde{A}` |

## 其他

| $\mathbf{E}$  `\mathbf{E}`         | $\mathbb{R}$ ` \mathbb{R}`        | $\mathit{ABC}$  `\mathit{ABC}` |
| ---------------------------------- | ------------------------------------- | ---------------------------------- |
| $\mathrm{ABC}$  `\mathrm{ABC}` | $\mathfrak{ABC}$ `\mathfrak{ABC}` |                                    |



## 希腊字母

| $\alpha$  `\alpha`           | $\theta$  `\theta`       | $o$  ` o`                | $\upsilon$  `\upsilon` |
| ---------------------------- | ------------------------ | ------------------------ | ---------------------- |
| $\beta$  `\beta`             | $\vartheta$  `\vartheta` | $\pi$ ` \pi`             | $\phi$  `\phi`         |
| $\gamma$  `\gamma`           | $\iota$  `\iota`         | $\varpi$  `\varpi`       | $\varphi$  `\varphi`   |
| $\delta$  `\delta`           | $\kappa$ ` \kappa`       | $\rho$ ` \rho`           | $\chi$  `\chi`         |
| $\epsilon$  `\epsilon`       | $\lambda$ ` \lambda`     | $\varrho$  `\varrho`     | $\psi$  `\psi`         |
| $\varepsilon$  `\varepsilon` | $\mu$  `\mu`             | $\sigma$  `\sigma`       | $\omega$  `\omega`     |
| $\zeta$  `\zeta`             | $\nu$  `\nu`             | $\varsigma$  `\varsigma` |                        |
| $\eta$  `\eta`               | $\xi$  `\xi`             | $\tau$  `\tau`           |                        |
| $\Gamma$  `\Gamma`           | $\Lambda$ ` \Lambda`     | $\Sigma$  `\Sigma`       | $\Psi$  `\Psi`         |
| $\Theta$  `\Theta`           | $\Pi$ ` \Pi`             | $\Phi$  `\Phi`           |                        |



## 运算符



### 关系符号

可以在下列符号的相应命令前加上`\not` 命令，得到其否定形式，例如$\in$ 与$\not \in$ 。

| $\leq$  `\le`            | $\ge$  `\ge`             | $\equiv$  `\equiv`   | $\ll$  `\ll`         |
| ------------------------ | ------------------------ | -------------------- | -------------------- |
| $\gg$  `\gg`             | $\doteq$  `\doteq`       | $\prec$  `\prec`     | $\succ$  `\succ`     |
| $\simeq$  `\simeq`       | $\subset$  `\subset`     | $\supset$  `\supset` | $\approx$  `\approx` |
| $\subseteq$ ` \subseteq` | $\supseteq$  `\supseteq` | $\cong$  `\cong`     | $\in$  `\in`         |
| $\vdash$  `\vdash`       | $\dashv$  `\dashv`       |                      |                      |



### 运算符

| $\pm$  `\pm`                  | $\mp$  `\mp`                         | $\cdot$  `\cdot`   | $\div$  `\div`       |
| ----------------------------------- | ---------------------------------------- | ---------------------- | ------------------------ |
| $\times$  `\times`              | $\setminus$  `\setminus`             | $\star$  `\star`  | $\cup$  `\cup`       |
| $\cap$  `\cap`                  | $\ast$  `\ast`                       | $\circ$  `\circ`   | $\lor$ ` \lor`       |
| $\land$  `\land`                | $\oplus$  `\oplus`                   | $\ominus$  `\ominus` | $\diamond$  `\diamond` |
| $\otimes$  `\otimes`            | $\odot$  `\odot`                     | $\oslash$  `\oslash` | $\amalg$ ` \amalg`   |
| $\bigtriangleup$  `\bigtrianglep` | $\bigtriangledown$  `\bigtriangledown` | $\dagger$  `\dagger` | $\ddagger$  `\ddagger` |
| $\wr$  `\wr`                    | $\lnot$ `\not` |                          ||



### ”大“运算符

| $\sum_i^j$  `\sum_i^{j}` | $\prod$ ` \prod`           | $\bigcup$  `\bigcup`   | $\bigcap$  `\bigcap` |
| ------------------------ | -------------------------- | ---------------------- | -------------------- |
| $\bigvee$  `\bigvee`     | $\bigwedge$ `\bigwedge`    | $\int_a^b$  `\int_a^b` | $\oint$  `\oint`     |
| $\bigoplus$  `\bigoplus` | $\bigotimes$  `\bigotimes` | $\bigodot$  `\bigodot` |                      |



### 箭头

| $\leftarrow$  `\leftarrow`           | $\longleftarrow$  `\longleftarrow`            | $\rightarrow$  `\rightarrow` | $\longrightarrow$  `\longrightarrow`       |
| ------------------------------------ | --------------------------------------------- | ---------------------------- | ------------------------------------------ |
| $\leftrightarrow$  `\leftrightarrow` | $\longleftrightarrow$  `\longleftrightarrrow` | $\Leftarrow$ ` \Leftarrow`   | $\Rightarrow$  `\Rightarrow`               |
| $\Leftrightarrow$  `\Leftrightarrow` | $\iff$  `\iff(bigger spaces)`                 | $\mapsto$ `\mapsto`          | $\rightleftharpoons$  `\rightleftharpoons` |
| $\leadsto$  `\leadsto`               |                                               |                              |                                            |



### 常用函数符号

| $\sin \theta$  `\sin \theta`                                 | $\cos\theta$  `\cos\theta` | $\tan\theta$  `\tan\theta` | $\arcsin$ `\arcsin` |
| ------------------------------------------------------------ | -------------------------- | -------------------------- | ------------------- |
| $\arccos$ `\arccos`                                          | $\cosh$  `\cosh`           | $\tanh$  `\tanh`           | $\limsup$ `\limsup` |
| $f'(x) = \lim_{\Delta x \rightarrow 0} \frac{f(x + \Delta x) - f(x)}{\Delta x}$  `\lim_{\Delta x \rightarrow 0} \frac{f(x + \Delta x) - f(x)}{\Delta x}` | $\max$  `\max`             | $\min$ ` \min`             | $\inf$  `\inf`      |
| $\log$  `\log`                                               | $\ln$  `\ln`               | $\ker$  `\ker`             | $\Pr$  `\Pr`        |
| $\dim$  `\dim`                                               | $\det$  `\det`             | $\exp$  `\exp`             |                     |



### 其他

| $\lvert a \rvert$  `\lvert a \rvert` | $\lVert a \rVert$ ` \lVert a \rVert` | $\dots$  `\dots`                                             | $\cdots$  `\cdots`(for matrix) |
| ------------------------------------ | ------------------------------------ | ------------------------------------------------------------ | ------------------------------ |
| $\vdots$  `\vdots`                   | $\ddots$  `\ddots`                   | $\forall$  `\forall`                                         | $\exists$  `\exists`           |
| $\partial$  `\partial`               | $\nabla$  `\nabla`                   | $\bot$  `\bot`                                               | $\top$  `\top`                 |
| $\angle$  `\angle`                   | $\surd$  `\surd`                     | $\emptyset$  `\emptyset`                                     | $\ell$  `\ell`                 |
| $\infty$ `\infty`                    | $\heartsuit$  `\heartsuit`           | $\clubsuit$  `\clubsuit`                                     | $\spadesuit$  `\spadesuit`     |
| $\therefore$  `\therefore`           | $\because$  `\because`               | $\mathop{\arg\min}_{\theta}$   `\mathop{\arg\min}_{\theta}`(套在LaTeX equation环境下，下标$\theta$能自动在字母下面) |                                |



## 矩阵表示

1. 

$$
\begin{align}
	\left[ \begin{matrix}
  a_{11} & a_{12} & \cdots & a_{1n} \\
  a_{21} & a_{22} & \cdots & a_{25} \\
  \vdots & \vdots & \ddots & \vdots \\
  a_{n1} & a_{n2} & \cdots & a_{nn}
  \end{matrix}\right]
\end{align}
$$

```latex
\begin{align} % 推荐用align或equation的数学环境
	\left[ \begin{matrix} % 推荐使用matrix的环境, 如果使用array环境需要指定{ccc}列数
  a_{11} & a_{12} & \cdots & a_{1n} \\
  a_{21} & a_{22} & \cdots & a_{25} \\
  \vdots & \vdots & \ddots & \vdots \\
  a_{n1} & a_{n2} & \cdots & a_{nn}
  \end{matrix}\right] % \left[ 与\right]配对，[还可以换成{, (等 
\end{align}

% 如使用nicematrix宏包，需要在完整版的LaTex环境中引用该包
% 详见官方连接https://ctan.org/pkg/nicematrix
```



2. 上下大括号

$$
\begin{align}
&\begin{matrix} 5050 \\ \overbrace{ 1+2+\cdots+100 }\end{matrix} \\
\\
&\begin{matrix} \underbrace{ a+b+\cdots+z } \\ 26\end{matrix}
\end{align}
$$



```latex
\begin{align}
&\begin{matrix} 5050 \\ \overbrace{ 1+2+\cdots+100 }\end{matrix} \\
\\
&\begin{matrix} \underbrace{ a+b+\cdots+z } \\ 26\end{matrix}

\end{align}
```



3. 方程组/分段函数


$$
=
\begin{cases}
3x + 5y +  z, & x+y+z <1\\
7x - 2y + 4z, & 1\le x+y+z <5\\
-6x + 3y + 2z, & x+y+z > 1 
\end{cases}
$$

```latex
=
\begin{cases}
3x + 5y +  z, & x+y+z <1\\
7x - 2y + 4z, & 1\le x+y+z <5\\
-6x + 3y + 2z, & x+y+z > 1 
\end{cases}
```

4. 数组

$$
\begin{array}{|c|c||c|} a & b & S \\
\hline
0&0&1\\
0&1&1\\
1&0&1\\
1&1&0\\
\end{array}
$$



```latex
\begin{array}{|c|c||c|} a & b & S \\
\hline
0&0&1\\
0&1&1\\
1&0&1\\
1&1&0\\
\end{array}
```

(未完待续，动态补充)

## 参考资料

1. https://www.cnblogs.com/yalphait/articles/8685586.html
2. https://zhuanlan.zhihu.com/p/266267223
3. https://blog.csdn.net/u012684062/article/details/78398191

