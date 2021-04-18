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


# Joint & Conditional Probability

**Joint Probability**: $p(x, y) = P(X=x, Y=y)$, the probability of $X=x$ and $Y=y$. 

**Conditional Probability**: $p(x|y)  = P(X=x|Y=y) = p(x, y)/p(y) $, the probability of $X=x$ given $Y=y$. 

**Sum Rule (marginalization/summing out)**:
$$ p(x) = \sum_yp(x,y)$$
$$p(x_1) = \sum_{x_2}\sum_{x_3}...\sum_{x_N}p(x_1, x_2, ..., x_N)$$

**Product/Chain Rule**:
$$p(x,y) = p(y|x)p(x)$$
$$p(x_1, ..., x_N) = p(x_1)p(x_2|x_1)...p(x_N|x_1,...,x_{N-1})$$

**Bayes Rule**:
$$p(x|y) = \frac{p(y|x)p(x)}{p(y)}=\frac{p(y|x)p(x)}{\sum_{x'} p(y|x')p(x')}$$

# Frequently Used Distributions



# References

[Github Stanford CS229 Machine Learning](https://github.com/afshinea/stanford-cs-229-machine-learning/blob/master/en/refresher-probabilities-statistics.pdf)

[Probability Basics for Machine Learning](http://www.cs.toronto.edu/~urtasun/courses/CSC2515/Tutorial-ReviewProbability.pdf)



