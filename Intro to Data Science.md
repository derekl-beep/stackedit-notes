

# Machine Learning

### Overview

Machine learning is:

- Models from training data
- Optimization & Regression
- A combination of linear algebra, optimisation theory, statistics, and more ...
- Human guided, e.g.
	- Questions to addressed
	- Data to be collected, inputs / outputs of ML models
	- ML architecture

Machine learning is **NOT**:

- Magic
- Just neural networks (NN)

In some sense, machine learning is an optimazation problem, in which we optimize the underlying models with the data we collected.

### Goals

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

$$\tilde{U}\tilde{U}^T \neq I_{r \times r}, \tilde{V} \tilde{V}^T \neq I_{r \times r}.$$


### Eckart-Young Theorem [1936]

The theorem states that the best possible matrix approximation of $X$ with rank $r$ is given by first $r$ truncated singular value decomposition of $X$.

$$
\arg \min_{\tilde{X} \text{ s.t. } \text{rank}(\tilde{X}) = r } =\| X -\tilde{X} \| _F = \tilde{U} \tilde{\Sigma} \tilde{V}^T
$$

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
eyJoaXN0b3J5IjpbLTU4NzEwNjIwLDE4NTc5MTkwMzgsMTc4Nj
U1MzI4NCwtMTYwODU0OTc1MiwxMDE1MTEzMTQ2LC0xMTU0NjM5
MzkxLC05MTIyMjA2OTAsNzMwOTk4MTE2XX0=
-->