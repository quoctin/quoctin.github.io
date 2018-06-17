---
layout: post
title:  "Mihcak's denoising filter for 2D images"
date:   2018-06-17 01:00 -0200
description: Mihcak's denoising filter for 2D images
permalink: /mihcak-filter/
category: "blog"
usemathjax: true
---

## Motivation
<p align="justify">
A compressible signal is generally composed by only a few principle components. Keeping only principle components and discarding redundant components is the goal of many compression algorithms. We can think of a compressible signal as the composition of many "similar structures", and there exist cheaper ways to represent them. On the contrary, noise is not compressible as it doesn't contain "random structures".
</p>
<p align="justify">
The target of this post is not about compression, but about a denoising algorithm for 2D images as this algorithm shares the same motivation as compression. Both of them aim to identifying random structures in a signal and attempt to remove them.
</p>

## Wavelet decomposition
<p>
Principle components in a natural image are mostly contained in low frequency band, which are visible to human eyes. Therefore, compression or denoising is usually done on frequency domain. Discrete Fourier Transform is famous for analyzing frequency components of an image. However, it doesn't present the spectrum at different portions or different scales. Wavelet decomposition does.
</p>
<p>
Going deep into wavelet decomposition stays beyond this post. In the view of linear algebra, if a signal $f(t)$ is on the space spanned by a basis $\Phi(k)$, it can be expressed by linear combination of the basis.

$$f(t) = \sum_{k=1}^N a_k \Phi_k(t), \quad k \; \text{is the integer index} \tag{1} \label{1}$$

If the set of $\{\Phi_k\}$ is carefully chosen, there exist another set of $\{\tilde{\Phi}_k\}$ such that they are <b>orthonormal</b>:

$$\langle \Phi_i(t), \tilde{\Phi}_j(t)\rangle = \begin{cases} \int \Phi_i(t) \tilde{\Phi}^*_j(t) dt = \delta_{ij} \quad if i=j \\ 0 if i\neqj \end{cases} \tag{2} \label{2}$$
where $^*$ is the complex conjugate and $\delta_{ij}$  is the unit function.
The property ($\ref{2}$) allows to compute $a_k = \langle f(t), \tilde{\Phi}_k(t) \rangle$ as the transform, and (\ref{1}) as the inverse transform.
</p>

<p>
  In 2D wavelet decomposition, we have two kinds of basis functions $\Phi(x,y)$ and $\Psi(x,y)$ corresponding to <i>scaling</i> and <i>wavelet</i> functions. $\Phi(x,y)$ is subscripted by $(j,m,n)$ where $j$ tells the <i>scale</i> of frequency, and $(m,n)$ is the 2D subscription of a particular function. There are three different sets of wavelet functions $\Psi^{H}(x,y), \Psi^{V}(x,y), \Psi^{D}(x,y)$, each of them is similarly subscripted by $(j,m,n)$.
</p>

<p>
  Suppose the basis functions are ready, the image $I$ is decomposed into <b>four</b> bands for each decomposition level: <b>LL, HL, LH, HH </b>. The band <b>LL</b> contains low frequency components of the image, while <b>HL, LH, HH</b> represent variations along $x$-axis, $y$-axis, and diagonal. One can decide to decompose $I$ with more than one level, where the subsequent level is performed on the current <b>LL</b> band instead of $I$. After one decomposition level, the resolution is halved to haft.
</p>

<p>
  In the next section, we perform decomposition based on <i>Daubechies</i> wavelets which is a particular set of basis functions $\Phi(x,y)$ and $\Psi(x,y)$ commonly used in practice, up to 4 decomposition levels.
</p>
