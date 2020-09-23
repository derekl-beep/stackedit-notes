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

When the first coupon is due in $\tau$ fraction of a half year, the bond price is further adjusted by a factor of $\big( 1+\frac{y}{2}\big)^{1-\tau}$.
```
<Insert cashflow diagram>
```

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

## Spot Rates

A spot rate is the rate on a spot loan, an agreement between a lender and a borrower at the time of the agreement, to be repaid at a later time.

Denote the semiannually compounded t-year spot rate by $\hat{r}(t)$. The spot rate and the discount factor are directly related as $$d(t)=\frac{1}{(1+\frac{\hat{r}(t)}{2})^{2t}}$$, or $$\hat{r}(t)=2 \Big(d(t)^{-\frac{1}{2t}}-1 \Big)$$. This also implies investing a unit dollar today will generate $(1+\frac{\hat{r}(t)}{2})^{2t}$ dollars in t years.


In fact, the discount factor, the swap rate, the spot rate and the forward rate of a certain term are directly related.

### Calculating a bond price by spot rates



$$\begin{aligned}
	P &= \frac{c}{2}\bigg[ \frac{1}{\big(1+\frac{\hat{r}(0.5)}{2}\big)} +\frac{1}{\big(1+\frac{\hat{r}(1)}{2}\big)^2}+ \dots +\frac{1}{\big(1+\frac{\hat{r}(T)}{2}\big)^{2T}} \bigg] + \frac{1}{\big(1+\frac{\hat{r}(T)}{2}\big)^{2T}} 
	\\
	&=\frac{1}{\big(1+\frac{\hat{r}(T)}{2}\big)^{2T}} +\frac{c}{2} \sum_{i=1}^{2T}\frac{1}{\big(1+\frac{\hat{r}(\frac{i}{2})}{2}\big)^{i}}
\end{aligned}
$$, where $P$ is the bond price, $c$ is the coupon rate; $\hat{r}(t)$ is the $t$-year spot rate compounded semiannually; and $T$ is the time to maturity in years.


## Forward Rates

A forward rate is the rate on a **forward loan**, which is an agreement to lend money at some time in the future to be repaid some time after that.

There are many possible forward rates, e.g. 
- the rate on a loan given in six months for a subsequent term of 1.5 years;
- the rate in five years for six months; etc.

This subsection, however, focuses exclusively on forward rates over **sequential six‐month periods**.

Let $f(t)$ denote the forward rate on a loan from year $t−0.5$ to year $t$. Then, investing 1 unit of currency from year $t−0.5$ for six months generates proceeds, at year $t$, of $$\Big(1+\frac{f(t)}{2} \Big)$$.

### Forward rates and spot rates

$$f(t)=2\bigg[ \frac{(1+\frac{\hat{r}(t)}{2})^{2t}}{(1+\frac{\hat{r}(t-0.5)}{2})^{2t-1}}-1 \bigg]$$

#### Proof

Consider two investment alternatives: 
1. A $t$-year loan
2. A $(t-0.5)$-year loan combined with a forward loan over $(t-0.5)$ to $t$ years

By the law of one price (LOOP), the returns are the same, so 
$$
\begin{aligned}
	\Big( 1+\frac{\hat{r}(t)}{2} \Big)^{2t} &= \Big( 1+\frac{\hat{r}(t-0.5)}{2} \Big)^{2(t-0.5)} \Big(1+\frac{f(t)}{2} \Big) \\
	&= \Big( 1+\frac{\hat{r}(t-0.5)}{2} \Big)^{2t-1} \Big(1+\frac{f(t)}{2} \Big) \\
\end{aligned}
$$, and rearranging the terms gives $$f(t)=2\bigg[ \frac{(1+\frac{\hat{r}(t)}{2})^{2t}}{(1+\frac{\hat{r}(t-0.5)}{2})^{2t-1}}-1 \bigg]$$.

Alternatively, a spot rate can be expressed as the product of sequential forward rates, i.e. 
$$\Big(1 + \frac{\hat{r}(t)}{2} \Big) ^ {2t} = \Big(1 + \frac{f(0.5)}{2} \Big) \Big(1 + \frac{f(1)}{2} \Big) \dots \Big(1 + \frac{f(t)}{2} \Big) =\prod_{i=1}^{2t}\Big(1 + \frac{f(\frac{i}{2})}{2} \Big)$$. Note that $f(0.5)=\hat{r}(0.5)$

### Forward rates and discount factors

$$f(t)=2\bigg[ \frac{d(t-0.5)}{d(t)} -1\bigg]$$



### Calculating a bond price by forward rates

$$\begin{aligned}
	P &= \frac{c}{2}\bigg[ \frac{1}{\big(1+\frac{f(0.5)}{2}\big)} +\frac{1}{\big(1+\frac{f(0.5)}{2}\big)\big(1+\frac{f(1)}{2}\big)}+ \dots +\frac{1}{\big(1+\frac{f(0.5)}{2}\big)\big(1+\frac{f(1)}{2}\big)\dots\big(1+\frac{f(T)}{2}\big)} \bigg] +\frac{1}{\big(1+\frac{f(0.5)}{2}\big)\big(1+\frac{f(1)}{2}\big)\dots\big(1+\frac{f(T)}{2}\big)} 
\end{aligned}
$$, where $P$ is the bond price, $c$ is the coupon rate; $f(t)$ is the six-month forward lend at $t-0.5$ year; and $T$ is the time to maturity in years.

## Swap Rates
// TBA

## Forward Rate Agreements (FRA)
// TBA

# 4 - One‐Factor Risk Metrics and Hedges

Overview 

Measure of risk
- DV01
- Duration
- Convexity  

Yield‐based risk management
- Hedge


## DV01

Suppose the price of a fixed income security is a function of a yield, $y$, then DV01 of the security is the change in price for one-basis point (i.e. 0.01%) of the change in yield.

$$DV01=-\frac{1}{10,000} \frac{\partial P}{\partial y}$$, or (practically)

$$DV01=-P(y+0.01\%)+P(y)=-\Delta P(y)$$. This measures the sensitivity of the price of the security to the yield.

The concept is similar to the delta value of an option, where $\Delta=\frac{\partial V}{\partial S}$, where $V$ is the option price, and $S$ is the underlying asset price.

### Example

The yield of 5s of 2/15/2011 at 2/15/2001 is $y=5%$. What is its $DV01$?

$P(y)=100$ because $c=y=0.05$.

$P(y+0.01\%)=100 \Big (\frac{0.05}{0.0501} \Big[ 1-\frac{1}{(1+\frac{0.0501}{2})^{20}} \Big] +\frac{1}{(1+\frac{0.0501}{2})^{20}} \Big)=99.9221$

$DV01=-99.9221+100=0.07791$

For 1 basis point change in the yield, the bond price is approximately changed (either increase / decrease) by $0.07791.

### Example

How about  when yield drops by one basis point?

$P(y-0.01\%)=100 \Big (\frac{0.05}{0.0499} \Big[ 1-\frac{1}{(1+\frac{0.0499}{2})^{20}} \Big] +\frac{1}{(1+\frac{0.0499}{2})^{20}} \Big)=100.0780$

$DV01=100.0780-100=0.0780$

Therefore, $P(y-0.01\%)-P(y) \neq P(y)-P(y+0.01\%)$.

For symmetry and higher accuracy, we redefine
$$DV01=-\frac{P(y+0.01\%)-P(y-0.01\%)}{2}$$. This is similar to the **central difference** in finite difference methods to calculate for numerical differentiation, which results in a higher accuracy.

## DV01 Hedging

Market makers in the fixed income market would like to maintain a DV01-neutural portfolio. A DV01-neutral portfolio implies a **small** changes in yield (or the overall interest rates) does not impact the total value of the portfolio.

This makes use of the first-order Taylor expansion of the portfolio value r.s.t. yield. The concept is similar to delta-hedging in the equity derivative markets.

If we hedge security A with security B, the face amount of B for hedging is given by

$$F_B = F_A \times \frac{DV01_A}{DV01_B}$$


### Example

A market maker sells \$ 100M face value of the call option when the yield is 5\%. How should the market maker hedge the market risk? Given $DV01_{option}=0.0369$ and $DV01_{bond}=0.0779$. 

Let $F$ be the face value for bond buying, then $F$ is subject to

$$F=\$100M \times\frac{0.0369}{0.0779}=\$47.37M $$

Checking: 

Market prices: Call: $3.0501; Bond: $100

$$\text{Portfolio} = -\$100M\times \frac{3.0501}{100}+\$47.37M \times \frac{100}{100}=\$44,319,900$$

If yield decreases by one bps, then the value of the portfolio (of short call and long bond) is

$$\text{Portfolio} = -\$100M\times \frac{3.0501+0.0369}{100}+\$47.37M \times \frac{100+0.0779}{100}=\$44,319,847$$

Hence, the change in the portfolio value is negligible.

## Duration

### Duration & DV01

$$
\begin{aligned}
	D &= -\frac{1}{P}\frac{\Delta P}{\Delta y} \\
	&=-\frac{10,000}{P}DV01
\end{aligned}
$$

As duration and DV01 is linearly related, duration-neutral and DV01-neutral is the same hedging strategy.



## Convexity

A second‐order Taylor approximation of the price‐rate function is

$$
\begin{aligned}
	P(y+\Delta y) &\approx P(y)+\frac{dP}{dy}\Delta y+\frac{1}{2}\frac{d^2P}{dy^2}\Delta y^2 \\
	\Delta P &\approx  \frac{dP}{dy}\Delta y+\frac{1}{2}\frac{d^2P}{dy^2}\Delta y^2  
\end{aligned}
$$. Dividing both side by the bond price gives

$$
\begin{aligned}
	\frac{\Delta P}{P} &\approx  \frac{1}{P}\frac{dP}{dy}\Delta y+\frac{1}{2}\frac{1}{P}\frac{d^2P}{dy^2}\Delta y^2   \\
	&= -D\Delta y+\frac{1}{2}C\Delta y^2
\end{aligned}
$$, where $C=\frac{1}{P}\frac{d^2P}{dy^2}$ is the convexity.

Practically, the convexity is obtained with the central difference method, i.e.
$$C=\frac{1}{P} \frac{P(y+\Delta y)-2P(y)+P(y-\Delta y)}{\Delta y^2}$$

### Approximation Quality

Please visit FIGURE 4.6 in Bruce, T. (2012) Fixed Income Securities: Tools for Today's Markets, 3rd edition. Wiley Finance. 

# 5 - Key Rate Hedging

A major weakness of the duration/DV01 based hedging is the assumption that yield curve does parallel shift. 

In reality, it is widely recognized that rates in different regions of the term structure are far from perfectly correlated.

The risk that rates along the term structure move by different amounts is known as **curve risk**.

# 6 - Regression‐based Hedging
// TBA

# 7 - The Science of Term Structure Models

## Lognormal Model for 
# 9 - The Art of Term Structure Models: Drifts

// TBA

# 16 - Swaps and Swapotions
// TBA

# 18 - Eurodollar Futures
// TBA

# 18II - The Black’s Formula for Caps and Swaptions

//TBA


---
More notes can be found on https://github.com/derekl-beep/cs-notes.

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU0NDQ5OTc4NCwtMTE5NjM1NTYyNCwtOT
QxMjkzMDc0LDM3ODcwNDM1OSw0MTcyODE5ODQsMzQyNDM5NTM0
LDE3NjkxMTM5MDYsLTczOTQ0NDgxMSwxNTAzMDUzMDIzLDU5NT
c2NzM2NSw4MTUxODE1OTIsNTc2Nzc3MTA0LC0xMTQxMzAwNDIz
LDQyODI0NzI5Nyw1NTMyMTQ4NjRdfQ==
-->