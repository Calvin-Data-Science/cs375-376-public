---
title: 'Classification Models'
summary: 'Apply linear and tree-based classification models to a dataset; compare metrics'
revised: 2026
weight: 3
---



## Objectives

- Practice with the `fit` and `predict` interface of sklearn models
- Use linear models and decision trees for classification tasks
- Explain the difference between accuracy and log loss
- Explain underfitting and overfitting

## Notebooks

{{% notebook name="Classification in `scikit-learn`" nbname="u03n2-sklearn-classification.ipynb" %}}

**For reference only**, you might want to have your sklearn-regression notebook open: {{% notebook name="Regression in `scikit-learn`" nbname="u02n2-sklearn-regression.ipynb" %}}

## Key Concepts

### Reframing Regression as Classification

Rather than predicting exact home prices (regression), we'll predict price *categories* (classification):

- Low (bottom third)
- Medium (middle third) 
- High (top third)

Why? Price distribution is highly skewed - a small error on expensive homes dominates the loss. Classification evens out the importance. *Really, we're mostly doing this to help you see the difference between these two types of problems.*

> **Watch out**: Notice that the class is expressed as a *number* (0, 1, 2), but this is *not* a regression problem. The numbers are just labels for the classes.

### Cross-Entropy Loss

- Measures how *surprised* the model is by the correct answer
- Example: Model predicts probabilities [0.7, 0.2, 0.1] for classes [Low, Med, High]
  - If true class is Low: -log(0.7) = 0.36 (not very surprised)
  - If true class is High: -log(0.1) = 2.30 (very surprised!)
- Perfect prediction: probability 1.0 on correct answer, 0 elsewhere → loss = 0 
- Random guessing: probability [1/3, 1/3, 1/3] → loss = 1.10

```
      True Class
      ↓ 
[0.7, 0.2, 0.1] → -log(prob of true class)
 ↑
Model's predicted probabilities
```

## Working Through the Notebook

1. **Data Setup**

   - Use same X (lat/long) as regression
   - New y: price_bin column (0=low, 1=med, 2=high)
   - Split into train/validation sets

2. **Three Models**

   - Logistic Regression: Linear boundaries between classes
   - Decision Tree: Box-like regions
   - Random Forest: Smooth combination of many trees

3. **For Each Model**

   - Fit on training data
   - Plot probability contours
   - Compute accuracy and cross-entropy loss
   - Compare training vs validation performance

## Analysis Tips

- Look at probability plots:
  - Sharp vs smooth boundaries? 
  - Simple vs complex shapes?
  - High vs low confidence?

- Compare metrics:
  - Accuracy: Fraction correct
  - Cross-entropy: (average of negative-log of) confidence in correct answer
  - A model can have high accuracy but high cross-entropy if either (1) not confident enough when it's correct or (2) over-confident when it's wrong

- Identify overfitting/underfitting:
  - Underfitting: can't capture patterns in training data
  - Overfitting: captured patterns that aren't real / won't generalize
