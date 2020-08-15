# Fourier Series

A function can be expressed as an infinite sum of sine and cosine functions of increasing frequency. A Fourier series projects a function into orthogonal basis of sines and cosines. 

For a function defined from $-\pi$ to $\pi$,

$$
f(x) = \frac{A_0}{2} + \sum_{k=0}^{\infty}{\big(A_k \cos(kx)+B_k \sin(kx)\big)}
$$

, where

$A_k = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \cos{(kx)} dx = \frac{1}{\|\cos{(kx)} \|^2} \big\langle f(x), \cos{(kx)} \big\rangle$

and 

$B_k = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \sin{(kx)} dx = \frac{1}{\|\sin{(kx)} \|^2} \big\langle f(x), \sin{(kx)} \big\rangle$.



## Fourier series on a L-periodic function

For a function define from $0$ to $L$, i.e. $f(x)\in L_2([0,L])$,

$$
f(x) = \frac{A_0}{2} + \sum_{k=0}^{\infty}{\Big(A_k \cos{\big(\frac{2\pi kx}{L}\big)} + B_k \sin\big(\frac{2\pi kx}{L}\big)\Big)}
$$

, where

$A_k = \frac{2}{L} \int_{0}^{L} f(x) \cos{ \big(\frac{2\pi kx}{L}\big) } dx$

and 

$B_k = \frac{2}{L} \int_{0}^{L} f(x) \sin{ \big(\frac{2\pi kx}{L}\big) } dx$.



# Inner Products in Hilbert Space

The inner product of functions are similar to the inner product of vectors. It tells us how similar / aligned two functions are in the function space.

The inner product of two real functions, $f$ and $g$ is defined as

$$
\langle f(x), g(x) \rangle = \int_{a}^{b} f(x)g(x)dx
$$

The inner product of two functions can also be thought as **the inner product of the data points** of the two functions normalised by the constant interval between data.

$$
\langle \vec{f}, \vec{g} \rangle \Delta x =\sum_{k=1}^{n} {f(x_k) g(x_k)} \Delta x
$$

As the resolution of the data points increases, i.e. $\Delta x \rarr 0$ and $n \rarr \infty$, the expression gives exact inner product of the two functions.

<p align="center"><img src="https://raw.githubusercontent.com/derekl-beep/screen-captures/master/Screenshot%202020-08-14%20at%206.42.12%20PM.png" height="50%" width="50%" /> </p>

`Source: https://www.youtube.com/watch?v=g-eNeXlZKAQ&list=PLMrJAkhIeNNT_Xh3Oy0Y4LTj0Oxo8GqsC&index=4`


# Complex Fourier Series

Inner product of complex-valued functions are
$$
\langle f(x), g(x)\rangle = \int_{-\pi}^{\pi} f(x) \bar{g}(x)dx
$$
, where $\bar{g}(x)$ is the complex conjugate of $g(x)$.


Euler formula:

$$
e^{ikx} = \cos{(kx)} + i \sin{(kx)} \coloneqq \Psi_k.
$$

The functions with different frequency are orthogonal to each others. This can be shown by evaluating the inner products.

$$
\langle \Psi_j, \Psi_k \rangle
=\int_{-\pi}^{\pi} {e^{ikx} e^{-ijx}} dx
=\int_{-\pi}^{\pi} {e^{i(k-j)x}} dx
= \frac{1}{i(k-j)} \Big[ {e^{i(k-j)x}}  \Big]_{-\pi}^{\pi}
=\left\{ \begin{array}{l}
	0, \text{if } j \neq k\\
	2 \pi, \text{if } j=k 
	\end{array}
	\right. .
$$

The Fourier series of a function can be expressed as an infinite sum of ...

$$
f(x) 
	= \sum_{-\infty}^{\infty} {C_k e^{ikx}}
	=\sum_{-\infty}^{\infty}(\alpha_k+i\beta_k) \big(\cos{(kx)} + i\sin{(kx)} \big)
	=\frac{1}{2\pi} \sum_{-\infty}^{\infty} \langle f(x), \Psi_k \rangle \Psi_k
$$
, where

$C_k = \bar{C}_{-k}$ if $f(x)$ is real-valued.

# Fourier Series in Python

GitHub Repository: https://github.com/dynamicslab/databook_python


### Algorithm




### Fourier approximation of a hat function




### Fourier approximation of discontinuity and the Gibbs phenomenon





# References

- Fourier Analysis (YouTube Playlist)
Prof. Steve Brunton
University of Washington
Preview:
<p align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/videoseries?list=PLMrJAkhIeNNT_Xh3Oy0Y4LTj0Oxo8GqsC" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe><p>


- Data-driven Science and Engineering - Machine Learning, Dynamical Systems and Control
http://databookuw.com




> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIwNzEyNzMyMiwzNTkxMDE5MjYsMzQ4Mz
AxOTE0LC0xNzExNzMzMzA4LDgxNzA4MDk1OSwtMjA4MTM1MTc1
NSwtMTEzOTQ3NjM0Myw1MTMxNjIzMzMsODQ4NjYxNTIsLTExMj
Q2NjAxNCwyMDcyMDg2OTgyLDE1NjMwMjUzN119
-->