---
layout: post
title:  "Variants of RMSProp and Adagrad with Logarithmic Regret Bounds ( along with some Open questions )"
date:   2017-06-21 
categories: [online convex optimization, stochastic optimization, machine learning, deep learning]
excerpt: "My paper titled \" <a href='http://www.ml.uni-saarland.de/Publications/MukHei-VariantsRMSPropAdagradLogRegret.pdf' target='_blank' ><b>Variants of RMSProp and Adagrad with Logarithmic Regret Bounds</b></a> \" written  in collaboration with Prof. Dr. Matthias Hein, Saarland University has been accepted at ICML 2017. Please find the abstract below.
<br>
<br>
Adaptive gradient methods have become recently very popular, in particular as they have been shown to be useful in the training of deep neural networks. In this paper we have analyzed RMSProp, originally proposed for the training of deep neural networks, in the context of online convex optimization and show $\\sqrt{T}$-type regret bounds. Moreover, we propose two variants SC-Adagrad and SC-RMSProp for which we show logarithmic regret bounds for strongly convex functions. Finally, we demonstrate in the experiments that these new variants outperform other adaptive gradient techniques or stochastic gradient descent in the optimization of strongly convex functions as well as in training of deep neural networks.
<br>
<br>
Disclaimer: This article explores lot of mathematical details which may not be necessary if you want to use the algorithms especially from Deep learning background. So i will try to write a tutorial soon so that it would be to easy to understand the algorithms, SC-Adagrad in particular. Having said that, I  still think it is still a good idea to go through the paper <a href='http://www.ml.uni-saarland.de/Publications/MukHei-VariantsRMSPropAdagradLogRegret.pdf' target='_blank' >here</a>  and you can have a look at the end of the paper for  Deep learning experiments where we compare our methods exhaustively.
"
comments: true
---
My paper titled "Variants of RMSProp and Adagrad with Logarithmic Regret Bounds" written in collaboration with Prof. Dr. Matthias Hein, Saarland University has been accepted at ICML 2017. Please find the conference (short) version [here](http://www.ml.uni-saarland.de/Publications/MukHei-VariantsRMSPropAdagradLogRegret.pdf){:target="_blank"} and the long version [here](http://www.ml.uni-saarland.de/Publications/MukHei-VariantsRMSPropAdagradLogRegretLongVersion.pdf){:target="_blank"} or on arxiv [here](https://arxiv.org/abs/1706.05507){:target="_blank"}. Please find the abstract below.

>Adaptive gradient methods have become recently very popular, in particular as they have been shown to be useful in the training of deep neural networks. In this paper we have analyzed RMSProp, originally proposed for the training of deep neural networks, in the context of online convex optimization and show $$\sqrt{T}$$-type regret bounds. Moreover, we propose two variants SC-Adagrad and SC-RMSProp for which we show logarithmic regret bounds for strongly convex functions. Finally, we demonstrate in the experiments that these new variants outperform other adaptive gradient techniques or stochastic gradient descent in the optimization of strongly convex functions as well as in training of deep neural networks.

Also, this work leads to following open questions.

> Is there a optimal decay scheme for SC-Adagrad and SC-RMSProp? If so how much do we gain in the regret bounds?

> SC-Adagrad and SC-RMSProp are primarily proposed for Strongly convex problems, however they work very well on many deep networks in terms of generalization as well as optimization performance. So why is this the case? Is loss surface of deep nets more similar to strongly convex problems?

> Can the regret bounds of Adagrad and RMSProp (Ours) (see for Algorithm 3 in Page 5 [here](http://www.ml.uni-saarland.de/Publications/MukHei-VariantsRMSPropAdagradLogRegret.pdf){:target="_blank"}) be lower bounded? If so is it better than $$\log T$$?

> Clearly, it would be interesting to see how the bounds and performance changes in distributed setting (both synchronous and asynchronous).

> All the algorithms proposed in our paper, SC-Adagrad, SC-RMSProp and RMSProp (Ours) can be extended to use the full matrices. We are exploring this currently though it seems like we dont gain much in the regret bound and clearly the full matrix versions of the algorithms are not very helpful in large scale machine learning context.

Disclaimer: This article explores lot of mathematical details which may not be necessary if you want to use the algorithms especially in Deep learning. So i will try to write a tutorial soon so that it would be to easy to understand the algorithms, SC-Adagrad in particular. Having said that, I  still think it is still a good idea to go through the paper <a href='http://www.ml.uni-saarland.de/Publications/MukHei-VariantsRMSPropAdagradLogRegret.pdf' target='_blank' >here</a>  and you can have a look at the end of the paper for  Deep learning experiments where we compare our methods exhaustively.

There can be more open questions possible, but i will leave it here for now and will update whenever i get some time.