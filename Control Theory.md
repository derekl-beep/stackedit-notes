# Modern Control Theory


## Overview

To be avaliable.

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
The approximation is only true around the vincinity of $\bar{x}$, where the system is instantaneous stable, by adding feedback control, e.g. $u=-Kx$, we aim to stablize the system around $\bar{x}$. Therefore, $A=\frac{Df}{Dx}|_{\bar{x}}$ can be considered as time-invariant, and is a good linear approximation of $f(x)$ within the space we're interested in.

### Example: Pendulum

Equation of Motion (EOM): $$\ddot{\theta}=-\frac{g}{L} \sin \theta -\delta \dot{\theta}$$. Assuming $g/L=1$, we simplify it as $$\ddot{\theta}=-\sin \theta -\delta \dot{\theta}$$.

State-space formulation:

$$\begin{Bmatrix} x_1 \\ x_2 \end{Bmatrix} = \begin{Bmatrix} \theta \\ \dot{\theta} \end{Bmatrix}$$, we have 
$$\begin{Bmatrix} \dot{x}_1 \\ \dot{x}_2 \end{Bmatrix} = \begin{bmatrix} x_2 \\ -\sin x_1 - \delta x_2\end{bmatrix}$$, which is a non-linear function of the state vector. 


## Motivation of Full-State Estimation

$$\dot{x}=Ax+Bu$$, where $x \in \mathbb{R}^n, u \in \mathbb{R}^q$.

With full state measurements, we can design the input as $u=-Kx$ to stabilise the system, and we have $$\dot{x} = Ax - BKx = (A-BK)x$$.

`<Insert the block diagram>`

In reality, we rarely have measurements on all states, i.e. $$y=Cx$$, where $y \in \mathbb{R}^p$ is the measured state vector, and $C \in \mathbb{R}^{p \times n}$ is the measurement matrix, mapping the state vector in $\mathbb{R}^n$ to the measurement vector in $\mathbb{R}^p$.

## Observability

The observability of $(A,C)$ tells us if a full-state estimation if possible with a system matrix $A$ and a measurement matrix $C$, or equavilently, if we can estimate any state $x$ from the time-series measurements $y(t)$.

MATLAB function:
```matlab
>> obsv(A, C)
```

In reality, we design an observer / an estimator, e.g. Kalman Filter, to obtain the full-state estimation, and then design a controller, e.g. LQR, to stabilise the system based on the estimation. 

`<Insert the block diagram>`

### Observablility matrix

$$\mathcal{O} = \begin{bmatrix} 
C \\ CA \\CA^2 \\ \vdots \\ CA^{n-1}
\end{bmatrix}$$

The system is observable if 
1. the rank of $\mathcal{O}$ is $n$ 
2. we can estimate $x$ from $y$.

MATLAB command:
```matlab
>> rank(obsv(A, C))
```

The Observability Gramian gives the information about the degree of observability.


```matlab
>> [U, S, V] = svd(obsv(A, C))
```

The columns of $V$ (the rows of $V^T$) are in order the most observable states in the state-space, i.e. the direction with the highest signal-to-noise ratio.

## Full-State Estimation

$$
\begin{aligned}
	\dot{x} &= Ax +Bu \\
	y &= Cx
\end{aligned}
$$, where $x \in \mathbb{R}^n, u \in \mathbb{R}^q, y \in \mathbb{R}^p$ are the state vector, input vector and measurement vector respectively.


`<Block diagram>`

The dynamics of the estimated state vector is formulated as
$$
\frac{d}{dt}\hat{x} = A\hat{x} +Bu + K_f(y-\hat{y})
$$, where $\hat{y} = C\hat{x}$.

$$
\begin{aligned}
	\frac{d}{dt}\hat{x} &= A\hat{x} +Bu + K_f y -K_f C \hat{x} \\
	&= (A-K_fC) \hat{x} + \begin{bmatrix} B &K_f\end{bmatrix} \begin{bmatrix} u \\ y \end{bmatrix}
\end{aligned}
$$. Hence, $\begin{bmatrix} u \\ y \end{bmatrix}$ is like the input to the full-state estimator, and $(A-K_fC)$ is like the system matrix, defining the dynamics of $\hat{x}$.

We can show if $(A-K_fC)$ is stable, $\hat{x}$ will stably converge to $x$, the true state.

### Estimation errors

The estimation error is defined as 
$$\epsilon = x - \hat{x} \in \mathbb{R}^n$$.

The rate of change of the estimation errors is hence

$$
\begin{aligned}
	\frac{d}{dt} \epsilon &= \frac{d}{dt} x - \frac{d}{dt} \hat{x} \\
	&= (Ax-Bu)-(A\hat{x}+Bu-K_fy-K_fC\hat{x}) \\
	&= A(x-\hat{x}) - K_f C (x-\hat{x}) \\
	&= (A-K_f C) \epsilon
\end{aligned}
$$

If $(A,C)$ is observable, then we can place the eigenvalues of $(A-K_f C)$ anywhere by choosing $K_f$.

This implies if the system is observable, the error $\epsilon$ can be made to converge to zero, or equivalently the full-state estimation $\hat{x}$ converges to the true state $x$. 

## The Kalman Filter

The Kalman filer is an analog of the linear quadrutic regulator (LQR) for optimal full-state estimation, given information on the process noise (modelling error) and measurement noise. 

### Mathematical formulation

$$
\begin{aligned}
	\dot{x}&=Ax+Bu+w_d \\
	y&=Cx+w_n
\end{aligned}
$$, where $w_d \in \mathbb{R}^n \sim N(0,V_d)$ is the process noise, and $w_n \in \mathbb{R}^p \sim N(0,V_n)$is the measurement noise. Both are assumed to be Gaussian processes.

The cost function for minimisation is $$J=\mathbb{E}{[(x-\hat{x})^T(x-\hat{x})]}$$.

### MATLAB command
```matlab
>> Kf = lqe(A, C, Vd, Vn)
```

## Linear Quadratic Gaussian (LQG)

`<Block diagram of LQG>`

Linear: linear system
Quadratic: a quadratic cost function
Gaussian: Gaussian white noises

$$
\frac{d}{dt} \begin{bmatrix} 
x \\ \epsilon
\end{bmatrix}
= \begin{bmatrix} 
(A-BK_r) & BK_r \\ 0 & (A-K_f C) 
\end{bmatrix}
\begin{bmatrix} 
x \\ \epsilon
\end{bmatrix} + \begin{bmatrix} 
I & 0 \\ I & -K_f
\end{bmatrix} 
\begin{bmatrix} 
w_d \\ w_n
\end{bmatrix}
$$

#### Proof

$$
\begin{aligned}
	\dot{x} &= Ax+Bu+w_d \\
	&= Ax - BK_r\hat{x} + w_d \\
	&= Ax - BK_rx + BK_r\epsilon + w_d
\end{aligned}
$$, given $u=-K_r\hat{x}$ and $\hat{x}=x-\epsilon$. Also,

$$
\dot{\epsilon} = (A-K_fC)\epsilon + w_d -K_f w_n
$$. Writing these two equations in block matrices gives the dynamics of state vector $\begin{bmatrix} 
x \\ \epsilon
\end{bmatrix}$.

## Introduction to Robust Control


There was a paper by John C. Doyle in 1978 that changes the modern control field: 
Guaranteed Margins for LQG Regulators (Doyle, 1978). ***Abstract -- There are none***. [Link](https://authors.library.caltech.edu/93672/1/01101812.pdf).

### Robustness and Performance

Robustness: a measure of how sensitive the system is to model uncertainties, time delays, disturbances, etc.

Performance: a measure of how fast the system responses.


## Three Equivalent Representations of Linear Systems

1. State-space representation:
$$\begin{aligned} 
	\dot{x} &= Ax+Bu \\
	y&=Cx
\end{aligned}$$

2. Frequency domain (transfer function):
$$G(s)=C(sI-A)^{-1}B$$

3. Time domain (impulse response):
$$y(t)=\int_{0}^{t}{h(t-\tau)u(\tau)d\tau}$$

### Transfer functions
When a linear system is excited with a sine wave, e.g. $u(t)=\sin(\omega t)$, the responses are also sinusoidal with the same frequency, e.g. $y(t)=A\sin(\omega t +\phi)$, and possibly a different amplitude and a shift in phrase. 

Magnitude of transfer function:
$$|G(i \omega)| = A$$

Angle of transfer function:
$$\angle G(i \omega) = \phi$$

## Example Frequency Response (Bode Plot) for Spring-Mass-Damper

### Equation of Motion
$$
m\ddot{x}+d\dot{x}+kx=u
$$

### Laplace Transform
 $$
 \begin{aligned}
 \mathcal{L}\bigg\{\frac{d}{dt}x\bigg\}&=s\bar{x}(x)-x(0) \\
& =s\bar{x}(s), \text{for x(0)=0}
  \end{aligned}
 $$

Also, 

$$
 \begin{aligned}
 \mathcal{L}\bigg\{\frac{d^2}{dt^2}x\bigg\}&=s^2\bar{x}(x)
  \end{aligned}
$$

To simply the model, assume $m=d=k=1$, and we have


$$\begin{aligned}
\ddot{x} + \dot{x} + x &=u \\
s^2\bar{x} + s\bar{x}
\end{aligned}$$


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
eyJoaXN0b3J5IjpbLTQzMDA5MjY4NCwtMTQxMzk1NTUwMywtMj
Q4NDIyMTc0LC0xOTAwNDkyMDk3LC0yMDI0NjQ4NDYxLC05MjMw
NTkxNjMsLTE0NjIxMTc5ODEsMTc5OTg0NzY5OCwtMzkwNjU2MT
A3LC0yMTA5MjUxMzQ1LC04MjA3MjcxMCwtMTQ3MzI0MzIwMywy
MDcyODI1MzM1LDc1Njc3MjI4NywtMTczMjkzOTQwNiwtMTcwOD
c4MjgwOCwtMTM1NDgwNTQ5LC02MjcyNTE4OTcsLTQ4MTIyNDk0
NSwtNjQ0MTQ0NTEzXX0=
-->