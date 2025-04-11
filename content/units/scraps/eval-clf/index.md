---
title: 'Lab 3: Evaluating classifiers'
summary: 'Try out some variations on a classification model.'
draft: true
---


## Objectives

- Run experiments to determine the effects of hyperparameters on classifier performance

## TODO

- make it mandatory to do at least 2 trials and report a range of accuracy values

## Getting Started

Get the [template](lab02.ipynb). Save it in your `cs344` folder.

## Instructions

We're going to start with the cat-vs-dog classifier that we built in chapter 1 and try changing a few things.

### Classifier 1

Here is an example of a task that a research advisor might give you:

> Train a classifier to distinguish between images of cats and dogs.
> 
> - Use the [Oxford-IIIT Pet Dataset](http://www.robots.ox.ac.uk/~vgg/data/pets/).
> - Fine-tune a 34-layer ResNet model for 1 epoch
> - Report the error rate on a held-out validation set of 20% of the data.

The first code block from chapter 1 (or lab 1) accomplishes this task. It has been included in your lab template with a few blanks; fill them in. (You may reference Lab 1.)

> Note: If you experience an "out of memory error":
> 
> 1. Check that you don't have another notebook already running (if you're not sure, log off and log back in).
> 2. "Restart and Run All" on the Kernel menu.
> 3. If this still doesn't work, add `bs=8` as a keyword parameter to `ImageDataLoaders.from_name_func`. 

{{% task %}}
Make a list with one element: the last `error_rate` reported during classifier training: `clf_1_error_rates = [0.005413]`.

(Just hard-code the number. Also: you'll see two tables; look at the second table.)
{{% /task %}}

### Classifier 2

One aspect that affects how a model performs is how many *layers* of processing it was trained to do. Generally, a *deeper* model (more layers) can be more accurate, but requires more computational time, and often requires more training to reach that level of accuracy. Let's try a classifier using a different number of layers:

{{% task %}}
Repeat the previous task, but use an 18-layer ResNet architecture instead (`resnet18`). Record the result in `clf_2_error_rates`. How does the error rate compare?
{{% /task %}}

### Comparisons

*Optional, come back to this when you're done with the rest of the lab.*

One of our goals in this class is to get in the habit of treating numbers critically, especially understanding the variability behind them.

So, instead of just comparing the single accuracy (error rate) numbers we get from both classifiers, let's compare the *range* of results we'd get from repeating the experiment several times.

A random *seed* makes a sequence of random numbers (or decisions) identical, which really helps for reproducibility. So to run our experiment several times, all we need to do is change the seed before each run.

{{% task %}}
Repeat the two classifier training runs we did above, changing the seed we pass to `set_seed` (*not* the `seed` passed to `ImageDataLoaders`; we'll discuss why later). Put the accuracy numbers in the `error_rates` lists we constructed. Aim for at least 3 numbers in each list.

Now, compare the two lists. Which classifier performs better? Do you think the difference you observe between the two classifiers could have arisen simply by chance? Why or why not?
{{% /task %}}

We just changed the *architecture*, but not anything else. We could also change:

- The *data*: give it different images (or more or fewer of the same images)
- The *task*: have it try to predict something different
- The *hyperparameters*: train it a different way, e.g., let it train longer (more epochs) or adjust itself faster (higher learning rate)
