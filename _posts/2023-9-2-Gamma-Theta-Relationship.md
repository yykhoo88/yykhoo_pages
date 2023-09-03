---
layout: post
mathjax: true
title: The option Gamma-Theta relationship
date:   2023-09-02
tags: [black-scholes]
---
<center><img src="/images/2023-09-02/gamma-theta.png" width="300" /></center>

Black-Scholes option traders always talked about the Gamma-Theta relationship. Specifically, if an option is delta hedged, there exist an approximated relationship between gamma and theta. To derive this let’s consider the Black Scholes PDE.

$$
\begin{align}
\frac{\partial V}{\partial t} + rS \frac{\partial V}{\partial S} + \frac{1}{2} \sigma^2 S^2 \frac{\partial^2 V}{\partial S^2}&= rV
\end{align}
$$

Now let's put in the usual symbol for sensitivities,

$$
\begin{align}
\theta + rS\Delta + \frac{1}{2} \sigma^2 S^2 \gamma &= rV \\
\theta + \frac{1}{2} \sigma^2 S^2 \gamma &= r [V-S\Delta]
\end{align}
$$

Now if we consider $\Delta \to 0$ and $V \to 0$ (assuming no free lunch) or some trader prefer to say when interest rate are low... Either way,

$$
\begin{align}
\theta + \frac{1}{2} \sigma^2 S^2 \gamma &= 0
\end{align}
$$

The math can go slightly further. See [Link](https://quant.stackexchange.com/questions/67821/how-to-derive-the-relationship-between-gamma-and-theta). However this formula is a useful estimation for the theta-gamma breakeven for an delta hedged option. Finally, just to build an intuition on this relationship, we read from Hull's book:

> When gamma is positive, theta tends to be negative. The portfolio declines in value if there is no change in S, but increases in value if there is a large positive or negative change in S. When gamma is negative, theta tends to be positive and the reverse is true: the portfolio increases in value if there is no change in S but decreases in value if there is a large positive or negative change in S. As the absolute value of gamma increases, the sensitivity of the value of the portfolio to S increases.