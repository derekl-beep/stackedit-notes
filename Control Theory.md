# Control Theory


## Overview

```
// TBA
```
## Linear Systems

Linear systems of ordinary differential equations (ODEs) 

$$
\dot{x}=Ax
$$

, where $x \in \mathbb{R}^n$ is the **state vector**,
 and  $A \in \mathbb{R}^{n \times n}$ is the **system matrix**.


The basic solution is

$$
x(t) = e^{At}x(0)
$$

, where $e^{At}=I+tA+\frac{t^2}{2!}A^2+\frac{t^3}{3!}A^3+...$. 
However, computing this infinite sum of matrices are numerically difficult. 

### Eigenvalues and Eigenvectors of the System Matrix

$$A \xi = \lambda \xi$$

Any vector $\xi_i \in \mathbb{R}^n \neq 0$ and constant $\lambda_i \in \mathbb{C}$ satisfying this equation are the **eigenvector** and the **eigenvalue** of matrix $A$ respectively.

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
 
Define $x=Tz$, we have

$$
\begin{aligned}
\dot{x} &= Ax  \\
T\dot{z} &= ATz \\
\dot{z} &= T^{-1}ATz \\
\dot{z} &= Dz 
\end{aligned}
$$ , and

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
$$.


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

### Closed-form expression of  $e^{At}$

Given $A=TDT^{-1}$, the computation of $e^{At}$ can be simplified by the use of the eigenvector and eigenvalue matrices as $$e^{At}=T e^{Dt} T^{-1}$$, and hence, $$x(t)=T e^{Dt} T^{-1}x(0)$$.

#### Proof
$$
\begin{aligned}
  e^{At} &= e^{TDT^{-1}t} \\
&= I+t TDT^{-1}+\frac{t^2}{2!}(TDT^{-1})^2+\frac{t^3}{3!}(TDT^{-1})^3+... \\
&= TT^{-1}+t TDT^{-1}+\frac{t^2}{2!}TD^2T^{-1}+\frac{t^3}{3!}TD^3T^{-1}+... \\
&= T(I+tD+\frac{t^2}{2!}D^2+\frac{t^3}{3!}D^3+...)T^{-1} \\
&= T e^{Dt} T^{-1} 
\end{aligned}
$$

## Stability and Eigenvalues



Stability tells us what the states of the systems will be as time goes to infinity.

### Continuous systems

The basic solution given the initial condition is $$x(t)=Te^{Dt}T^{-1}x(0)$$.

The stability of the system only depends on the time-varying quantities, i.e. $e^{Dt}$. 

$$e^{Dt}=\begin{bmatrix}  
e^{\lambda_1 t} & 0 & \dots & 0 \\  
0 & e^{\lambda_2 t} & \dots & 0 \\
\vdots & \vdots &\ddots & \vdots \\
0 & 0 & \dots & e^{\lambda_n t}
\end{bmatrix}$$


Given $\lambda = a + ib \in \mathbb{C}$, $$e^{\lambda t}=e^{at}[\cos{(bt)}+i\sin{(bt)}]$$. The amplitude of the sinusoidal terms is always within unity. The exponential term (the real part of the eigenvalue), hence, determines the stability behaviour of the system.

<p align="center">
	<img src="https://i.imgur.com/rpPx8Ug.jpg" 
	height="50%" width="50%"/>
</p>

> Source: https://youtu.be/h7nJ6ZL4Lf0?list=PLMrJAkhIeNNR20Mz-VpzgfQs5zrYi085m

The system is stable if and only if all the real part of the eigenvalues of the system matrix are non-positive. $$\text{Re}(\lambda_i) \leq0, \forall i = 1,2,...,n$$

To control an unstable system with feedbacks, e.g. $u=-Kx$, the system behaviours, as well as the eigenvalues, can be changed.

$$\dot{x}=Ax+Bu=Ax-BKx=(A-BK)x$$

<p align="center">
	<img src="https://i.imgur.com/bSMPYCA.jpg" 
	height="50%" width="50%"/>
</p>

> Source: https://youtu.be/h7nJ6ZL4Lf0?list=PLMrJAkhIeNNR20Mz-VpzgfQs5zrYi085m


### Discrete-time systems

$$x_{k+1}=\tilde{A}x_k$$, where $x_k=x(k\Delta t)$, and $\tilde{A}=e^{A \Delta t}$.

Given an initial condition $x_0=x(0)$, we can compute the whole set of dynamics at discrete time as $$\begin{aligned} x_1&=\tilde{A}x_0 \\ x_2&=\tilde{A}^2x_0 \\ x_3&=\tilde{A}^3x_0 \\ &\vdots \\ x_N&=\tilde{A}^Nx_0 \end{aligned}$$

Same as the continuous-time system matrix $A$, the discrete-time system matrix $\tilde{A}$ can be decomposed into the eigenvector and eigenvalue matrices as $$\tilde{A}=\tilde{T}\tilde{D}\tilde{T}^{-1}$$, and hence, $$x_N=\tilde{T}\tilde{D}^N\tilde{T}^{-1}x_0$$.

Simlilarly the eigenvalues determine the stability of the discrete-time system. The system is stable if and only if all the radius of the complex eigenvalues are less than or equal to $1$, i.e. $$|\tilde{\lambda}_i| \leq1, \forall i=1,2,...,n$$. The tilde (~) sign is an indication for the discrete-time space.

<p align="center">
	<img src="https://i.imgur.com/cLLAT5O.jpg" 
	height="50%" width="50%"/>
</p>

> Source: https://youtu.be/h7nJ6ZL4Lf0?list=PLMrJAkhIeNNR20Mz-VpzgfQs5zrYi085m



This can be seen by expressing the complex eigenvalues as a product of radius $R$ and angle $\theta$ as

$$\begin{aligned} 
\tilde{\lambda}&=Re^{i\theta} \\
\tilde{\lambda}^N&=R^Ne^{iN\theta}
\end{aligned}$$

The exponential part always has an amplitude within a unity.

## Linearizing Around a Fixed Point

The non-linear dynamics of a system of ODEs can be described as $$\dot{x}=f(x)$$, where $x \in \mathbb{R}^n$ is the state vector.

### Linearization steps

Step 1: find the fixed points $\bar{x}$ s.t. $f(\bar{x})=0$
Step 2: Linearize $f$ about $\bar{x}$ using the Jocabian matrix $\frac{Df}{Dx}|_{\bar{x}}=[\frac{\partial f_i}{\partial x_j}]$

### Example

Given
$$
	\begin{aligned} 
	\dot{x_1} &= f_1(x_1, x_2) = x_1x_2 \\
	\dot{x_2} &= f_2(x_1, x_2) = x_1^2+x_2^2
	 \end{aligned}
 $$, we have 
 $$
	 \frac{Df}{Dx}
	 =\begin{bmatrix}
		\frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} \\
		\frac{\partial f_2}{\partial x_1} & \frac{\partial f_2}{\partial x_2}
	 \end{bmatrix}
	 = \begin{bmatrix}
	 x_2 & x_1 \\ 
	 2x_1 & 2x_2
	 \end{bmatrix}
$$, and hence 
$$
\begin{Bmatrix}
\dot{x_1} \\ \dot{x_2}
\end{Bmatrix}
	 \approx \begin{bmatrix}
	 \bar{x}_2 & \bar{x}_1 \\ 
	 2\bar{x}_1 & 2\bar{x}_2
	 \end{bmatrix} 
	 \begin{Bmatrix}
x_1 \\ x_2
\end{Bmatrix}
$$.

#### Proof

By the Taylor expression,

$$ \begin{aligned}
\dot{x}=f(x)&=f(\bar{x})+\frac{Df}{Dx}|_{\bar{x}} \cdot (x-\bar{x}) + \frac{D^2f}{Dx^2}|_{\bar{x}} \cdot (x-\bar{x})^2 + \dots  \\
&\approx f(\bar{x})+\frac{Df}{Dx}|_{\bar{x}} \cdot (x-\bar{x})
\end{aligned}
$$

By definition, we choose $\bar{x}$ s.t. $f(\bar{x})=0$, so
$$\Delta \dot{x} = \frac{Df}{Dx}|_{\bar{x}} \Delta x = A \Delta x$$


#### Remark
Although the approximation is only true around the vincinity of $\bar{x}$, where the system is instantaneous stable, by adding feedback control, e.g. $u=-Kx$, we aim to stablize the system around $\bar{x}$. Therefore, $A=\frac{Df}{Dx}|_{\bar{x}}$ can be considered as time-invariant, and is a good linear approximation of $f(x)$ within the pa

## References

- Control Bootcamp (YouTube Playlist)
Prof. Steven L. Brunton. University of Washington.
<p align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/videoseries?list=PLMrJAkhIeNNR20Mz-VpzgfQs5zrYi085m" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe><p>

- Data-driven Science and Engineering - Machine Learning, Dynamical Systems and Control
http://databookuw.com

---
More notes can be found on https://github.com/derekl-beep/cs-notes.

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzcyNjYzMjU1LC0xMzU0ODA1NDksLTYyNz
I1MTg5NywtNDgxMjI0OTQ1LC02NDQxNDQ1MTMsMTg0NjE5NjY2
MywtMTIwMzQ2NjU1MSwtODU4NDUxNCwyMDMwMTc0MDAxLDE3Nz
A5MzI2MjAsMTA0NzM2NzMzOV19
-->