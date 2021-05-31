---
title: 'Gumbel-Softmax'
date: 2021-05-31
permalink: /posts/2021/05/Gumbel-Softmax/
tags:
  - Gumbel-Softmax
---



# Introduction

If we want to learn some discrete representations, like some categorical features with a neural network, we usually learn the parameters of such discrete distribution and sample from such that parametric distribution. However, we cannot back-propagate through samples.

![img](https://4.bp.blogspot.com/-fpP3tK8x5Xk/WCKuHOhS7qI/AAAAAAAAFKs/hGfcGjBC3msRhQczwPMoiWhfIOtnGL1CACEw/s320/gumbel1.png)

For example, the gradient can flow well in left figure, but stop at stochastic node $z$ in right figure.

# Gumbel-Softmax Distribution

The Gumbel-Softmax distribution is re-parameterization trick that can bypass the stochastic node during back propagation. An example of re-parameterization trick is used to train the variational autoencoders. Instead of directly sampling from the Gaussian distribution $(\mu, \sigma)$,  we reparameterize it as follows,
$$ z  = \mu + \sigma * \varepsilon, \text{where } \varepsilon \sim \mathcal{N}(0, 1)$$
The noise $\varepsilon$ is zero-mean to avoid the bias added. In such way, we dicomposite a stochastic sampling into separate deterministic and  stochastic components. 

![Fig 2](https://sassafras13.github.io/images/2020-08-13-GumbelSoftmax-fig2.png)

We first introduce the Gumbel-Max trick that  provides a simple way to draw samples $z$ from categorical distribution. 

$$z = \text{one\_hot}(\arg\max_i [g_i + \log(\pi_i)])$$

$g$ is the random noise from the Gumbel distribution $g = -\log(-\log(\mu)), \mu \sim \text{Uniform}(0,1)$.  A mathematical proof of Gumbel-Max is equivalent to the softmax operation can be found in [link](https://lips.cs.princeton.edu/the-gumbel-max-trick-for-discrete-distributions/).

![Fig 3](https://sassafras13.github.io/images/2020-08-13-GumbelSoftmax-fig3.png)

The $\arg\max$ operation is not differentiable. We replace it with softmax function, divided by a factor $\tau$.

$$z = \text{softmax} ((log(\pi) + g)/\tau)$$ 

![Fig 4](https://sassafras13.github.io/images/2020-08-13-GumbelSoftmax-fig4.png)

The $\tau$ is the constant referred as temperature. The temperature approaches to $0$, samples from Gumbel-Softmax distribution become one-hot and Gumbel-Softmax distribution is idential to the categorical distribution.

The authors explain that an annealing schedule that gradually reduces the temperature during the training. They start from some larger values and gradually descrease the value until it approachs to zero. Because the temperature balances the trade-off between the model accuracy and variance: at high temperature, the model has very low variance, which is good at training a robust model. However, as the temperature decreases, the variance also decreases. 

With the Gumbel-Softmax distribution, the probability distribution $\pi$ becomes the deterministic function which back propagate the gradient with low variance. 

    Notices: There are inconsistent notations between the text and image. The figures are from another blog. 

 