---
title: 'Probability Basics for Machine Learning'
date: 2021-04-18
permalink: /posts/2021/04/probability-basics
tags:
  - Probability
---

Note of Probability Basics.

# Notations and Definition

**Sample Space**: the space of all possible outcomes of an experiment denoted as $\mathcal{S}$.

**Random Variable**: the outcomes or states of the world, denoted as $X$.

**Permutation**: A permutation is an arrangement of $r$ objects from a pool of $n$ objects, in a given order. The number of such arrangements is given by $P(n, r)$, defined as,

$$ P(n, r) = \frac{n!}{(n-r)!}$$

**Combination**: A combination is an arrangement of $r$ objects from a pool of $n$ objects,  where the order does not matter. The number of such arrangements is given by $C(n, r)$, defined as,

$$ C(n,r) = \frac{P(n,r )}{r!} = \frac{n!}{(n-r)!r!}$$

We will write $p(x)$ to mean Probability $P(X = x)$. $p(x)$ is the probability density function (**PDF**):
- Assigns a number to each $x$ in sample space.
- Non-negative, $0 \le p(x) \le 1$, and sums (integrates) to 1.
- reflects how often does $x$ occur, or how much do we believe $x$.

**Cumulative distribution function (CDF)**- The cumulative distribution function $F$, which is motononically non-decreasing and is such that $\lim_{x\to -\infty} F(x) = 0$ and $\lim_{x\to +\infty} F(x) = 1$, is defined as :

$$ F(x) = P(X \le x)$$

**Expectation**:  $E[x] = \int_xx\cdot p(x)dx$

**Variance**: $Var(X) = E[(X-E[X])^2] = E[X^2] - E[X]^2$

**Standard Deviation**: $\sigma = \sqrt{Var(X)}$

**Transformation of random variables**- Let the variables $X$ and $Y$ be linked by some function. By noting $f_X$ and $f_Y$ the distribution of $X$ and $Y$ respectively, we have,

$$f_Y(y) = f_X(x)|\frac{dx}{dy}|$$

**Leibniz integral rule**: Let $g$ be a function of $x$ and potentially $c$, and $a,b$ boundaries that may depend on $c$. We have,

$$\frac{\partial}{\partial c}(\int_a^bg(x)dx) = \frac{\partial b}{\partial c} \cdot g(b) - \frac{\partial a}{\partial c} \cdot g(a) + \int_a^b\frac{g}{\partial c}(x)dx$$

**Chebyshev's inequality**: Let $X$ be a random variable with expected value $\mu$ and standard deviation $\sigma$. For $k,\sigma \gt 0$, we have the following inequality:

$$P(|X-\mu| \ge k\sigma) \le \frac{1}{k^2}$$


# Joint & Conditional Probability

**Joint Probability**: $p(x, y) = P(X=x, Y=y)$, the probability of $X=x$ and $Y=y$. 

**Conditional Probability**: $p(x\|y)  = P(X=x\|Y=y) = p(x, y)/p(y) $, the probability of $X=x$ given $Y=y$. 

**Sum Rule (marginalization/summing out)**:

$$ p(x) = \sum_yp(x,y)$$

$$p(x_1) = \sum_{x_2}\sum_{x_3}...\sum_{x_N}p(x_1, x_2, ..., x_N)$$

**Product/Chain Rule**:

$$p(x,y) = p(y|x)p(x)$$

$$p(x_1, ..., x_N) = p(x_1)p(x_2|x_1)...p(x_N|x_1,...,x_{N-1})$$

**Bayes Rule**:

$$p(x|y) = \frac{p(y|x)p(x)}{p(y)}=\frac{p(y|x)p(x)}{\sum_{x'} p(y|x')p(x')}$$

**Covariance**- We define the covariance of two random variables $X$ and $Y$ as follows, which is also noted as $\sigma_{XY}^2$.

$$Cov(X,Y) = E[(X-\mu_X)(Y-\mu_Y)] = E[XY] - \mu_X\mu_Y$$

**Correlation**: The correlation between two random variables $X$ and $Y$ are,

$$\rho_{XY}  = \frac{\sigma_{XY}^2}{\sigma_X \cdot \sigma_Y}$$

If $X$ and $Y$ are independent, then $\rho_{XY}=0$

# Frequently Used Distributions

| Type |Distribution  |PDF | E[x]| Var(X)|
|--|--|--|--|--|
| Discrete | $X\sim B(n,p)$, Binomal | $p(X=x) =\binom{n}{x}p^xq^{n-x},x\in[0, n]$| $np$| $npq$
| Discrete | $X\sim Po(\mu)$，Poisson |$p(X=x) =\frac{\mu^x}{x!}e^{-\mu}, x\in\mathbb{N}$ | $\mu$| $\mu$
| Continuous | $X\sim \mathcal{U}(a,b)$，Uniform |$f(x) = \frac{1}{b-a},x\in[a,b]$ | $\frac{a+b}{2}$| $\frac{(b-a)^2}{12}$
| Continuous | $X\sim \mathcal{N}(\mu,\sigma)$，Gaussian |$f(x) = \frac{1}{\sqrt{2\pi}\sigma}e^{-\frac{1}{2}(\frac{x-\mu}{\sigma})^2},x\in\mathbb{R}$ | $\mu$| $\sigma^2$
| Continuous | $X\sim Exp(\lambda)$，Exponential | $f(x)=\lambda e^{-\lambda x}, x\in \mathbb{R}_+$| $\frac{1}{\lambda}$| $\frac{1}{\lambda^2}$


**Exponential family**

$$p(x|\eta) = h(x)g(\eta)exp(\eta^T\mu(x))$$

where,
- $x$: discrete or continuous scalar/vector
- $\eta$: 'natural parameters'
- $\mu(x)$: some function of $x$.
- $g(\eta)$: normalier, $g(\eta)\int h(x)exp(\eta^T\mu(x))dx =1$

# Parameter Estimation

**Random Sample**- A random sample is a collection of $n$ random variables $X_1,X_2,...,X_n$ that are independent and identically distributed with $X$.

**Estimator**- Suppose a fixed parameter $\theta$ needs to be estimated. A estimator  is a function that maps the sample space to a set of estimates. An estimator of $\theta$ is denoted as $\hat{\theta}$.

**Error**- For a given sample $x$, the error of the estimator $\hat{\theta}$ is defined as,

$$e(x) = \hat{\theta}(x) - \theta$$

**Mean squared error** The MSE of $\hat{\theta}$ is defined as the expected value of the square errors:

$$MSE(\hat{\theta}) = E[(\hat{\theta}(X) - \theta)^2] $$

**Sampling deviation** For a given sample $x$, the sampling deviation of the estimator $\hat{\theta}$ is defined as,

$$d(x) = \hat{\theta}(x) - E[\hat{\theta}(X)] = \hat{\theta}(x) - E[\hat{\theta}]$$

**Variance** The variance indicates how far, on average, the collection of estimates are from the expected value of the estimates.

$$Variance = var( \hat{\theta}) = E[( \hat{\theta} - E[ \hat{\theta}])^2] $$

**Bias** The bias of an estimator $\hat{\theta}$ is defined as being the difference between the expected value of the distribution of $\hat{\theta}$ and the true value, 

$$Bias = B(\hat{\theta}) = E[\hat{\theta}] - \theta$$

The relation among MSE, variance and bias, 

$$MSE(\hat{\theta}) = var(\theta) + (B(\hat{\theta}))^2$$

**Sample mean and variance** $\bar{X} = \frac{1}{n}\sum_{i=1}^nX_i$, and $\sigma^2 = \frac{1}{n-1}\sum_{i=1}^n(X_i-\bar{X})^2$

**Central Limit Theorem** Let us have a sample $X_1, X_2, ..., X_n$ following a given distribution with mean $\mu$ and variance $\sigma^2$, then we have:

$$\bar{X} \sim_{n\to +\infty} N(\mu, \frac{\sigma}{\sqrt{n}}) $$

# Bayesian Probability

$$p(\theta|d) = \frac{p(d|\theta)p(\theta)}{p(d)}$$

$p(d|\theta)$ is the likelihood function

$p(\theta)$ is the prior probability of (or our prior belief over) $\theta$.

$p(d) = \int p(d\|\theta)p(\theta)d\theta$ is the normalization constant or partition function.

$p(\theta\|d)$ is the posterior distribution.

# References

[Github Stanford CS229 Machine Learning](https://github.com/afshinea/stanford-cs-229-machine-learning/blob/master/en/refresher-probabilities-statistics.pdf)

[Probability Basics for Machine Learning](http://www.cs.toronto.edu/~urtasun/courses/CSC2515/Tutorial-ReviewProbability.pdf)http://www.cs.toronto.edu/~urtasun/courses/CSC2515/Tutorial-ReviewProbability.pdf)
