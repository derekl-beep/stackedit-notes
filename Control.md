
## Overview

## Linear System Theory

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

, where $e^{At}=I+tA+\frac{t^2}{2!}A^2+\frac{t^3}{3!}A^3+...$. However, this infinite sum of matrices are numerically difficult.

### Eigenvalues and Eigenvector of the System Matrix

$$A \xi = \lambda \xi$$

Any vector $\xi_i$ and constant $\lambda_i$ satisfying this equation are the eigenvector and the eigenvalue of matrix $A$.

Tackling dynamical systems in the eigen-coordinates are advantageous.

Define 

$$T=[\xi_1 \ \xi_2 ... \xi_n]$$ and $$D=[]$$


, we have $AT=TD$.

Define $x=Tz$

$$
\dot{x}=Ax \\
T\dot{z} = ATz \\
\dot{z}=T^{-1}ATz \\
\dot{z} = Dz
$$




---
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MTUzNjA4NjYsOTk2NTA0MzAyLC0xNz
Q4Njk3NjI1XX0=
-->