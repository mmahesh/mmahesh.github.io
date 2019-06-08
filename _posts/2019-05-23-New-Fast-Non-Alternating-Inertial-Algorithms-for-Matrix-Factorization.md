---
layout: post
title:  "New Fast Non-Alternating Inertial Algorithms for Matrix Factorization"
date:   2019-05-23 
categories: [matrix factorization, matrix completion, non-convex optimization, Bregman distance, inertia,  machine learning, computer vision,mathematical optimization]
excerpt: "New Algorithms for Matrix Factorization problems such as NMF, Dictionary Learning, Sparse NMF and many others. Matrix Completion on MovieLens Dataset is also given."
comments: true
---
Our new paper titled [Beyond Alternating Updates for Matrix Factorization
with Inertial Bregman Proximal Gradient Algorithms](/show_pub5/){:target="_blank"} written  in collaboration with Peter Ochs is now online at arxiv. This work is based on our previous work on [Inertial Bregman Proximal Gradient Algorithm in Non-Convex Optimization](/articles/2019-04/Convex-Concave-Backtracking-for-Inertial-Bregman-Proximal-Gradient-Algorithms-in-Non-Convex-Optimization){:target="_blank"}. The abstract is given below.
<br><br>
>Matrix Factorization is a popular non-convex objective, for which alternating minimization schemes are mostly used. They usually suffer from the major drawback that the solution is biased towards one of the optimization variables. A remedy is non-alternating schemes. However, due to a lack of Lipschitz continuity of the gradient in matrix factorization problems, convergence cannot be guaranteed. A recently developed remedy relies on the concept of Bregman distances, which generalizes the standard Euclidean distance. We exploit this theory by proposing a novel Bregman distance for matrix factorization problems, which, at the same time, allows for simple/closed form update steps. Therefore, for non-alternating schemes, such as the recently introduced Bregman Proximal Gradient (BPG) method and an inertial variant Convex–Concave Inertial BPG (CoCaIn BPG), convergence of the whole sequence to a stationary point is proved for Matrix Factorization. In several experiments, we observe a superior performance of our non-alternating schemes in terms of speed and objective value at the limit point.

[Paper link](/show_pub5/){:target="_blank"} 

[arxiv link](https://arxiv.org/abs/1905.09050){:target="_blank"}

> Simple Illustration from Page 2.

![image](/simple_example.png)

> BPG for Matrix Factorization from Page 5.

![image](/bpg-mf.png)

> CoCaIn BPG for Matrix Factorization from Page 7.

![image](/cocain-bpg-mf.png)

