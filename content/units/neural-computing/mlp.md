---
title: "From Logistic Regression to the Multi-Layer Perceptron"
weight: 3
revised: 2024
---

## Objectives

- I've trained a logistic regression model with Keras (and seen how it's basically the same as PyTorch)
- I've applied logistic regression to the classic MNIST dataset
- I've seen how to extend logistic regression to a multi-layer perceptron (MLP) by adding a hidden layer and a nonlinearity

## Getting Started

Start with the following notebook:

- {{% notebook name="Linear and Logistic Regression with Keras" nbname="u05n2-logreg-mlp.ipynb" %}}


## Step 1: Linear Regression on MNIST (the wrong way)

Notice that we start with a cell that loads one of a set of datasets.  Start with `toy2` as before.

We'll first fit a linear regression with MSE loss. The code chunk provided does this.

{{% task %}}
1. Run the model-fitting chunk, then the plotting chunk that follows.
2. Bring up your Lab 3 notebook and check that the results are the same (both the line and the loss).
3. Switch to MAE loss (`loss='mae'`), rerun the fitting and plotting code, and check that the line and loss have changed.
4. Read through the code side by side with your Lab 3 code.
{{% /task %}}

There's nothing to turn in for this step. But as you compare this code with your Lab 3 code, try to identify:

1. For each part of this code chunk (except noted below), what part of your Lab 3 training loop does it correspond to?
2. What part of your Lab 3 code is entirely missing (because the framework takes care of it for you?)
3. There are several numbers in this code. What parts of the Lab 3 code does each one correspond to?

Note: the `keras.layers.Input()` layer does not process the data, it just checks that each sample has the expected shape.

Note 2: Remember that the model never depends on how many image we have. We specify what the model should do to each image independently; Keras handles applying that computation to every image.

## Step 2: Linear Regression on MNIST (Wrong Way 1)

Now, let's try to use this same approach to classify handwritten digits from the MNIST dataset.

We'll flatten the 28x28 images into 784-dimensional vectors. That part is okay, but as we saw on Wednesday, the rest of this approach is very wrong. Let's see why.

{{% task %}}
1. Switch back to MSE loss.
2. In the data-loading chunk, switch to `DATASET = 'mnist'`.
3. **Run All** again. **Stop and practice reading the exception you get** in the model-fitting code. As usual, start reading a Python traceback from the *bottom*; in this case, the main part of the error starts with "Input 0 of layer ... is incompatible". Study that line until you can understand all of it (except the name of the layer).
4. Change the `Input()` layer to have `shape=(784,)` and run again.
{{% /task %}}

Notice that (1) each epoch is taking much longer and (2) your loss is (probably) `nan`, i.e., not a number, i.e., too big to represent. Stop the cell; this is getting nowhere. (If you're using MAE loss your model may have actually converged, but switch to MSE to follow us.) Why? **The learning rate was too high**. Now that we're taking SGD steps based on *minibatches* of data, and there are far more parameters, the gradients are much more noisy--so taking too big of a step will make the model get *worse* on average. But since each epoch now actually does many updates, we don't need nearly as many.

{{% task %}}
1. Reduce the learning rate to 0.01, and reduce epochs to 5. (If you're getting impatient at this point, you can turn on an accelerator--but it doesn't actually help this network very much. Instead, take the time watching how the loss and accuracy change throughout training. You may notice some things that initially surprise you.)
2. Rerun the plot chunk. Since it no longer makes sense to show the predictions as a 1d function, the template code instead shows you a *histogram* of the predictions. 
{{% /task %}}

Since the weights correspond to pixels in an image, we can visualize the weights directly to see what the model has learned. **Uncomment the `show_weight_images(linear_layer)` chunk** and study the image that is shown. (Positive weights are blue, negative are red.) To me, this image is showing that the model is getting the predictions "right for the wrong reasons".

But how often is this model actually getting the *correct digit*?

{{% task %}}
1. Add `metrics=['accuracy']` to the `model.compile()` call. (Make sure your `loss` is still `mse`.)
2. Add `validation_split=.25` to the `model.fit()` call. This holds out 25% of the data as a validation set.
3. Meanwhile, let's also upgrade the optimizer to one that automatically tunes the learning rate: `optimizer=keras.optimizers.RMSprop()`.
{{% /task %}}

Reflection (not to turn in, but you'll need this for the analysis questions at the end.)

1. Write down the training and validation loss and accuracy you get for this model.
2. On a sheet of paper (or a good sketching app), draw a diagram of this model. Also write out how the model computes a prediction, either in math or in code.
3. Sketch on your paper the *distribution* of predicted values. What range of values do you get? Why does this make sense given the way we set up this model?

## Step 3: Linear Regression Predicting One-Hot (Wrong Way 2)

For classification, we want a score for each possible digit (0-9), so we need 10 outputs, one for each digit.

{{% task %}}
Change the model to output a score for each digit. (The `Dense` layer specifies the output shape.) Re-run. You'll get an error.
{{% /task %}}

We're getting an error because we're comparing 10 numbers (per sample) to just one number. We need a *target* that's like the output -- 10 numbers, with a "correct" score for each digit. Since each digit only has one label, there will be 1 special number (we'll use `1`) and 9 ordinary numbers (we'll use `0`). This is called a *one-hot encoding*.

{{% task %}}
Use `keras.utils.to_categorical(y_true, num_classes=10)` to one-hot encode the true labels; call the result `y_true_onehot` (don't overwrite our existing `y_true`). Do this in a new chunk, right before the model training code, since we'll need `y_true_onehot` for the model training:

```python
y_true_onehot = keras.utils.to_categorical(y_true, num_classes=10)
print('one hot shape', y_true_onehot.shape)
print('one hot example:')
print(y_true_onehot[:5])
```

{{% /task %}}

Make sure you understand both the `shape` and the example rows printed. Now that you've gotten the targets encoded appropriately:

{{% task %}}
1. Change the target to the one-hot-encoded targets, `y_true_onehot`.
2. Re-run training and plotting. Look at the weight images now; why are they that way?
{{% /task %}}

Let's show what the model predicted for the first training example; think about why this makes sense in light of the model and how it was trained:

```python
probs = model.predict(x[0:1])
plt.barh(np.arange(10), probs[0])
```

Repeat the reflection questions from Step 2.

## Step 4: Linreg + Softmax Predicting One-Hot (Almost-Right Way)

Add `activation='softmax'` to the `Dense()` layer.

What happened to the loss? The predictions?

Do the weight images make more sense now? **Think about why these make sense**.

Write down the training and validation loss and accuracy you get for this model. Repeat the other reflection questions also.

Again, show what the model predicted for the first training example.

## Step 5: Logistic Regression

Finally, note that we're using a loss function that's not appropriate for comparing discrete probabilitiies. MSE loss is the appropriate measure of badness of fit if the data was generated by a Gaussian distribution centered on the predicted value. But instead the data is actually a discrete choice between 10 options, which is better modeled as a *categorical* distribution. And for that, we want the ***categorical* cross-entropy loss**, which in ML jargon is usually called just "cross-entropy". That turns this model into what is conventionally called "logistic regression".

> Technically you could call the MSE a "Gaussian cross-entropy" but very few people would understand what you're talking about.

So, change `loss='crossentropy'` and repeat. Do the weights make more sense now? Repeat all the reflection questions here.

## Step 6: Evaluating By Hand

{{% task %}}
Compute the model's and accuracy on the *test* set (which got loaded when we loaded the data, as `test_images, test_labels`).
{{% /task %}}

To make sure you understand how the model is making predictions, **implement this step by hand**. Step by step:

1. Compute the model's `test_predicted_probs` by running the forward pass of the model on `test_images`. Use the `weights` and `bias` arrays that the plotting code extracted from the fitted model. Use these methods (only): matrix multiply (`@`), addition (`+`), and softmax (`keras.ops.softmax(some_var, axis=-1)`). Report the shape of `test_predicted_probs`.

  > **Note**: The `keras.ops.softmax` operation returns a `torch.tensor`. Convert it to a NumPy array by using `test_predicted_probs = np.array(test_predicted_probs)`. Otherwise the accuracy comparison will fail due to a [bug in PyTorch](https://github.com/pytorch/pytorch/issues/43579).

2. Compute the model's top prediction `test_predictions` for each image by finding the index of the highest value in each output of the model: Use the `np.argmax()` function on the `test_predicted_probs` array. You'll need to specify which `axis` for `np.argmax()` to use. Report the shape of `test_predictions`.
3. Compute the model's accuracy by computing the `np.mean` of the boolean array you get by comparing `test_predictions` for equality with the `test_labels`. Report the accuracy and error rate (100% minus accuracy).

Make sure you can explain the shape of each step.

## Step 7: Going Deeper

The dataset we're using, MNIST, was organized by Yann LeCun. His [website](http://yann.lecun.com/exdb/mnist/) has a table of results from different models on this dataset. The model we're trained so far corresponds to the top row of the table ("linear classifier (1-layer NN)"), which LeCun reported as having a test error rate of 12%. (I get significantly better accuracy than that; was he using the wrong loss?)

Let's replicate one of the other results in that table, the one labeled "2-layer NN, 800 HU, Cross-Entropy Loss".

{{% task %}}
Before your final `Dense` layer, add a `Dense` layer with 800 dimensions (jargon: "hidden units") and ReLU activation (`activation='relu'`). Repeat the experiment and also compute the *test* accuracy. How close is your result to the one in the table?
{{% /task %}}

**Congratulations, you've just trained a deep neural network**!

You'll need to upgrade your calculation of test accuracy to handle the new model. First, you'll need to extract the weights and biases of the new layers:

```python
w1, b1 = model.layers[-2].get_weights()
w2, b2 = model.layers[-1].get_weights()
```

Then compute the first layer's linear transformation. To compute the ReLU activation, use `np.maximum(y, 0)`. Then compute the second layer's output as before.

Note that the weight images code will not work for this model (there would be 8000 images to show!).

> Note: you might want to try this deeper model on the temps dataset first.

## Analysis

### Table

Make a table of the results you got for each model that we trained on the MNIST images (Steps 2 through 7; except step 6 since that's not a new model). I'll start you off:

| Model Description                    | Prediction Equation | Weights shape | Biases shape | Loss Function | Validation Loss | Validation Accuracy |
|------------------------------------|----------------------|---------------|--------------|----------------|-----------------|----------------------|
| Linear regression (one number output) | `y = x @ W + b` | (784, 1) | (1,) | MSE | | |
| Linear regression (10 number output) | `y = x @ W + b` |  |  |  | | |

You can make this table in Markdown using the following template (notice how the column widths don't have to match):

```
| Model Description                    | Prediction Equation | Weights shape | Biases shape | Loss Function | Validation Loss | Validation Accuracy |
|------------------------------------|----------------------|---------------|--------------|----------------|-----------------|----------------------|
| Linear regression (one number output) | `y = x @ W + b` | (784, 1) | (1,) | MSE | | |
| Linear regression (10 number output) | `y = x @ W + b` |  |  |  | | |
```

Note: we didn't compute the test-set accuracy for the earlier models, only the validation accuracy. You don't need to go back and compute the test-set accuracy for those models.

### Narrative

Make a bulleted list of the models in the table you just made. For each one:

1. Describe how its training setup was different from the prior one.
2. Describe why that difference should lead to an improvement in the results.
3. Give an example of what its predictions might look like (e.g., "floating-point numbers usually between -1 and 9.8"), and describe why that makes sense given the way we set up this model.
4. Describe how its accuracy differs from the previous one.

Then answer these general questions:

1. How is the `softmax` operation useful in classification?
2. Suppose an interviewer asks you "What's the difference between linear regression and logistic regression?" Describe at least two differences you could mention.
3. The weight images helped us see that even though some of the models were getting good accuracy, they were doing so for the wrong reasons. Consider the weight images for the logistic regression model (Step 5). Why did the weights look vaguely like the digits? Why did the weights look not exactly like the digits?
