---
title: "Linear Regression the Really Hard Way (gradient descent)"
weight: 10
revised: 2024
---

<!-- #next-year We could do micrograd here? e.g., https://windowsontheory.org/2020/11/03/yet-another-backpropagation-tutorial/ -->

In today's lab, you'll write your own training loop.

We'll stick with linear regression since it's simple enough that you should be able to understand everything that is happening, yet also complex enough to demonstrate the basic ideas of gradient descent and backpropagation.

We'll also use **MAE** loss since (1) the gradients come out looking nice and (2) unlike linear regression with MSE loss, there's not a simple formula that would directly compute the results; we basically have to use gradient descent.

## Getting Started

{{% notebook name="Linear Regression the Hard Way" nbname="u03n1-linreg-manual.ipynb" %}}

The notebook for this week starts you off with one of several one-dimensional datasets. For now, keep `DATASET` set to `"toy"`, which is the same dataset as we used in the activity on Wednesday. Bring up your notebook from Wednesday also so you can check some of your calculations.

Find the cell marked "Working Cell". You'll be doing all of your work here (though you may make some other cells to, e.g., try out some calculations or inspect the values of some variables.)

## Step 1: Forward pass

Implement a forward pass of **linear regression with MAE loss** by implementing the following algorithm. (Avoid combining steps right now; you'll want the intermediate results soon.) **Each step should be one single line**; don't write functions or loops at this point.

1. Compute `y_pred` as the *dot product* between `x` and `weights`, plus `bias`.
2. Compute the residuals `resid`.
3. Compute `abs_resid` as the absolute values of `resid`.
4. Compute `loss` as the mean of `abs_resid`.
4. Append the current loss to the `losses` list.

Check that your forward pass works correctly by (1) setting the weights and bias variables to different values and checking that the "Fitted Model" plot (on the right) shows a line of the expected slope, and (2) checking that the MAE you compute is lower when the line seems to fit the data better. (*Compare your results with a neighboring group to check.*)

> Note: The cell shows two plots; the one on the left is the plot of how losses change. Since you have only computed one loss, that plot will be blank at first.

Put your weight and bias initializations back to 0 for the following steps.

## Step 2: Backprop through the loss

Now we'll start computing the gradients. The *backpropagation* algorithm is wonderful because it's *modular*: we only have to think about one part of the computation at a time. Let's start at the loss and, as the name suggests, work backwards.

The loss was computed as
$$ \text{MAE} = \frac{1}{n} \sum_{i=1}^n |y_i - \hat{y}_i| $$

How much does the MAE change as we wiggle each of the predicted y's? Well, two things happen to each wiggle: (1) the absolute-value operator might flip its sign, and (2) the division by $n$ scales it. So we just need to implement those two operations. We'll break it down:

1. Compute `n_points` as `x.shape[0]`
2. Compute the signs of the residuals using `np.sign(resid)`. *Do this first in a separate cell so that you can see what the result looks like, then implement it within your working cell once you're confident you understand what's going on.*
3. Scale the signs by dividing by `n_points`.
4. Check your results against the `d_mae_d_ypred` you computed in the Wednesday notebook. Are the values correct? *Are they of the correct sign?* Consider whether you might need to *negate* the result (by putting a `-` sign in front).
5. Store the result in a variable called `y_pred_grad`.

> Note: it's conventional to use `x_grad` as an abbreviation for the gradient of the *loss* with respect to some value `x`. Since all of the gradients we'll need to hang on to will be with respect to the loss, this ends up not being ambiguous.

## Step 3: Backprop through adding `bias`

Now let's compute `bias_grad`, i.e., d_loss/d_bias. Thanks to the chain rule, all we need to compute is d_bias/d_ypred; then we multiply (actually, dot-product) that by d_loss_d_ypred, *which we already computed(!)*, and we have the result.

As we noticed on Wednesday, the gradient of the bias is just the sum of `y_pred_grad` (i.e., a dot product of `y_pred_grad` with a vector of all 1's. You don't have to work out why this is right now, but if you want to do so later, the key observation is that when an output splits into multiple paths, we *add the gradients through each path*.)

1. Compute `bias_grad` as the `sum` of `y_pred_grad`.

We have now completed the *backward pass*. (We'll handle the gradient of `weights` in a moment.)

## Step 4: Gradient Descent Step

Now, let's take a step of *gradient descent*.

1. Update `bias` by subtracting `learning_rate` * `bias_grad`.

**Temporarily** comment out the `bias = np.array...` initialization line so that your bias starts at the updated value. Run the chunk a couple of times and **check that your loss decreased**.

**Uncomment** the initialization before moving on.

## Step 5: Training Loop

Put the forward pass, backward pass, and gradient descent step inside a `for i in range(num_iter)` loop. 

Everything else, including the initialization of the parameters and the `losses` log list, and the plotting part, *should be **outside** of the loop*.

Run the cell and check that your loss reaches a low value. Observe the plot of losses going down and then stabilizing.

## Step 6: Backprop through the weights

Now add code to compute the gradient for the `weights`, and update it according to the learning rate as well:

1. Compute `weights_grad` as `x.T @ y_pred_grad` (that's the *transpose* of the input, needed to get the dimensions to work out correctly).
2. Update `weights -= ... * weights_grad`

Now check that the loss is even lower.

## Step 7: Switch the loss to MSE

See if you can figure out how to do this yourself!

Check your work by switching to the `toy2` dataset and seeing if the MSE vs MAE loss converges to a different line. (Think about which one will be more swayed by the outlier point.)

> Note: make sure that you update the **gradient** accordingly. If you need help figuring out the gradient of MSE loss, try changing the loss to MSE in the Wednesday notebook and see if you can figure out the pattern.
>
> Or, you can realize that the steps in the backprop were actually:
>
> 1. Compute `n_points` as `x.shape[0]`
> 2. Back-propagate through the `mean` operation: compute `abs_resid_grad` as `1 / n_points`.
> 3. Backpropagate through the `abs` operation: compute `resid_grad` as `np.sign(resid)` times `abs_resid_grad`.
> 4. Backpropagate through the `y_true - y_pred` operation: this just flips the sign, so compute `y_pred_grad` by negating `resid_grad` (by putting a `-` sign in front, or multiplying by -1.
