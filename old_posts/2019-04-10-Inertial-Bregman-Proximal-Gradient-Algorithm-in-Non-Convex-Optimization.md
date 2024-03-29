---
layout: post
title:  "Inertial Bregman Proximal Gradient Algorithm in Non-Convex Optimization"
date:   2019-04-10 
categories: [non-convex optimization, Bregman distance, inertia, Bregman proximal gradient (BPG),CoCaIn BPG,  machine learning, computer vision,mathematical optimization]
excerpt: "Fast Inertial Algorithms for Non-Convex Optimization."
comments: true
---
Our new paper titled [Convex-Concave Backtracking for Inertial Bregman Proximal
Gradient Algorithms in Non-Convex Optimization](https://www.researchgate.net/publication/332300750_Convex-Concave_Backtracking_for_Inertial_Bregman_Proximal_Gradient_Algorithms_in_Non-Convex_Optimization){:target="_blank"} written  in collaboration with Peter Ochs, Thomas Pock and Shoham Sabach is now online at arxiv. The abstract is given below.
<br><br>
>Backtracking line-search is an old yet powerful strategy for finding better step size to be used in proximal gradient algorithms. The main principle is to locally find a simple convex upper bound of the objective function, which in turn controls the step size that is used. In case of inertial proximal gradient algorithms, the situation becomes much more difficult and usually leads to very restrictive rules on the extrapolation parameter. In this paper, we show that the extrapolation parameter can be controlled by locally finding also a simple concave lower bound of the objective function. This gives rise to a double convex-concave backtracking procedure which allows for an adaptive and optimal choice of both the step size and extrapolation parameters. We apply this procedure to the class of inertial Bregman proximal gradient methods, and prove that any sequence generated converges globally to critical points of the function at hand. Numerical experiments on a number of challenging non-convex problems in image processing and machine learning were conducted and show the power of combining inertial step and double backtracking strategy in achieving improved performances.

[Paper link](https://www.researchgate.net/publication/332300750_Convex-Concave_Backtracking_for_Inertial_Bregman_Proximal_Gradient_Algorithms_in_Non-Convex_Optimization){:target="_blank"} 

[Follow up work on Matrix Factorization](/articles/2019-05/New-Fast-Non-Alternating-Inertial-Algorithms-for-Matrix-Factorization){:target="_blank"} 

[arxiv link](https://arxiv.org/abs/1904.03537){:target="_blank"}

> Algorithm given below as in Page 7.

![image](/cocain-bpg-algorithm.png)

