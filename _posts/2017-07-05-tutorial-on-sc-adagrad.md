---
layout: post
title:  "Tutorial on new stochastic gradient methods for deep learning"
date:   2017-07-05 
categories: [online convex optimization, stochastic optimization, machine learning, deep learning]
excerpt: "This is a tutorial on SC-Adagrad, a new stochastic gradient method and some comparisions to other methods in particular Adam, SGD, Adagrad."
comments: true
---
This is a brief tutorial (without lot of mathematical details) on SC-Adagrad, a new stochastic optimization method proposed in [here](http://www.ml.uni-saarland.de/Publications/MukHei-VariantsRMSPropAdagradLogRegret.pdf){:target="_blank"}. Disclaimer: I am one of the author :). Clearly, there is an abundance of stochastic optimization methods for training deep neural networks. Recently, [Adam](https://arxiv.org/pdf/1412.6980.pdf){:target="_blank"} has become a go to optimization method for training deep nets. In this post, I will briefly review Stochastic Gradient Descent, Adam, Adagrad and finally dwell into the details of SC-Adagrad.

This is definitely not the first tutorial of its kind. There are many excellent blog posts which briefly summarize the stochastic optimization methods. Some of them are [BlogPost1](http://sebastianruder.com/optimizing-gradient-descent/){:target="_blank"} and [BlogPost2](http://colinraffel.com/wiki/stochastic_optimization_techniques){:target="_blank"}. In my opinion, if you read these blog posts before reading this post, you are more likely to understand SC-Adagrad algorithm better. For those who are more mathematically inclined, i would suggest to go through the [paper](http://www.ml.uni-saarland.de/Publications/MukHei-VariantsRMSPropAdagradLogRegret.pdf){:target="_blank"} instead.

Note: In the following algorithms, all the operations are element-wise. Also, my motive is to give a brief overview, so that you get an idea of the algorithm as easily as possible. Hence, i had to exclude lot of mathematical details.

## Stochastic Gradient Descent a.k.a SGD 

Let $g_t$  be your gradient while training a model with parameters at $t$-th instance denoted by $\theta_t$, and choosing $\alpha$ to the stepsize parameter the SGD update step is

$$\theta_{t+1}\gets\theta_t - \alpha g_t$$

## [Adam](https://arxiv.org/pdf/1412.6980.pdf){:target="_blank"}   

Choosing the same notation as SGD, we have some additional steps here

$$m_{t+1} = \beta_1 m_t + (1-\beta_1)g_{t}$$

$$\widehat{m}_{t+1} = \frac{m_{t+1}}{1-\beta_1^{t+1}}$$

$$v_{t+1} = \beta_2 v_t + (1-\beta_2)g_{t}^2$$

$$\widehat{v}_{t+1} = \frac{v_{t+1}}{1-\beta_1^{t+1}}$$

$$\theta_{t+1}\gets\theta_t - \alpha \frac{\widehat{m}_{t+1}}{\sqrt{\widehat{v}_{t+1}}+\epsilon}$$

Here $\epsilon$ is a numerical stability parameter.


## [Adagrad](http://www.magicbroom.info/Papers/DuchiHaSi10.pdf){:target="_blank"}

Adam was proposed after Adagrad, for conveniece i described Adam first and Adagrad here. Choosing the same notation as Adam, we have Adagrad as follows


$$v_{t+1} = \beta v_t + (1-\beta)g_{t}^2$$

$$\theta_{t+1}\gets\theta_t - \alpha \frac{g_t}{\sqrt{v_{t+1}}+\epsilon}$$


## [SC-Adagrad](http://www.ml.uni-saarland.de/Publications/MukHei-VariantsRMSPropAdagradLogRegret.pdf){:target="_blank"}

Choosing the same notation as Adam, we have Adagrad as follows


$$v_{t+1} = \beta v_t + (1-\beta)g_{t}^2$$

$$\theta_{t+1}\gets\theta_t - \alpha \frac{g_t}{v_{t+1}+\xi_2 e^{-\xi_1 v_{t+1}}}$$

Note there are two changes compared to Adagrad, 

> We removed the square root in the denominator of Adagrad

> Also we changed the numerical stability parameter from $\epsilon$ to $\xi_2 e^{-\xi_1 v_{t+1}}$ where  in general we choose $\xi_1=0.1, \xi_2=0.1$.

> Adagrad was developed for convex problems, whereas we developed the SC-Adagrad primarily for Strongly convex problems. To our surprise, it had excellent performance on many deep neural networks in particular ResNet-18, CNN and MLP.

The blogs mentioned earlier, do a pretty good job in going through the details of stochastic gradient methods. This post is just to get a brief overview of SC-Adagrad Algorithm. For detailed analysis in Online convex optimation framework, for getting to know equivalence of RMSProp and Adagrad, check our paper [here](http://www.ml.uni-saarland.de/Publications/MukHei-VariantsRMSPropAdagradLogRegret.pdf){:target="_blank"}.

Thanks for reading the post. Stay tuned for more updates. :)

<!-- TODO: Motivation, more details fill in other algorithms aswell
Give Code aswell maybe github repo
Add resnet, cnn exps -->
