---
title: "PyTorch Autograd and SGD"
revised: 2025
---

## How to Compute Gradients

- Numerical approximation: $\frac{f(x+h) - f(x)}{h}$
  - Pros: Easy to implement
  - Cons: Computationally expensive, not accurate
- Symbolic differentiation: $\frac{df}{dx}$
  - Pros: Accurate
  - Cons: Can make unwieldy expressions
- Automatic differentiation: `grad(f, x)`
  - Pros: Accurate, efficient, works even with billions of parameters
  - Cons: Can be hard to debug, requires intermediate values to be stored
  
## PyTorch Autograd

PyTorch uses automatic differentiation to compute gradients.

Example:

```python
import torch

# Let's call it "w" as if it were a weight in a neural network
w = torch.tensor(2.0, requires_grad=True)
y = w**2
y.backward()
print(w.grad)
```

After calling `y.backward()`, the gradient of `y` with respect to `w` is stored in `w.grad`.

## (Stochastic) Gradient Descent

If we want to minimize a function $f(w)$, we can use gradient descent:

1. Initialize $w$ randomly
2. Repeat:
   - Compute the gradient of $f$ with respect to $w$
   - Update $w$ by moving in the opposite direction of the gradient

If the function depends on some *data* (e.g., it's the loss of a neural network computed on a batch of data), we often use *stochastic gradient descent* (SGD):

1. Initialize $w$ randomly
2. Repeat:
   - Sample a batch of data
   - Compute the gradient of the loss with respect to $w$ on the batch
   - Update $w$ by moving in the opposite direction of the gradient

We call it *stochastic* because it uses a *stochastic* estimate of the gradient.

## Warm-Up Activity

Suppose we're trying to minimize a function $f(p) = p^2 + 2x + 1$ using gradient descent: 

```python
def f(p):
  return p**2 + 2*p + 1

def grad_f(p):
  # gradient of f with respect to p
  return ______________________

print(f(3)) # ______
print(grad_f(3)) # ______

# fill in the blank to minimize
p = random()
for i in range(100):
  p = ______________________
```

What should we fill in the blanks to minimize the function?

## Notebooks

{{% notebook name="Compute gradients using PyTorch" nbname="u06n2-compute-grad-pytorch.ipynb" %}}
