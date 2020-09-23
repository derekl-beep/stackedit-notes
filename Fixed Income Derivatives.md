# Fixed Income Derivatives

## Overview

These notes are based on my coursework in [MATH 4511](https://prog-crs.ust.hk/ugcourse/2020-21/MATH) - Quantitative Methods for Fixed Income Derivatives back at [HKUST](https://www.ust.hk/home), Math Department, instructed by [Prof. Wu Lixin](https://www.math.ust.hk/~malwu/).

### Course description
Bond, bond markets and interest-rate derivatives markets. Yields, forward rate and swap rates. Yield-based risk management and regression-based hedging. Mortgage mathematics. Binomial models for equity and fixed-income derivatives. Arbitrage pricing and risk-neutral valuation principle. Eurodollar futures. Lognormal models and Black formula for caps and swaptions.

### Prerequisite(s)
- Multivariable calculus
- Linear algebra
- Probability
- Background in financial markets

### Textbook and Reference Books

Textbook
- Bruce, T. (2012) Fixed Income Securities: Tools for Today's Markets, 3rd edition. Wiley Finance.

Reference books  
- McDonald, Robert, L. (2014). Derivatives Markets, 3rd ed. Pearson.  
- Hull, John (2014). Options, Futures, and Other Derivatives, 9th ed. Prentice Hall.

### Course Outlines

- Introduction to financial markets  
- Linear and nonlinear derivatives
- Arbitrage pricing of linear derivatives
- Binomial model for nonlinear derivatives
- The Black‐Scholes option models
- Bond mathematics   
- Yield‐based risk management  
- Pricing of vanilla securities  
- Term structure models for interest‐rate derivatives
- Binomial interest‐rate model for bond options
- Mortgage mathematics

# 1 - Bond Prices, Discount Factors, and Arbitrage

## Discount Factors

The discount factor for a particular term indicate the **present value** of one unit currency to be received at the end of the term. 

The discount factors for different terms of a currency can usually be extracted from the corresponding Treasury bond prices because these bonds promoise future cash flows at a fixed interval of time. 

Denote the discount factor for $t$ years by $d(t)$.

Suppose the $1\frac{1}{4}\%$ s of November 30, 2010 (6 months from now) is trading at $100.550, so we have $$\begin{aligned} 100.550 &= (100+\frac{1\frac{1}{4}}{2})d(0.5) \\ d(0.5)&=0.99925\end{aligned}$$

### Bootstrapping the Discount Factors

<p align="center">
	<img src="https://i.imgur.com/GzOkgy7.png" 
	height="50%" width="50%"/>
</p>

>Source: Bruce, T. (2012) Fixed Income Securities: Tools for Today's Markets, 3rd edition.

With the prices of a series of U.S. Treasury bonds, we can extracted the discount factors directly. For example, 

$$
\begin{aligned}
	\begin{bmatrix}
		100+\frac{1\frac{1}{4}}{2} & 0 & 0 \\
		\frac{4\frac{7}{8}}{2} & 100+\frac{4\frac{7}{8}}{2} & 0 \\
		\frac{4\frac{1}{2}}{2} & \frac{4\frac{1}{2}}{2} & 100+\frac{4\frac{1}{2}}{2} 
	\end{bmatrix} 
	\begin{Bmatrix}
	d(0.5) \\ d(1.0) \\d(1.5)
	\end{Bmatrix}
	&= \begin{Bmatrix} 
	100.550 \\ 104.513 \\ 105.856
	\end{Bmatrix} \\
	\begin{Bmatrix}
	d(0.5) \\ d(1.0) \\d(1.5)
	\end{Bmatrix}
	&= \begin{Bmatrix}
	0.99925 \\ 0.99648 \\ 0.99135
	\end{Bmatrix}
\end{aligned}
$$

### Example (Arbitrage)

Suppose the $3/4$ s of November 30, 2011 is trading at $100.19. We can show that there is an arbitrage oppurtunty.

The fair price of the bond, calculated with the discount factors is
$$B_{fair}=\frac{3}{8}d(0.5) + \frac{3}{8}d(1.0) + (100+\frac{3}{8})d(0.5) = 100.255$$, which is higher than the market price, implying this bond is undervalued by the market.

We can short a replicating portfolio of the $3/4$ s of November 30, 2011, and long a portfolio of the $3/4$ s of November 30, 2011 to make a profit. 

To construct the replicating portfolio, denote the face values of the $1\frac{1}{4}$s, $4\frac{7}{8}$s and $4\frac{1}{2}$s be $F_1$, $F_2$ and $F_3$ respectively. Then, 
$$
\begin{aligned}
	\begin{pmatrix}
		1+\frac{1.25\%}{2} & \frac{4.875\%}{2} & \frac{4.5\%}{2} \\
		0 & 1+\frac{4.875\%}{2} & \frac{4.5\%}{2} \\
		0 & 0 & 1+\frac{4.5\%}{2}
	\end{pmatrix} 
	\begin{pmatrix}
	F_1 \\ F_2 \\F_3
	\end{pmatrix}
	&= \begin{pmatrix} 
	\frac{0.75\%}{2} \\ \frac{0.75\%}{2} \\1+\frac{0.75\%}{2}
	\end{pmatrix} \\
	\begin{pmatrix}
	F_1 \\ F_2 \\F_3
	\end{pmatrix}
	&= \begin{pmatrix}
	-1.779 \\-1.790 \\98.166
	\end{pmatrix}
\end{aligned}
$$

The cost of the replicating portfolio = $\frac{-1.779}{100}\times 100.550+ \frac{-1.790}{100} \times 104.513 + \frac{98.166}{100} \times 105.856 = 100.255$.

## Quote Convention of Bond Prices

```
// TBA
```
 
## Accrued Interest

```
// TBA
```

## Day‐Count Conventions

```
// TBA
```

# 2 - Yields, Spot Rates and Forward Rates

## Popular Compounding Frequencies

$\omega=1$, annual compounding (Euro bonds)
$\omega=2$, semiannual compounding (USD bonds)
$\omega=4$, quarterly compounding (floating rate notes)
$\omega=12$, monthly compounding (mortgages)
$\omega=365$, daily compounding (saving accounts)
$\omega=\infty$, continuous compounding (theoretical modelling)



## Bond Yields

### Yield-to-maturity

The definition of yield-to-maturity (YTM) of a USD coupon bond (compounded semiannually) for settlement on a coupon payment is 

$$
\begin{aligned}
P &= \frac{\frac{1}{2}c}{(1+\frac{y}{2})} +  \frac{\frac{1}{2}c}{(1+\frac{y}{2})^2} + \dots + \frac{1+\frac{1}{2}c}{(1+\frac{y}{2})^{2T}} \\
&= \frac{c}{2} \sum_{t=1}^{2T}{\frac{1}{(1+\frac{y}{2})^t}} +\frac{1}{(1+\frac{y}{2})^{2T}} \\
&=\frac{c}{y} \Big[ 1-\frac{1}{(1+\frac{y}{2})^{2T}} \Big] +\frac{1}{(1+\frac{y}{2})^{2T}}
\end{aligned}
$$

When the first coupon is due in $\tau$ fraction of a half year, the bond price is further discounted 
$$P=\Big( 1+\frac{y}{2}\Big)^{1-\tau} \Big\{ \frac{c}{y} \Big[ 1-\frac{1}{(1+\frac{y}{2})^{2T}} \Big] +\frac{1}{(1+\frac{y}{2})^{2T}} \Big\}$$

### Example

The price of the $4 \frac{1}{2}$s of November 30, 2011 (Table 1.2), was 105.856. The yield‐to‐maturity, $y$, of this bond is therefore defined such that

$$105.856=\frac{2.25}{1+\frac{1}{y}} + \frac{2.25}{(1+\frac{1}{y})^2} + \frac{100 + 2.25}{(1+\frac{1}{y})^3}$$, which can be solved by numerical methods, e.g. the Newton's method.

### Price‐yield Relationship

// TBA

### Coupon-yield Relationship

$$P(T) =\frac{c}{y} \Big[ 1-\frac{1}{(1+\frac{y}{2})^{2T}} \Big] +\frac{1}{(1+\frac{y}{2})^{2T}}$$

- Par bond: when $c=y,P(T)=1$.  
- Premium bond: when $c > y, P(T) > 1$.  
- Bond sold at discount: when $c < y, P(T) < 1$.

### Pull‐to‐Par

Pull to par is the movement of a **bond's price toward its face value** as it approaches its maturity date. Premium bonds, which trade at a higher price than their face (par) value, will decrease in price as they approach maturity. Discount bonds, which trade at a lower price than their par value, will increase in price as they approach maturity.

> Source: https://www.investopedia.com/terms/p/pull-to-par.asp


### Formula for Annuities

An annuity makes annual payments of $c$ until date $T$ with no final principal payment.

The cashflow of an annuity is similar to that of a coupon bond, except there is no final principal payment at the maturity.

The annuity formula: 
$$A(T)=\frac{c}{y}\Big[1-\frac{1}{(1+y)^{T}} \Big]$$

The perpetuity (as $T \rightarrow \infty$) formula:
$$P=\frac{c}{y}$$



---
More notes can be found on https://github.com/derekl-beep/cs-notes.

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg1MjI4ODIyOCwxNTAzMDUzMDIzLDU5NT
c2NzM2NSw4MTUxODE1OTIsNTc2Nzc3MTA0LC0xMTQxMzAwNDIz
LDQyODI0NzI5Nyw1NTMyMTQ4NjRdfQ==
-->