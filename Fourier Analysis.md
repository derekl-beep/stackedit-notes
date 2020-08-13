

# Fourier Series

A function can be expressed as an infinite sum of sine and cosine functions of increasing frequency. A Fourier series projects a function into orthogonal basis of sines and cosines. 

$$
f(x) = \frac{A_0}{2} + \sum_{k=0}^{\infty}{\big(A_k \cos(kx)+B_k \sin(kx)\big)}
$$

, where

$A_k = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \cos{(kx)} dx = \frac{1}{\|\cos{(kx)} \|^2} \big\langle f(x), \cos{(kx)} \big\rangle$

and 

$B_k = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \sin{(kx)} dx = \frac{1}{\|\sin{(kx)} \|^2} \big\langle f(x), \sin{(kx)} \big\rangle$




# References

- Fourier Analysis (YouTube Playlist)
Prof. Steve Brunton
University of Washington
Preview:
<p align="center"><iframe width="100%" height="315" src="https://www.youtube.com/embed/videoseries?list=PLMrJAkhIeNNT_Xh3Oy0Y4LTj0Oxo8GqsC" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe><p>


- Data-driven Science and Engineering - Machine Learning, Dynamical Systems and Control
http://databookuw.com


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTczMDQ4NTcwNSwxNTYzMDI1MzddfQ==
-->