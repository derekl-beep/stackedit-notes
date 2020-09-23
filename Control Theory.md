# Control Theory


## Overview

// TBA

## Linear Systems

Linear systems of ordinary differential equations (ODEs) 

$$
\dot{x}=Ax
$$

, where $x \in \mathbb{R}^n$ is the state vector,
 and  $A \in \mathbb{R}^{n \times n}$ is the system matrix.


The basic solution is

$$
x(t) = e^{At}x(0)
$$

, where $e^{At}=I+tA+\frac{t^2}{2!}A^2+\frac{t^3}{3!}A^3+...$. 
However, computing this infinite sum of matrices are numerically difficult. 

### Eigenvalues and Eigenvectors of the System Matrix

$$A \xi = \lambda \xi$$

Any vector $\xi_i \in \mathbb{R}^n \neq 0$ and constant $\lambda_i \in \mathbb{R}$ satisfying this equation are the **eigenvector** and the **eigenvalue** of matrix $A$ respectively.

Tackling dynamical systems in the eigenvector coordinates are advantageous. It gives us diagonal system dynamics, which is easier to solve.

Define 

$$T=[\xi_1 \ \xi_2 ... \xi_n] \in \mathbb{R}^{n \times n}$$ and $$D=\text{diag}([\lambda_1, \lambda_2,...,\lambda_n])
=\begin{bmatrix}  
\lambda_1 & 0 & \dots & 0 \\  
0 & \lambda_2 & \dots & 0 \\
\vdots & \vdots &\ddots & \vdots \\
0 & 0 & \dots & \lambda_n
\end{bmatrix}
$$


We have $$AT=TD$$.

MATLAB function:
```matlab
>> [T, D] = eig(A);
```

### Transformed coordinates

By defining the $z$ coordinates, which is the direction of the eigenvectors, we can simplify the calculations by decoupling the dynamics. 
 
Define $x=Tz$

$$
\dot{x}=Ax \\
T\dot{z} = ATz \\
\dot{z}=T^{-1}ATz \\
\dot{z} = Dz
$$


$$
\begin{Bmatrix}  
\dot{z_1} \\ \dot{z_2} \\ \vdots \\ \dot{z_n}
\end{Bmatrix}
= \begin{bmatrix}  
\lambda_1 & 0 & \dots & 0 \\  
0 & \lambda_2 & \dots & 0 \\
\vdots & \vdots &\ddots & \vdots \\
0 & 0 & \dots & \lambda_n
\end{bmatrix}
\begin{Bmatrix}
z_1 \\ z_2 \\ \vdots \\ z_n
\end{Bmatrix}
$$

The dynamics are, hence, decoupled in the transformed coordinates, e.g. $$\dot{z}_i =  \lambda_i z_i$$ for $i=1,2,...,n$. 

Solving the differential equations for indivdiual coordinate gives $$z_i(t)=e^{\lambda_i t}z_i(0)$$ for $i=1,2,...,n$.

In matrix format, we have 
$$
z(t) = e^{Dt}z(0)
=\begin{bmatrix}  
e^{\lambda_1 t} & 0 & \dots & 0 \\  
0 & e^{\lambda_2 t} & \dots & 0 \\
\vdots & \vdots &\ddots & \vdots \\
0 & 0 & \dots & e^{\lambda_n t}
\end{bmatrix}
\begin{Bmatrix}
z_1(0) \\ z_2(0) \\ \vdots \\ z_n(0)
\end{Bmatrix}
$$.

### Computing 

We have $$A=TDT^{-1}$$.

$$e^{At}=e^{TDT^{-1}t} \\ \\
=I+t TDT^{-1}+\frac{t^2}{2!}(TDT^{-1})^2+\frac{t^3}{3!}(TDT^{-1})^3+... \\ \\
=TT^{-1}+t TDT^{-1}+\frac{t^2}{2!}TD^2T^{-1}+\frac{t^3}{3!}TD^3T^{-1}+... \\\\
=T(I+tD+\frac{t^2}{2!}D^2+\frac{t^3}{3!}D^3+...)T^{-1} \\ \\
=T e^{Dt} T^{-1}
$$


## References

- Control Bootcamp (YouTube Playlist)
Prof. Steven L. Brunton. University of Washington.
<p align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/videoseries?list=PLMrJAkhIeNNR20Mz-VpzgfQs5zrYi085m" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe><p>

- Data-driven Science and Engineering - Machine Learning, Dynamical Systems and Control
http://databookuw.com

---
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI2OTYyMzE0NSwxMDQ3MzY3MzM5XX0=
-->