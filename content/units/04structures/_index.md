---
title: "Unit 4: Neural Models"
weight: 4
revised: 2024
---

In this unit we extend our modeling skills to encompass classification models, and start to build the tools that will let us represent complex functions by using hidden layers. Both of these objectives require us to learn about *nonlinear* operations. We'll focus on the two most commonly used ones: the *softmax* operator (which converts scores to probabilities) and the *rectifier* ("ReLU", which clips negative values).

{{< unit_objectives "04structures" >}}

<!-- - [$1 gesture recognizer](https://depts.washington.edu/acelab/proj/dollar/index.html) for a different style of simple model (we won't study this) -->

## Automatic Differentiation

We'll be doing some automatic differentiation this week:

- [Yet another backpropagation tutorial](https://windowsontheory.org/2020/11/03/yet-another-backpropagation-tutorial/) by Harvard CS Professor Boaz Barak
[Overview of PyTorch Autograd Engine | PyTorch](https://pytorch.org/blog/overview-of-pytorch-autograd-engine/)
- [Automatic differentiation in machine learning: a survey](https://arxiv.org/abs/1502.05767)
- [`autograd-for-dummies`: A minimal autograd engine and neural network library for machine learning students.](https://github.com/malwaredllc/autograd-for-dummies)
