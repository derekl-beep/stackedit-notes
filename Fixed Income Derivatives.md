# Fixed Income Derivatives

## Overview

These notes are based on my coursework of [MATH 4511](https://prog-crs.ust.hk/ugcourse/2020-21/MATH) - Quantitative Methods for Fixed Income Derivatives back at [HKUST](https://www.ust.hk/home), Math Department, instructed by [Prof. Wu Lixin](https://www.math.ust.hk/~malwu/).

### Course description
Bond, bond markets and interest-rate derivatives markets. Yields, forward rate and swap rates. Yield-based risk management and regression-based hedging. Mortgage mathematics. Binomial models for equity and fixed-income derivatives. Arbitrage pricing and risk-neutral valuation principle. Eurodollar futures. Lognormal models and Black formula for caps and swaptions.

### Prerequisite(s)
- Multivariable calculus
- Linear algebra
- Probability
- Background in financial markets

### Textbook and Reference Books

Textbook
- Bruce, T. (2002) Fixed Income Securities: Tools for Today's Markets, 2nd edition (Wiley Finance)

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



## Discount Factors

The discount factor for a particular term indicate the **present value** of one unit currency to be received at the end of the term. 

The discount factors for different terms of a currency can usually be extracted from the corresponding Treasury bond prices because these bonds promoise future cash flows at a fixed interval of time. 

Denote the discount factor for $t$ years by $d(t)$.

Suppose the $1\frac{1}{4}\%$ s of November 30, 2010 (6 months from now) is trading at $100.550, so we have $$\begin{aligned} 100.550 &= (100+\frac{1\frac{1}{4}}{2})d(0.5) \\ d(0.5)&=0.99925\end{aligned}$$

### Bootstrapping the Discount Factors



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTk0NzM3NjkwLDQyODI0NzI5Nyw1NTMyMT
Q4NjRdfQ==
-->