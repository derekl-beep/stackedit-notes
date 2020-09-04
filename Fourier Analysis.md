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



## Inner Products in Hilbert Space

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

>Source: https://www.youtube.com/watch?v=g-eNeXlZKAQ&list=PLMrJAkhIeNNT_Xh3Oy0Y4LTj0Oxo8GqsC&index=4


## Complex Fourier Series

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

## Fourier Series in Python


### Algorithm

```c
// TBC
```


### Fourier approximation of a hat function

The figure shows the approximation of a hat function using 1 to 20 modes.

<p align="center"><img src="https://github.com/derekl-beep/screen-captures/blob/master/Screenshot%202020-08-15%20at%201.00.32%20PM.png?raw=true" height="50%" width="50%" /> </p>

The approximation error decreases monotonically as the number of modes / terms increases.

<p align="center"><img src="https://github.com/derekl-beep/screen-captures/blob/master/Screenshot%202020-08-15%20at%201.00.42%20PM.png?raw=true" height="50%" width="50%"/> </p>

>Source: https://github.com/dynamicslab/databook_python/blob/master/CH02/CH02_SEC01_1_FourierSines.ipynb



### Fourier approximation of discontinuity and the Gibbs phenomenon

The **truncated** Fourier series, i.e. keeping only the lower frequency terms, gives a satisfying approximation of continuous functions. However, obvious fluctuations can be seen at discontinuities. This approximation error is named as the Gibbs phenomenon.

<p align="center">
	<img src="https://github.com/derekl-beep/screen-captures/blob/master/Screenshot%202020-08-15%20at%201.05.00%20PM.png?raw=true" 
	height="50%" width="50%"/>
</p>

>Source: https://github.com/dynamicslab/databook_python/blob/master/CH02/CH02_SEC01_2_Gibbs.ipynb


## The Fourier Transform

The Fourier series is defined for periodic functions, e.g. $f(x) \in L_2([-L, L])$. The Fourier transform, instead, generalised the definition for an infinite domain.

Fourier series formula:

$$
f(x)
	= \sum_{k=-\infty}^{\infty} {c_k e^{ik \pi x/L}}
$$

, where 

$$
c_k
	=\frac{1}{2\pi} \langle f(x), \Psi_k \rangle 
	= \frac{1}{2L} \int_{-L}^{L} {f(x) e^{ik \pi x/L}} dx .
$$

If we define $\omega_k=\frac{k\pi}{L}=k\Delta \omega$,

$$
f(x)
	= \sum_{k=-\infty}^{\infty} \Big( { \frac{1}{2L} \int_{-L}^{L} {f(\xi)e^{i\omega_k \xi}} d\xi \Big) e^{i\omega_k x}}.
$$

<p align="center">
	<img src="https://github.com/derekl-beep/screen-captures/blob/master/Screenshot%202020-08-16%20at%209.23.26%20AM.png?raw=true" 
	height="50%" width="50%"/>
</p>

> Source: https://www.youtube.com/watch?v=jVYs-GTqm5U

To extend the Fourier series to the Fourier transform, we take limitation of the period to the infinity, i.e. $[-L, L] \rarr (-\infty, \infty)$ and $\Delta \omega \rarr 0$. The resolution with which we can resolve the frequencies becomes infinitesimally small, and the summation in the Fourier series becomes a Riemann integral.

$$
f(x)
	=\lim_{\Delta \omega \rarr 0} \sum_{k=-\infty}^{\infty} \Big( { \frac{\Delta \omega}{2 \pi} \int_{-\pi / \Delta \omega}^{\pi / \Delta \omega} {f(\xi)e^{i k\Delta \omega \xi}} d\xi \Big) e^{i k\Delta \omega x}}
	\\
	{}
	\\
	=\int_{-\infty}^{\infty} {\frac{1}{2 \pi} \int_{-\infty}^{\infty} {f(\xi)e^{i \omega \xi}} d\xi} e^{i \omega x} d \omega
$$

The Fourier cofficient / the Fourier transform, which is a continuous function of frequency $\omega$, is defined as
$$
\hat{f}(\omega) = \mathcal{F}(f(x)) = \int_{-\infty}^{\infty} {f(x) e^{i \omega x}} dx
$$

The inverse Fourier transform is thus defined as 

$$
f(x)=\mathcal{F}^{-1}(\hat{f}(\omega))
	=\frac{1}{2 \pi} \int_{-\infty}^{\infty} {\hat{f}(\omega) e^{i \omega x} d \omega}
$$

The Fourier transform $\mathcal{F}$ is an unitary operator.


## The Fourier Transform and Convolution Integrals

The convolution integral in the spatial variable can be simplified by Fourier transforming the functions first.

The convolution of two functions, $f(x)$ and $g(x)$, is defined as

$$
(f*g)=\int_{-\infty}^{\infty} f(\xi-x)g(x)d\xi
$$

The Fourier transform of the convolution integral gives a product of the two functions in the frequency domain.

$$
\mathcal{F}(f*g) = \mathcal{F}(f) \mathcal{F}(g) = \hat{f}(\omega) \hat{g}(\omega)
$$

The following shows the inverse Fourier transform of $\hat{f}(\omega) \hat{g}(\omega)$ gives the convolution integral $(f*g)$.

$$
\mathcal{F}^{-1}(\hat{f}(\omega) \hat{g}(\omega))
	=\frac{1}{2\pi}\int_{-\infty}^{\infty} \hat{f}(\omega) \hat{g}(\omega) e^{i \omega x} d \omega.
$$

Expressing $\hat{g}(\omega)$ as a Fourier transform of $g(x)$ gives

$$
\begin{aligned}
  &\begin{aligned}
   \mathcal{F}^{-1}(\hat{f}(\omega) \hat{g}(\omega))
  \end{aligned}\\
  &\begin{aligned}
=\frac{1}{2\pi}\int_{-\infty}^{\infty} \hat{f}(\omega) \Bigg(\int_{-\infty}^{\infty} {g(y)e^{-i \omega y}dy} \Bigg) e^{i \omega x} d \omega
  \end{aligned}\\
  &\begin{aligned}
 = \int_{-\infty}^{\infty} g(y) \Bigg(  \frac{1}{2\pi}\int_{-\infty}^{\infty} \hat{f}(\omega) e^{i \omega (x-y)} d\omega \Bigg) dy
  \end{aligned}\\
  &\begin{aligned}
= \int_{-\infty}^{\infty} f(x-y)  g(y) dy
\end{aligned}\\
	&\begin{aligned}
	= f*g
	\end{aligned}
\end{aligned}
$$

## Parseval's Theorem

$$
\int_{-\infty}^{\infty}
$$

The norm of $f$ represents the energy in $f$. Parseval's theorem states that the energy in the frequency domain is directly proportional to the energy in the space domain. 

This implies that truncating those negligibly small Fourier coefficients does not impact

Besides, the Fourier transform is a linear operator, such that

$$
\mathcal{F}(\alpha f(x)+\beta g(x)) = \alpha \mathcal{F}(f) +\beta\mathcal{F}(g).
$$



# References

- Fourier Analysis (YouTube Playlist)
Prof. Steven L. Brunton
University of Washington
Preview:
<p align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/videoseries?list=PLMrJAkhIeNNT_Xh3Oy0Y4LTj0Oxo8GqsC" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe><p>


- Data-driven Science and Engineering - Machine Learning, Dynamical Systems and Control
http://databookuw.com

- GitHub Repository
https://github.com/dynamicslab/databook_python



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYxNzY0NDQ2OSwxMjY5NzA0NTIxLDEwNT
QzODY4NjQsLTYwNjE1OTk2MSwxNTc0NTk1MjI5LDE1MzQyMTc0
OTYsLTE3ODMxOTMzNzQsMTIwNzEyNzMyMiwzNTkxMDE5MjYsMz
Q4MzAxOTE0LC0xNzExNzMzMzA4LDgxNzA4MDk1OSwtMjA4MTM1
MTc1NSwtMTEzOTQ3NjM0Myw1MTMxNjIzMzMsODQ4NjYxNTIsLT
ExMjQ2NjAxNCwyMDcyMDg2OTgyLDE1NjMwMjUzN119
-->