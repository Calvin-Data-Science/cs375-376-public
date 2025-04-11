---
title: "Intro to Array Computing"
weight: 1
revised: 2025
---

You might have heard (or experienced) that Python is slow. So how can Python be the language behind basically all of the recent advances in AI, which all require huge amounts of computing? The secret is *array computing*. The Python code is orchestrating operations that happen on powerful "accelerator" hardware like GPUs and TPUs. Those operations typically involve repeatedly applying an operation to a big (usually rectangular) arrays of numbers, hence, *array* computing.

For those used to writing loops, this sort of coding can take some getting used to. Here are two exercises that previous students have found very helpful in getting their mind around how arrays work in PyTorch. (The concepts are basically identical in other libraries like TensorFlow, NumPy, and JAX.)

## Objectives

- Apply mathematical operations to arrays using PyTorch

## Notebooks

- {{% notebook name="PyTorch Warmup" nbname="u02n1-pytorch.ipynb" %}}
  - Dot Products
    - `for` loop approach
      - Torch Elementwise Operations
    - Torch Reduction Ops
    - Building a dot product out of Torch ops
  - Linear Layer
    - Linear layer, Module-style
  - Mean Squared Error
  - Multidimensional arrays
  - Appendix

The reference below is an AI-generated summary of the material in the notebook.

## Dot Products

A dot product is a fundamental operation in neural networks, particularly in linear (Dense) layers. Key concepts:

### Intuitions
- Measures similarity/alignment between vectors
- Can be thought of as "How much does the input look like this pattern?"
- In a Linear layer, performs rotation and stretching of input space
- Similar to multiple linear regression's weighted mixture

### Mathematical Form
Basic form: `y = w1*x1 + w2*x2 + ... + wN*xN + b`
- Each input `x[i]` is multiplied by its corresponding weight `w[i]`
- Results are summed together
- Often includes a bias term `b` (can be omitted for simplicity)

### Implementation Methods
1. Using PyTorch's built-in operations:
   - `torch.dot(w, x)` or `w @ x`
2. Using elementwise operations:
   - Multiply corresponding elements: `w * x`
   - Sum the results: `(w * x).sum()`

## Linear Transformations

A linear transformation is the basic building block of neural networks:
- Takes form: `y = w*x + b`
- `w` represents weights
- `b` represents bias
- Can be implemented as a function or as a class (Module-style)

## PyTorch Operations

### Elementwise Operations
- Operations between tensors of same shape happen element-by-element
- Example: `w * x` multiplies corresponding elements

### Reduction Operations
Common reduction methods:
- `sum()`: Adds all elements
- `mean()`: Computes average
- `max()`: Finds maximum value
- `argmax()`: Finds index of maximum value

Can be called as methods (`x.sum()`) or functions (`torch.sum(x)`)

## Mean Squared Error (MSE)

Common error metric for regression tasks.

Formula: MSE = (1/n)Σ(y_true - y_pred)²

Implementation steps:
1. Compute residuals: `y_true - y_pred`
2. Square residuals: `(y_true - y_pred)**2`
3. Take mean: `((y_true - y_pred)**2).mean()`

PyTorch provides built-in implementations:
- Functional style: `F.mse_loss(y_pred, y_true)`
- Module style: `nn.MSELoss()`

## Multidimensional Arrays

### Key Concepts
- Can have multiple axes (dimensions)
- Indexing can use positive or negative indices
- Shape determines valid operations

### Reduction Operations on Multiple Dimensions
- Can reduce along specific axes using `axis` parameter
- Reducing along an axis removes that dimension
- Example: `x.sum(axis=1)` sums along axis 1

### Tensor Products
- Reduces along middle axis
- Shape compatibility matters for successful operations
- Results in new tensor with specific shape based on input dimensions
