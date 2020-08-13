

# Fourier Series

A function can be expressed as an infinite sum of sin and cos functions of increasing frequency.

$$
f(x) = \frac{A_0}{2} + \sum_{k=0}^{\infty}{\big(A_k \cos(kx)+B_k \sin(kx)\big)}
$$

, where

$A_k = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \cos{(kx)} dx = \frac{1}{\|\cos{(kx)} \|^2} \big\langle f(x), \cos{(kx)} \big\rangle$

and 

$B_k = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \sin{(kx)} dx = \frac{1}{\|\sin{(kx)} \|^2} \big\langle f(x), \sin{(kx)} \big\rangle$




# References


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ4NTk4OTk3M119
-->