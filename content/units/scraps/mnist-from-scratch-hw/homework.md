---
title: "Homework 3: MNIST Classifier from Scratch"
draft: false
---


## Task

Build a simple image classifier from scratch, using only basic numerical computing primitives (like matrix multiplication).

Specifically:

- Train a model to label the MNIST handwritten digits (10 classes, cross-entropy loss, see below for model details)
  - Highly recommended: plot the training loss and the validation loss.
- Evaluate the accuracy on the test (validation) set.
- Compare the results of the following different models (tune the learning rate and number of epochs as needed to get a good fit):
  - a single layer (logistic regression) model
  - a two-layer model with 30 hidden dimensions and ReLU activation.
  - (don't copy-paste the code; use flags to choose which to run, or write a function to do the training and call it with different parameters.)
- Optionally, also compare these variations:
  - try regularization, e.g., weight decay
  - Try different hidden dimensionality
  - Try to predict the digit as a *regression* task (i.e., predict a single number) using Mean Squared Error loss. Analyze the results -- why was this a bad idea?

Constraints:

- You may refer only to Fundamentals notebooks, and you must retype all code that you use for this assignment (except for the data-loading code provided below).
- Do not use any material other than the official documentation for PyTorch Tensors.
- Do not use any `fastai` capabilities beyond the data loading code provided.
  - In particular, don't use `Learner`. You should implement your own training loop.
- *Optional*: don't use `torch.nn` or `torch.optim`. You'll need to look at how `torch.nn.Linear` initializes its weights and implement that for yourself.
- *Optional*: do not use any of the PyTorch autograd mechanisms.

## Why?

- How everything works from the ground up
- Practice with array computing
- Build intuition for things like learning rates

Remember, this is about the *process*, not the result. You may be able to find a solution to this problem on the internet, but that's not the point. The point is to learn how to build a model from scratch, and to understand the process of training a model. If you find a solution on the internet, you should try to understand it, and then try to implement it yourself without looking at that solution. Please collaborate with your classmates, but all of the code you submit should be your own work.

## Instructions

Create a new notebook. You may start by copy-pasting this code, which sets up the data loading.

```python
# Import fastai, but only for the DataBlock part.
from fastai.vision.all import *

path = untar_data(URLs.MNIST)

# Create a subset of the images, so we train faster. We do this by taking 500 random images of each digit.
set_seed(0)
num_imgs_per_digit = 500
items = [
    p
    for split in ['training', 'testing']
    for digit in range(10)
    for p in (path/split/str(digit)).ls().shuffle()[:num_imgs_per_digit]
]

# Create the `dataloaders`. We need a slightly special `ImageBlock` because we want grayscale images.

block = DataBlock(
    blocks=(ImageBlock(PILImageBW), CategoryBlock),
    get_y = parent_label,
    splitter=GrandparentSplitter(train_name='training', valid_name="testing"),
)
dataloaders = block.dataloaders(items, bs=16)
print(f"{dataloaders.train.n} training images, {dataloaders.valid.n} validation images")
```

Beyond that, you're on your own! See "constraints" above.

## Optional Constraint: No Autograd

I have a suggested structure for implementing backpropagation yourself in a modular way. If you're interested, please ask me.

Note: the PyTorch `cross_entropy` function does some interesting things under the hood. See {{% notebook name="this notebook" nbname="cross_entropy_logsumexp.ipynb" %}}.

## Suggested Steps

(This section was written largely by GitHub Copilot -- and then rewritten, so I'm not sure how much Copilot text is left.)

1. Start with one of the labs that does something similar, such as the MNIST logistic regression lab. Don't copy-paste code; retype everything you need for this assignment.
2. Add a second layer, like we did in lab. Make sure to add the ReLU. Tune the learning rate and number of epochs to get a good fit.
3. Compare the results of the two models.
4. Try some variations, like changing the number of hidden dimensions.
5. Try one of the optional extensions, like replacing `nn.Linear` with your own implementation. You can start with the implementation you wrote in prior labs.

Some things to check:

- Did you include biases in the linear layers? Why or why not?
- How's your initialization? Compute what loss you'd expect at the start of training, and make sure your loss is starting out around there.
- Is the 2-layer network getting a substantially lower loss than the 1-layer network?

## Reflection Questions

- What did you learn about neural networks from this exercise?
- What did you learn about your own problem-solving process?
- How would you describe this experience in a job interview?
