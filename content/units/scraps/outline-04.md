---
title: "Friday class"
draft: true
---

Plan:

- [Exodus 21:33-36](https://www.biblegateway.com/passage/?search=Exodus+21%3A33-36&version=NIV&interface=print)
- Discussion topic presentation: [Autonomous Vehicles](../../../discussions/vehicles/)
- PyTorch can compute the gradient for us
  - Intuition of backpropagation
    - Not numerical gradient computation. It's "ill-conditioned" (viz. delta of 1e-3 vs 1e-4)
      > "Using the limit definition of the derivative for finite difference approximation commits both cardinal sins of numerical analysis:
        "*thou shalt not add small numbers to big numbers*", and "*thou shalt not subtract numbers which are approximately equal*". [Automatic differentiation in machine learning: a survey](https://arxiv.org/abs/1502.05767)
    - Not symbolic differentiation
  - How: tell it we want the gradient; call `result.backward()`
- Stochastic Gradient Descent: we only need a few points to find a descent direction
- Extend to a linear combination of basis functions
- PyTorch has a `Linear` layer.
- Loss functions and their gradients: MSE vs MAE
