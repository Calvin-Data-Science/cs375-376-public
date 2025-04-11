---
title: "Linear Regression the Hard Way"
weight: 2
revised: 2025
---

The simplest "neural computation" model is linear regression. We'll implement it today so that we can understand each part of how it works.

To keep things simple we'll use a "black box" optimizer, a function that just takes the data and the loss function and finds the best values of the parameters. 

> Later we'll study how to optimize a function using stochastic gradient descent, and how to compute the gradients of the loss function with respect to the parameters using backpropagation.

## Warm-Up Activity

Go to [the interactive figures for the Understanding Deep Learning book](https://udlbook.github.io/udlfigures/).

1. Go to Figure 2.2 (Least squares loss). Adjust the sliders to try to make the loss bigger or smaller. **What are the highest and lowest values you can get for the loss?** What does the plot look like at those different settings? (consider the line, the data points, and the dashed lines).
2. How can you tell if you got a good setting for the sliders? Can you tell just by observing the loss (without looking at the plot of the data and the line)?

## Notebooks

### Single Linear Regression

Work through this notebook to practice linear regression with a single feature.

- {{% notebook name="Linear Regression the Hard Way" nbname="u03n1-linreg-manual.ipynb" %}}

### Multiple Linear Regression

To reinforce our understanding and extend our understanding of linear regression to multiple features, we'll work through this notebook:

- {{% notebook name="Multiple Linear Regression, the Hard Way" nbname="u04n1-multi-linreg-manual.ipynb" %}}
