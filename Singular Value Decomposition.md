# Singular Value Decomposition (SVD)


SVD is:

- Data reduction
- Data-driven generalisation of Fourier transform (FFT)
- "Tailored" to specific problems
- Simple and interpretable linear algebra

SVD can solve:

- $Ax=b$, for non-squared $A$ regression
- basis PCA 
- correlations

Real-world applications include:

- Google's PageRank
- Facebook's facial recognition
- Netflix's recommendation system

## Mathematical Overview

$$
X=U \Sigma V^T
$$


$U$ and $V$ are unitary matries, meaning

$$
UU^T = U^TU=I_{n \times n}
$$

and

$$
VV^T = V^T V=I_{m \times m} .
$$

$\Sigma$ is a diagonal matrix with

$$
\sigma_1 \geq \sigma_2 \geq \sigma_3 \geq ... \geq \sigma_m \geq 0
$$

$U$ and $V$ contains the information about the column space and the row space of $X$ respectively. 

$\Sigma$ tells us how important various columns in $U$ and rows in $V$ are.

The SVD of a real matrix is guaranteed to exist, and to be unique.

To compute the SVD in MATLAB, we can do

```matlab
>> [U, S, V] = svd(X);
```

## Matrix Approximation

The economy SVD:

$$
X = U \Sigma V^T \\ {} \\
	= \sigma_1 u_1 v_1^T + \sigma_2 u_2 v_2^T + ... +\sigma_m u_m v_m^T +0 \\ {} \\
	=\hat{U} \hat{\Sigma} V^T
$$

, where $\hat{U}, \hat{\Sigma}, V \in \mathbb{R}^{m \times m}$

and

$\sigma_i u_i v_i^T$ are  rank-one matrices.

In MATLAB:
```matlab
>> [U, S, V] = svd(x, 'econ');
```

By using the first $r$ rank-one matrices to approximate $X$, we have
$$
X \approx \tilde{U} \tilde{\Sigma} \tilde{V}^T
$$

, where $\tilde{U}$,  $\tilde{\Sigma}$,  $\tilde{V}$ $\in \mathbb{R}^{r \times r}$, and $r < m$.

Note that, after truncation, $\tilde{U}$ and $\tilde{V}$ are no long unitary. We have

$$\tilde{U}^T\tilde{U} = I_{r \times r}, \tilde{V}^T\tilde{V} = I_{r \times r}$$

and 

$$\tilde{U}\tilde{U}^T \neq I_{}, \tilde{V} \tilde{V}^T \neq I_{}.$$


### Eckart-Young Theorem [1936]

The theorem states that the best possible matrix approximation of $X$ with rank $r$ is given by first $r$ truncated singular value decomposition of $X$.

$$
\arg \min_{\tilde{X} \text{ s.t. } \text{rank}(\tilde{X}) = r } =\| X -\tilde{X} \| _F = \tilde{U} \tilde{\Sigma} \tilde{V}^T
$$

##  Dominant Correlations

The $U$ and $V$ are the eigenvector matrices of the correlation matrices $XX^T$ and $X^TX$  respectively.

Given $X \in \mathbb{R}^{n \times m}$,

$$
X^{T}X = \begin{bmatrix}  
x_1^T x_1 & x_1^T x_2 & \dots & x_1^T x_m \\  
x_2^T x_1 & x_2^T x_2 & \dots & x_2^T x_m \\
\vdots & \vdots &\ddots & \vdots \\
x_m^T x_1 & x_m^T x_2 & \dots & x_m^T x_m
\end{bmatrix}_{m \times m}
$$

is the correlation matrix among the columns of $X$. Each non-diagonal entry of the matrix is an inner product between two columns, i.e. $x_i^T x_j = \langle x_i, x_j \rangle$. Each diagonal entry is an inner product of the column itself. Hence, the matrix contains information of the linear correlation between columns.

For example, if each column represents the flatten pixels of an individual face image, a large inner product tells us that the two faces are similar, having the same basic face structure, and vice versa.

Note that the correlation matrix $X^T X$ is symmetric and positive semi-definite. The eigenvalues of the matrix are guaranteed to be non-negative, i.e. $\lambda_i \geq 0$.



# References

- Intro to Data Science (YouTube Playlist)
Prof. Steven L. Brunton
University of Washington
<p align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/videoseries?list=PLMrJAkhIeNNQV7wi9r7Kut8liLFMWQOXn" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe><p>

- Data-driven Science and Engineering - Machine Learning, Dynamical Systems and Control
Authur(s): Steven L. Brunton, J. Nathan Kutz
http://databookuw.com

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMjI0MDI1NDAsNDkzMzYzNDcyLC0xOT
U5NzEyMjcwXX0=
-->