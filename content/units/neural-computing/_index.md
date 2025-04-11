---
title: "Neural Computation"
revised: 2025
weight: 10
---

## Key questions

- 375:
  - How do neural nets compute? (How does that differ from traditional programming?)
  - What are the "data structures" of neural computing and efficient operations we can do with them?
  - How can we update parameters to optimize an objective function?
- 376:
  - How can we represent text and other data as sequences?
  - How can we process and generate sequences using neural nets?
  - How can models capture and use nuanced long-range dependencies?

## Key objectives

After this course, I will be able to:

- 375:
  - I can compute the forward pass through a two-layer classification neural network by hand (or in simple code) and explain the purpose and operation of each part.
  - I can implement the following basic neural network primitives in efficient parallel code (using a library like NumPy or PyTorch): linear layers, elementwise nonlinearities (like ReLU), softmax, and loss functions like MSE and categorical cross-entropy.
  - I can draw clear diagrams of the data flow, including array shapes, for the forward pass and loss computation for the following models: linear regression, logistic regression, and a one-layer MLP.
  - I can interpret vectors of data as points in a space and explain similarity measures like the dot product.
  - I can use automatic differentiation APIs to compute and descend gradients.
- 376:
  - I can identify the shapes of data flowing through a Transformer-style language model.
  - I can sketch what the self-attention matrix would look like for a simple example.

## Learning Path

### CS 375

"I trained a neural net classifier from scratch."

1. Basic array/"tensor" operations in PyTorch
    - **Code**: array operations
    - **Concepts**: dot product, mean squared error
2. Linear Regression "the hard way" (but black-box optimizer)
    - **Code**: Representing data as arrays
    - **Concepts**: loss function, forward pass, optimizer
3. Logistic Regression "the hard way"
    - **Concepts**: softmax, cross-entropy loss
4. Multi-layer Perceptron
    - **Concepts**: nonlinearity (ReLU), initialization
5. Gradient Descent
    - **Concepts**: backpropagation, training loop
6. Data Loaders
    - **Concepts**: batching, shuffling

## Materials

- [Slides](/slides/computing.html)
