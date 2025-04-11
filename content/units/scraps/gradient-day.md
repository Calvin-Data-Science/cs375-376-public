---
title: "Gradient Day"
---

## Gradient day!


- [Gradient Game](https://ds100.org/su21/resources/assets/lectures/lec18/gradient_game_v3.html)

Activity code:

**Setup chunk:**

```python
import numpy as np
import matplotlib.pyplot as plt
```

**Calc Reminder**

```python
def approximate_gradient(f, x, eps=1e-6):
    return (f(x+eps) - f(x))/(eps)

def approximate_gradients(f, xx, eps=1e-6):
    xx = np.array(xx)
    result = []
    for i in range(len(xx)):
        delta = np.zeros_like(xx)
        delta[i] = eps
        result.append((f(xx+delta) - f(xx))/(eps))
    return np.array(result)

def f(x):
    return x**2

print(f"Gradient of f at x=2 is {approximate_gradient(f, 2.0)}")
```

**Linreg example setup:**

```python
x = np.array([0, 1, 2, 3])
y = np.array([-1, .5, 2.0, 3.5])
plt.plot(x, y, 'o')
```

```python
# Define parameters
w = 0.
b = 0.

# Define forward pass
def compute_ypred(w, b):
    return w * x + b

def compute_mae(y_pred):
    return np.mean(np.abs(y - y_pred))

def compute_mae_given_params(w, b):
    y_pred = compute_ypred(w, b)
    return compute_mae(y_pred)

# Show what it currently looks like
y_pred = compute_ypred(w, b)
plt.plot(x, y, 'o'); plt.plot(x, y_pred)
mae = compute_mae_given_params(w, b)
print("MAE:", mae)

# Functions to break it down
def compute_mae_given_w(w):
    return compute_mae_given_params(w, b)
def compute_mae_given_b(b):
    return compute_mae_given_params(w, b)
def compute_ypred_given_param_vec(xx):
    return compute_ypred(xx[0], xx[1])

# we computed things like:
# y_pred_grad = approximate_gradients(compute_mae, y_pred)
# approximate_gradient(compute_mae_given_w, w)
# approximate_gradient(compute_mae_given_w, b)
# and compare those with y_pred_grad.sum() and y_pred_grad @ x
```

Things we'll try to notice together:

1. The gradient gives an *ascent* direction.
  - Negative of grad is a *descent* direction.
  - But it's *local*: doesn't point towards *the* optimum
  - And you can step too far.
2. MAE grads are all +/- the same number; think about how this relates to how it's computed.
3. Bias grad is sum of MAE grad; think about why this makes sense.
4. Weight grad is dot of y_pred gradients with w.

