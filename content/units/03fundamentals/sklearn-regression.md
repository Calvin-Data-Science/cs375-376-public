---
title: 'Regression Models'
summary: 'Compare and contrast linear and tree-based regression models'
revised: 2025
---

Neural nets are strong performers for data that lacks clear features. But for well-structured tabular data with meaningful features (or data that can be translated to that form), simple models can sometimes perform very well, and can be much faster and sometimes more interpretable. Even if you plan to fit a neural net model, training a decision tree or random forest first can be a good quick first pass.

The Scikit-Learn (sklearn) `fit`-`predict` interface for modeling has become the *de facto* industry standard for this sort of modeling, so it's highly likely that what you see here will be useful in your future work.

## Objectives

- Contrast a training set and validation set; explain appropriate uses of both
- Use a decision tree for regression tasks
- Practice with the `fit` and `predict` interface of sklearn models
- Get a visual sense of how different regression models work.
- Explain underfitting and overfitting (TODO: this is actually in the classification notebook; move it there)

## Notebooks

{{% notebook name="Regression in scikit-learn" nbname="u02n2-sklearn-regression.ipynb" %}}

Note: the most important elements are:

- The Reflection section of Part 1
- The Analysis section at the end.

Upload your `.ipynb` files to Moodle. Make sure the names are sensible!

### Documentation

The sklearn documentation is exemplary. See:

- [Linear Models](https://scikit-learn.org/stable/modules/linear_model.html) for, e.g., linear regression
- [Decision Trees](https://scikit-learn.org/stable/modules/tree.html)
- [Ensemble Methods](https://scikit-learn.org/stable/modules/ensemble.html) for, e.g., random forests


## Libraries

We use *pandas* and NumPy for data wrangling, Matplotlib for plotting, and scikit-learn (sklearn) for the models.

Pandas (typically imported as `pd`, see above) is a very useful library for working with tabular datasets. For example, we can easily read a CSV file directly off the Internet.

The main object from pandas is a `DataFrame`:

- It holds a table of data. 
- Each column of data generally has a consistent data type. (Note: `object` columns are the exception. They usually mean "string", but could actually hold any Python object.)
- It behaves like a dictionary of its columns. Each column is a `Series` object.
- `Series` support broadcast operations, similar to NumPy arrays and Torch `tensor`s; they also have other functionality. (You can access the underlying NumPy array with the `.values` attribute.)

### Conventions

- `X` is typically used for input data (features)
- `y` is typically used for output data (labels)

Notice that `X` has two axes and thus is written in uppercase; `y` has 1 and thus is written in lowercase. (This is `sklearn` convention; other libraries are less consistent about this.)

The first index of both `X` and `y` is the sample index: `X` is a 2D array of shape `(n_samples, n_features)` and `y` is a 1D array of shape `(n_samples,)`.

### Data Splitting

To make sure we're evaluating how well the model *generalizes* (rather than just memorizing the training data), we split the data into a `train` and `valid` set. The model is fit on the `train` set and evaluated on the `valid` set.

Notes:

- Sometimes the `valid` set is called the *test* set. Sometimes there's all three: `train`, `valid`, and `test`.
- `random_state` is how `sklearn` specifies the random seed (it's actually slightly more flexible than a seed).

### Linear regression

- Make an instance of `LinearRegression` from `sklearn.linear_model`.
    - Making an instance sets up the structure of the model but doesn't actually fit it to data.
- The `fit` method takes `X` and `y` as arguments
- The `predict` method takes `X` and returns predicted `y` values (usually we call them `y_pred`)
    - since we have the actual `y` values in the `valid` set, we can compare them to the predicted values to compute error metrics
- The `score` method computes the R^2 score by default.
- The `coef_` attribute holds the coefficients of the model (the weights); the `intercept_` attribute holds the bias term.

Linear models construct their predictions as a linear combination of the input features. Viewed in the input space, linear models will always be flat, never bumpy or curvy.

Note: that doesn't mean that linear models can't be bumpy or curvy when viewed in a different space. For example, if you have a feature `x` and you add a feature `x^2`, the model can fit a parabola as a linear combination of `x` and `x^2`. This is the idea behind neural network models; they can fit very complex functions by composing simple functions. We'll dig into this soon.

### Metrics

sklearn has a number of metrics functions in `sklearn.metrics`. For regression, the most common are:

- `mean_squared_error`
- `mean_absolute_error`
- `r2_score`

The `score` method of sklearn regression models computes the R^2 score by default.

### Decision tree regression

Decision trees are a type of model that makes predictions by following a series of if-then rules. The rules are learned from the data. The tree is built by splitting the data into subsets based on the values of the features. The splits are chosen to minimize the error in the predictions.

In sklearn, decision trees for regression (sometimes called "regression trees") are implemented in the `DecisionTreeRegressor` class. The API is almost exactly the same as the `LinearRegression` class (it has `fit`, `predict`, and `score` methods).

Notice how the tree makes its prediction starting at the top (root) and checking one feature at a time. If the check is `True`, it goes left; otherwise, it goes right. When it hits a node with no check (a "leaf"), it predicts the value stored there. (Think: how do you think it might have computed that value?)

### Random Forest regression

Random Forests take random subsets of the data and fit decision trees to each one. As each tree is fit, it also considers only a random subset of features for each decision. The combination of these two reduces the *variance* of the model, that is, how much the model's predictions change if it's fit on different subsets of data.

## Analysis

These are the analysis questions from the notebook. You should answer them in your notebook.

1. Describe the basic steps for fitting a model in sklearn and making predictions.

2. Describe parameters that the `fit` method takes. For each one, describe its purpose and its shape.

3. Describe, qualitatively, what each of the 3 models here looks like in data space. Describe a characteristic of the visualization that would let you tell immediately which type of model it is from. You might notice differences in the shapes of the boundaries it draws and, if you look more closely, a difference in how the boundaries relate to the data.

4. Describe, quantitatively, how the performance of the different models compares. Which performs best? Which performs worst? Explain how the performance numbers make sense in light of the data-space plots.

## Extension

*optional*

1. Compute the loss on the *training* set for each of these models. Can that help you tell whether the model overfit or not?
2. Try using more features in the dataset. How well can you predict the price? Be careful about *categorical* features. (Note that you won't be able to use `plot_model` as-is if you add additional features.)

