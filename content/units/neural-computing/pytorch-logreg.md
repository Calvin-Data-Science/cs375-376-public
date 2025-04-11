---
title: "PyTorch and Logistic Regression"
weight: 5
revised: 2025
---

## Logistic Regression

- Analogy: logistic regression is like linear regression, but for classification.
- Example: predict whether an email is spam or not (binary logistic regression), or predict which of several categories a news article belongs to (multiclass logistic regression).
- Plain-English: (1) multiply inputs by weights, (2) add a bias, (3) squash the result to numbers between 0 and 1, (4) train to make the right answer more likely.
- Technical definition:
    - `logistic_regression` input: an array `X` of shape `(samples, features)`
    - `logistic_regression` output: an array `y` of shape `(samples, classes)` where `y[i, j]` is the probability that sample `i` is in class `j`.
    - `logits = x @ W + b` where `W` is an array of shape `(features, classes)` and `b` is an array of shape `(classes,)`.
    - `logits` is then passed through the softmax function to get the output **probabilities**: `y = softmax(logits)`.
        - The softmax function is defined as `softmax(x) = exp(x) / sum(exp(x))`, where the sums are taken across the classes.
    - Categorical cross entropy loss (negative log likelihood) is used to train the model: `loss_i = -sum(y_true_onehot_i * log(y_pred_i))`.

```goat
                                                                correct answer
                                                                     |
                             (scores)                                v
                .--------.    logits   .---------.   probs    .---------------. 
in features --->| Model  +------------>| softmax +----------->| cross-entropy +-----> loss
                '--------' n_classes   '---------' n_classes  '---------------'        1
                           (a vector)              (a vector)                      (a number)
```


Jargon:

- **Logits** or **scores**: the inputs to the softmax function.
- **probabilities** or **probs**: the outputs of the softmax function.

## PyTorch

Imports:

```python
import torch
import torch.nn as nn
import torch.optim as optim
import torch.nn.functional as F
```

Building a model object with the desired architecture (structure)

```python
model = nn.Linear(in_features=2, out_features=3, bias=True)

# or

class Model(nn.Module):
    def __init__(self):
        super().__init__()
        self.linear = nn.Linear(in_features=2, out_features=3, bias=True)
    
    def forward(self, x):
        return self.linear(x)
model = Model()

# or

n_hidden = 100
model = nn.Sequential(
    nn.Linear(in_features=2, out_features=n_hidden, bias=True),
    nn.ReLU(),
    nn.Linear(in_features=n_hidden, out_features=3, bias=True)
)
```

Training a model:

```python
loss_fn = nn.MSELoss()
optimizer = torch.optim.SGD(model.parameters())
# in a training loop ...
y_pred = model(x)
loss = loss_fn(y_pred, y_true)
loss.backward()
optimizer.step()
```

## Warm-Up Activity

Given on paper.

1. We're classifying houses as low/medium/high price based on longitude and latitude using logistic regression. The model outputs 3 scores, one for each class. For 100 houses (processed all at once in a "batch" of samples):

   a. What shape is `X`? `X.shape = `

   b. What shape should `W` (the array of weights) be? `W.shape = `

   c. What shape should `b` (the array of biases) be? `b.shape = `
   
   d. What shape will the output have? `(X @ W + b).shape = `

2. For one house, if our model outputs scores `[1.0, 2.0, -1.0]` for low/med/high prices:
   
   Write the steps to convert these scores to probabilities that sum to 1. (You can use words or math notation.)

3. If the true label for this house is "medium", what's the model's *accuracy* and *loss* for this house? (You can use words or math notation.)

## Notebooks

{{% notebook name="From Linear Regression in NumPy to Logistic Regression in PyTorch" nbname="u04n3-logreg-pytorch.ipynb" %}}
