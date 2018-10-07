---
layout: post
title:  "Tutorial on new stochastic gradient methods for deep learning"
date:   2017-07-05 
categories: [stochastic optimization, machine learning, deep learning]
excerpt: "This is a brief tutorial (without a lot of mathematical details) on SC-Adagrad, a new stochastic optimization method proposed in the ICML paper <a href='/show_pub1/' target='_blank' ><b>here</b></a> . Disclaimer: I am one of the authors :). This is a joint work with Prof. Dr. Matthias Hein, Saarland University. Clearly, there is an abundance of stochastic optimization methods for training deep neural networks. Recently, Adam has become a go to optimization method for training deep nets. In this post, I will briefly review Stochastic Gradient Descent (SGD), Adam, Adagrad, RMSProp and finally dwell into the details of SC-Adagrad, SC-RMSProp and a new variant of RMSProp that we proposed."
comments: true
---
This is a brief tutorial (without lot of mathematical details) on SC-Adagrad, a new stochastic optimization method proposed in [here](/show_pub1/){:target="_blank"}. Disclaimer: I am one of the authors :). This is a joint work with Prof. Dr. Matthias Hein, Saarland University . Clearly, there is an abundance of stochastic optimization methods for training deep neural networks. Recently, [Adam](https://arxiv.org/pdf/1412.6980.pdf){:target="_blank"} has become a go to optimization method for training deep nets. In this post, I will briefly review Stochastic Gradient Descent (SGD), Adam, Adagrad, RMSProp and finally dwell into the details of SC-Adagrad, SC-RMSProp and a new variant of RMSProp that we proposed.

This is definitely not the first tutorial of its kind. There are many excellent blog posts which briefly summarize the stochastic optimization methods like [this](http://sebastianruder.com/optimizing-gradient-descent/){:target="_blank"} and [this](http://colinraffel.com/wiki/stochastic_optimization_techniques){:target="_blank"}. In my opinion, if you read these blog posts before reading this post, you are more likely to understand the SC-Adagrad algorithm better. For those who are more mathematically inclined, I would suggest to go through the [paper](/show_pub1/){:target="_blank"} instead.

Note: In the following algorithms, all the operations are element-wise. Also, my motive is to give a brief overview, so that you get an idea of the algorithm as easily as possible. Hence, I had to exclude lot of mathematical details.

## Stochastic Gradient Descent a.k.a SGD

Let $g_t$  be your gradient while training a model with parameters at $t$-th instance denoted by $\theta_t$, and choosing $\alpha$ to the stepsize parameter the SGD update step is

$$\theta_{t+1}\gets\theta_t - \alpha g_t$$

## [Adam](https://arxiv.org/pdf/1412.6980.pdf){:target="_blank"}   

Choosing the same notation as SGD, and with some additional steps,Adam algorithm is as follows

$$m_{t} = \beta_1 m_{t-1} + (1-\beta_1)g_{t}\\
\widehat{m}_{t} = \frac{m_{t}}{1-\beta_1^{t}}\\
v_{t} = \beta_2 v_{t-1} + (1-\beta_2)g_{t}^2\\
\widehat{v}_{t} = \frac{v_{t}}{1-\beta_2^{t}}\\
\theta_{t+1}\gets\theta_t - \alpha \frac{\widehat{m}_{t}}{\sqrt{\widehat{v}_{t}}+\epsilon}$$


Here $\epsilon$ is a numerical stability parameter. The terms $m_{t}$ and $v_{t}$ represent the second order moments of the gradient. Depending on how the moment is calculated, the bias correction term has to be applied to obtain $$\widehat{m}_{t}$$ and $$\widehat{v}_{t}$$ respectively. Please find the details in the Adam paper [here](https://arxiv.org/pdf/1412.6980.pdf){:target="_blank"}.

## [RMSProp](http://www.cs.toronto.edu/~tijmen/csc321/slides/lecture_slides_lec6.pdf){:target="_blank"}

Choosing $\beta > 0$ typically $0.9$ the RMSProp algorithm is given by

$$
v_{t} = \beta v_{t-1} + (1-\beta) g_{t}^2\\
\theta_{t+1}\gets\theta_t - \alpha \frac{g_t}{\sqrt{v_{t}}+\epsilon}
$$

We propose a new modified variant of RMSProp as follows

$$\beta_t = 1 - \frac{1}{t}\\
v_{t} = \beta_t v_{t-1} + (1-\beta_t) g_{t}^2\\
\theta_{t+1}\gets\theta_t - \alpha \frac{g_t}{\sqrt{tv_{t}}+\delta}$$

where $0<\gamma \leq 1$ and $\delta > 0$ typically $10^{-8}$. For more details, see Section 4 [here](/show_pub1/){:target="_blank"}.

## [Adagrad](http://www.magicbroom.info/Papers/DuchiHaSi10.pdf){:target="_blank"}

Adam was proposed after Adagrad, but for convenience, I described Adam before Adagrad here. Choosing the same notation as Adam, the Adagrad algorithm is as follows 


$$v_{t} = v_{t-1} + g_{t}^2\\
\theta_{t+1}\gets\theta_t - \alpha \frac{g_t}{\sqrt{v_{t}}+\epsilon}$$

Unlike Adam, the first order moments are ignored. Even though it seemed like the second order moment is not calculated, Adagrad actually computes the second order moment. We describe this in the subsection 2.3 [here](/show_pub1/){:target="_blank"}. Also this leads to an interesting phenomenon that Adagrad is a special case of RMSProp which we describe in Section 4 in detail.

## [SC-Adagrad](/show_pub1/){:target="_blank"}

Now, we provide the SC-Adagrad below

$$v_{t} = v_{t-1} + g_{t}^2\\
\theta_{t+1}\gets\theta_t - \alpha \frac{g_t}{v_{t}+\xi_2 e^{-\xi_1 v_{t}}}$$

Note these are the changes compared to Adagrad, 

> We removed the square root in the denominator of Adagrad

> Also we changed the numerical stability parameter from $\epsilon$ to $\xi_2 e^{-\xi_1 v_{t}}$ where  in general we choose $\xi_1=0.1, \xi_2=0.1$.

> Adagrad was developed for convex problems, whereas we developed the SC-Adagrad primarily for Strongly convex problems. To our surprise, it had excellent performance (in terms of Test accuracy) on many deep neural networks in particular ResNet-18, CNN and MLP.


## [SC-RMSProp](/show_pub1/){:target="_blank"}
In the same spirit of RMSProp, we have SC-RMSProp given by

$$\beta_t = 1 -\frac{1}{t}\\
v_{t} = \beta_t v_{t-1} + (1-\beta_t) g_{t}^2\\
\theta_{t+1}\gets\theta_t - \alpha \frac{g_t}{tv_{t}+\xi_2 e^{-\xi_1 tv_{t}}}$$

where $0<\gamma \leq 1$. 

The blogs mentioned earlier, do a pretty good job in going through the details of stochastic gradient methods. This post just tries to give a brief overview of SC-Adagrad, SC-RMSProp Algorithms. For detailed analysis on the online convex optimation framework, for getting to know the equivalence of RMSProp and Adagrad, check our paper, to see empirical results on ResNet-18 network, CNN and MLP see [here](/show_pub1/){:target="_blank"} or [here](http://www.ml.uni-saarland.de/Publications/MukHei-VariantsRMSPropAdagradLogRegretLongVersion.pdf){:target="_blank"}.


## Overview 
[Code](https://github.com/mmahesh/variants_of_rmsprop_and_adagrad){:target="_blank"}

<a href='/icml_slides.pdf' target='_blank'>[Slides here]</a>
<br>
<a href='/main.pdf' target='_blank'>[Poster here]</a>
<br>
<div align="center">
  <a href='https://raw.githubusercontent.com/mmahesh/variants_of_rmsprop_and_adagrad/master/poster_image.jpg' target='_blank'><img src="https://raw.githubusercontent.com/mmahesh/variants_of_rmsprop_and_adagrad/master/poster_image.jpg" target='_blank'></a><br><br>
</div>


Thanks for reading the post. Stay tuned for more updates. :)

## References:

[Adagrad Paper](http://www.magicbroom.info/Papers/DuchiHaSi10.pdf){:target="_blank"}

[RMSProp Slides](http://www.cs.toronto.edu/~tijmen/csc321/slides/lecture_slides_lec6.pdf){:target="_blank"}

[Adam Paper](https://arxiv.org/pdf/1412.6980.pdf){:target="_blank"}

[SC-Adagrad,SC-RMSProp paper](http://www.ml.uni-saarland.de/Publications/MukHei-VariantsRMSPropAdagradLogRegret.pdf){:target="_blank"}

and ofcourse

[BlogPost1](http://sebastianruder.com/optimizing-gradient-descent/){:target="_blank"}

[BlogPost2](http://colinraffel.com/wiki/stochastic_optimization_techniques){:target="_blank"}

and other interesting reads

[UFLDL Tutorial Post1](http://ufldl.stanford.edu/tutorial/supervised/OptimizationStochasticGradientDescent/){:target="_blank"}

[Deep learning book Chapter](http://www.deeplearningbook.org/contents/optimization.html){:target="_blank"}

[Stanford C231n notes](http://cs231n.github.io/optimization-1/){:target="_blank"}
<!-- TODO: Motivation, more details fill in other algorithms aswell
Give Code aswell maybe github repo
Add resnet, cnn exps -->
