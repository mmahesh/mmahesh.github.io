---
layout: post
title:  "Tutorial on SC-Adagrad and relevant stochastic optimization methods"
date:   2017-06-21 
categories: [online convex optimization, stochastic optimization, machine learning, deep learning]
excerpt: "This is a tutorial on SC-Adagrad"
comments: true
---
This is a tutorial on SC-Adagrad, a new stochastic optimization proposed in [here](http://www.ml.uni-saarland.de/Publications/MukHei-VariantsRMSPropAdagradLogRegret.pdf){:target="_blank"}. Clearly, there is an abundance of stochastic optimization methods for training deep neural networks. Recently, Adam has become a go to optimization method for training deep nets. I breifly review Stochastic Gradient Descent, Adam, Adagrad and finally dwell into the details of SC-Adagrad.

## Stochastic Gradient Descent a.k.a SGD

Let $g_t$  be your gradient while training a model with parameters at $t$-th instance denoted by $\theta_t$, and choosing $\alpha$ to the stepsize parameter the SGD update step is

$$\theta_{t+1}\gets\theta_t - \alpha g_t$$

## Adam

Choosing the same notation as SGD, we have some additional steps here

$$m_{t+1} = \beta_1 m_t + (1-\beta_1)g_{t}$$

$$\widehat{m}_{t+1} = \frac{m_{t+1}}{1-\beta_1^{t+1}}$$

$$v_{t+1} = \beta_2 v_t + (1-\beta_2)g_{t}^2$$

$$\widehat{v}_{t+1} = \frac{v_{t+1}}{1-\beta_1^{t+1}}$$

$$\theta_{t+1}\gets\theta_t - \alpha \frac{\widehat{m}_{t+1}}{\sqrt{\widehat{v}_{t+1}}+\epsilon}$$

Here $\epsilon$ is a numerical stability parameter.


## Adagrad

Adam was proposed after Adagrad, for conveniece i describe Adam first and Adagrad here. Choosing the same notation as Adam, we have Adagrad as follows


$$v_{t+1} = \beta v_t + (1-\beta)g_{t}^2$$

$$\theta_{t+1}\gets\theta_t - \alpha \frac{g_t}{\sqrt{v_{t+1}}+\epsilon}$$


## SC-Adagrad

Choosing the same notation as Adam, we have Adagrad as follows


$$v_{t+1} = \beta v_t + (1-\beta)g_{t}^2$$

$$\theta_{t+1}\gets\theta_t - \alpha \frac{g_t}{v_{t+1}+\xi_2 e^{-\xi_1 v_{t+1}}}$$

Note there are two changes to Adagrad here, 

> We removed the square root in the denominator of Adagrad

> Also we changed the numerical stability parameter from $\epsilon$ to $\xi_2 e^{-\xi_1 v_{t+1}}$ where  in general we choose $\xi_1=0.1, \xi_2=0.1$.


# TODO: Motivation, more details fill in other algorithms aswell
# Give Code aswell
# Add resnet, cnn exps

## RMSProp

## RMSProp as in [here](http://www.ml.uni-saarland.de/Publications/MukHei-VariantsRMSPropAdagradLogRegret.pdf){:target="_blank"}