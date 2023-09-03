---
layout: post
mathjax: true
title: The option Gamma-Theta relationship
date:   2023-09-02
tags: [Black-Scholes]
---
<center><img src="/images/2023-09-03/YieldCurve.png" width="500" /></center>

Black-Scholes option traders always talked about the Gamma-Theta relationship. Specifically, if an option is delta hedged, there exist an approximated relationship between gamma and theta. To derive this let’s consider the Black Scholes PDE.

$$
\begin{align}
\frac{\partial V}{\partial t} + rS \frac{\partial V}{\partial S} + \frac{1}{2} \sigma^2 S^2 \frac{\partial^2 V}{\partial S^2}&= rV \\
\frac{dE}{dt} &= \beta SI - \alpha E \\
\frac{dI}{dt} &= \alpha E - \gamma I \\
\frac{dR}{dt} &= \gamma I
\end{align}
$$