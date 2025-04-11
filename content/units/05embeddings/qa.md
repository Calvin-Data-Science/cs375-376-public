---
title: "Week 5 Q&A"
date: 2022-02-10
---

## Reflections

### How do I see when everything is due?

Click Calendar in the left sidebar in Moodle.

Each week's web page also has a "Due this week" section with links to the assignments.

### Does the magnitude of the gradient approach zero when we're done training?

Not necessarily, especially with *stochastic* gradient descent and techniques like Dropout: there will always be some noise in the gradient. The parameters end up dancing around an area where loss is low.

### Does a trained classifier use average images?

Chapter 4 started by giving an example by averaging the pixel values of the 3's and 7's to make simple prototype images. But a trained image classifier will do something much more effective than that: it computes abstract vectorized representations of images where images that are in the same class *are* nearby each other. The final linear+softmax layer still just picks the class that has the prototype image vector that's closest to the current image. Those prototype image-vectors may happen to be near a weighted average of the images in that class, but there's no guarantee that that will happen (or that it produces the optimal classification).

### Why use MSE when it's so sensitive to outliers?

If we have to guess a single number for everything, the *mean* is the value that minimizes the MSE. So this question comes down to: why ever use the mean instead of the median?

One reason is that, if there *aren't* big outliers, the sample mean has less variance. Intuition: the median ignores the actual values of all but one or two data points; if you shifted every data point except the middle one up or down, the median won't change but the mean will.

### What are the parameters of a linear layer anyway?

You see this in the Fundamentals notebook where you trace the book's image classifier: the `Linear` layer has a `weights` that's `in_features` by `out_features`, and a `bias` that's `out_features` big.

The linear layer makes line-like relationships between each of its inputs and each of its outputs. Look at just one output (they're all independent anyway), which will just be a single number. If you change one of the inputs but keep all of the other inputs at the same value, and you plot the output vs that input you're changing, you'll get a line. The slope of that line is given by the weight that connects that input with that output, and the intercept of that line will be given by the bias for that output plus each of the other inputs times its corresponding weight.

### Is anyone held responsible for AI systems with racial bias?

Many people argue there's not enough accountability.

- The ACM conference on Fairness, Accountability, and Transparency ([ACM FAccT](https://facctconference.org/)) highlights work on some of the sociotechnical aspects of accountability.
- Cathy O'Neil (January Series speaker 2020) started a [consulting company](https://orcaarisk.com/) on exactly this.
- Perhaps one of you can present on transparency and accountability as a topic.

## Chapter 4

Sorry there's some Week 4 questions that I didn't get to...

### Chapter 4 uses "gradient" in several different ways. What's up with that?

Ignore the Pandas `df.style.background_gradient`; that's a tangent and has nothing to do with the gradient we're interested in.

The other several ways are actually the same: **gradient** always means "how much does the output we got change when this changes?" Note the focus on a specific value, not a general function: we've run the model with a specific set of parameters on a specific input and got a specific loss value; now we ask how much that loss would have changed if we changed one of the parameters *and left everything else the same*.

So if we do:

```python
def f(param, x): return x * param
x = tensor(1.0)
param = tensor(3.0, requires_grad=True)
loss = abs(f(param, x) - 2.0)
loss.backward()
```

Then we'd get a value at `param.grad`, which would be...

- the gradient of the **loss**
- with respect to *that parameter*
- at the current setting of inputs and parameters.

### Are there other ways of representing images besides pixels?

Look up how CT and MRI machines work! They're pretty neat. Ultimately you're going to get pixels (or *voxels*) out, but the in-between can look different. Also check out NeRFs! ([Technical Perspective](https://cacm.acm.org/magazines/2022/1/257453-technical-perspective-neural-radiance-fields-explode-on-the-scene/fulltext), [detailed article](https://cacm.acm.org/magazines/2022/1/257450-nerf/fulltext))

### PyTorch vs NumPy arrays?

They're very similar, especially under the hood. You can make a PyTorch view of a NumPy array and vice versa.

### Why not go even deeper?

Each layer requires more parameters, more computation, and more memory.

It used to be that deeper networks were also much harder to train. But *residual connections* have basically removed that issue now.

### Isn't there something smarter to do than initialize randomly?

A random initialization *at the right scale* can be really helpful. (see chapter 17-- basically, make sure that a forward pass through your network gives you a *reasonable* output, even if it's dead-wrong.)

You can try fancier things to get the network started, but that would come at the expense of just giving the whole network more glances at the data. And data usually wins.

### Might mini-batches mislead us?

Using minibatches instead of the whole dataset can be viewed as a way of adding noise. And in machine learning, noise often *helps*! It often helps the model generalize better. One recent paper even claims that *anticorrelated* noise (i.e., adding noise that tends to be in the opposite direction as the noise added in the previous step) helps generalization even more: [Anticorrelated Noise Injection for Improved Generalization | Abstract](https://arxiv.org/abs/2202.02831)

### What if there are a different number of elements in every row?

This comes up frequently in natural language modeling, where you have sentences or documents of different size. Generally you have to *pad* the inputs to the same length and then find some way of masking out the contribution of the padding you added.

### Why do we need ReLUs or other nonlinearities?

Because otherwise we'd have linear layers back to back. Suppose the first linear layer's weights are the matrix A, and the second linear layer has the weight matrix B, and we're going to feed in an input x. The activations after the first layer would be Ax, and the second layer would be B(Ax).

But matrix multiplication is commutative, so that would be the same as (BA)x. So it's the same as if we'd just had a *single* linear layer with weights given by the matrix product of B and A. So nothing gained by adding a layer.

The *nonlinearity* breaks the linear trick, so we can actually get the benefit of mulitple layers.

### Why use backprop (*automatic differentiation*) when we could just do the calculus?

Symbolic differentiation is reasonable when you have a simple function, but gets messy very quickly when your function gets more complex.

Moreover, automatic differentiation can often take advantage of intermediate results that would otherwise have to get recalculated between the main function call and the gradient computation.

Note that reverse-mode autodiff (like PyTorch uses) isn't necessarily optimal for all problems. For example, it's great when you have one output from lots of inputs, but it would be terrible if you had one input and lots of outputs; in that case *forward-mode autodiff* works much better. In general the optimal approach combines forward accumulation and backward accumulation; figuring out the optimal sequencing is NP-hard in general. So we just backward-mode everything and it generally works well enough.

## For fitting a line, there's a closed-form solution. Why not just use that?

For a single linear layer (which is what linear regression is) there's a closed-form solution (the projection), but once you get to multiple layers there's no closed-form solution.

Note: a random projection is actually a pretty good feature extractor: make a linear layer with random weights (check the signs of the outputs; each feature should have a mix of positive and negative), then add a ReLU, then fit the result with ordinary linear regression. It's a pretty good baseline.

### What are limitations of SGD?

- Getting the learning rate right is hard. Hence there's been a whole bunch of research on *adaptive* optimizers that automatically tune the learning rates. The most popular is probably one called Adam.
- It requires being able to compute the gradient. That might be tricky if, for example, your model is making a discrete choice and only gets information about the results of one action out of many.
- For structured problems (like classic linear regression and its relatives) there are often *much* faster algorithms.

## How much harder is it to code up a CNN?

It's not that much harder. The tricky part is implementing the "convolution" operation, which is just a matrix multiplication but "sliding" over the input. It's not too hard to get an implementation that's working but slow.

## Other questions and clarifications

These questions and issues also came up; I'd be happy to talk about them if anyone desires:

- difference between "bias" in the ethical sense, "bias" in the statistical sense, and "bias" in a linear layer
- "parameters" of a linear layer (all the weights and biases) vs the parameters taken by its constructor (how many weights and biases to use)
- Why did we flatten the image in the simple MNIST classifier?
