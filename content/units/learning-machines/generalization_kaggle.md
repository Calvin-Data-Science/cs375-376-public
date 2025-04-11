---
title: "Generalization and a Kaggle Competition"
weight: 4
revised: 2025
---

## Outcomes

The process of completing this assignment will improve your ability to:

- Explain the importance of evaluating image classifiers on unseen data.
- Describe characteristics of a dataset that are relevant to downstream performance.
- Use data augmentation to improve model generalization.
- Describe how the concept of *distributions* applies to image data.

Along the way, we'll participate in a Kaggle competition, so you'll get to practice with that.

## Task

Load up the classifier you trained in Homework 1. **Use it to make predictions on a set of images collected by others** in the class. You'll do this by participating in a Kaggle competition.

Click the link provided in Moodle to join the Kaggle competition. Create a Kaggle notebook in the Code tab of the competition, and load the following starter notebook:

{{% notebook name="Letter Classification Starter Notebook" nbname="letter-classification-starter-notebook-25sp.ipynb" %}}

Note that the starter notebook includes only the code; it is not a template for your report. You'll need to add descriptions as explained under Submission below.

1. Bring up your Homework 1 notebook. Copy and paste your model-training code from the Homework 1 notebook into the Homework 3 notebook in the section indicated. (You might need to add your dataset as an input.) **Note that although the competition has a "training" set, you should (mostly) use your Homework 1 model, including its dataset.
2. Run the notebook, fixing any path errors. The code will attempt to make use your model to make predictions on the "test" images. Once it completes successfully, **Submit your predictions to the competition**. Name your submission "Homework 1 baseline" or the like. Write down in your analysis how well your baseline does on the leaderboard.
    - Make sure that the weights were actually loaded; if you see a warning about random weights, make sure you're saving the weights to `WEIGHTS_FILENAME`.
3. The Kaggle competition includes a "training" dataset, *which we'll actually use as a **validation set***. Use this dataset (loaded into the notebook as `valid_dataset`) to evaluate your top losses and confusion matrix, like you did in Lab 5. **Report the most frequent mistakes** your classifier makes. **Quantify the mistakes** (using the confusion matrix) and make an educated guess as to *why* these might be the most common mistakes (by, for example, studying the top losses).
4. Make some changes to the training process you used in Homework 1. For example, you might want to add data augmentation or change the foundation model. Experiment as much as you want, but **make two more submissions** to evaluate on the test set and see what effect your changes had on the leaderboard. Be thoughtful about your changes and **explain them in your analysis**.
5. Optionally, try to improve your model's performance further to try to get a higher score on the leaderboard. You may, for example, train on the training set given in the competition.

## Analysis and Submission

Submit your Homework 3 notebook to Moodle. You don't need to submit a revised Homework 1 notebook, but make sure that your Homework 3 notebook includes details of what you changed in that notebook.

Your notebook should include:

- An introduction that summarizes what you did and what you found.
- A clear explanation of the source and nature of the data you used for training your initial (homework 1) classifier.
  - Include any relevant information you reported in the README in Homework 1.
  - Also, read the introduction to Microsoft's [Dataset Documentation (Datasheets for Datasets) template](https://www.microsoft.com/en-us/research/uploads/prod/2022/07/aether-datadoc-082522.pdf). Then, skim through the questions that follow. **Choose two or three questions** that are most relevant to *how well the model that you trained on that data worked on new data*. Include both the **question texts** and your answers. Good answers are those that would most help someone who is training on your dataset predict how it will work on new data.
- An organized summary of your results for the baseline model and the two modified models.
  - Recall that in Homework 1 you estimated the accuracy that your classifier would obtain on other people's images. **Compare the accuracy you observed from the baseline model to the accuracy that you thought you'd get.**
  - Discuss what you noticed from analyzing the mistakes of your baseline model.
  - Discuss what changes you tried in order to improve performance, and most importantly, *why you tried them*.
  - Discuss what you learned from the changes you tried.
- A clear conclusion that summarizes what you found and interprets what the results mean.


## Details


Possible things to adjust:

- How big your Homework 1 classifier's validation set is
- Which foundation model to use (see hw1 for a list of options)
- What data augmentation (if any) to apply
- How many epochs to train
- What learning rate to use

Think about what other sources of variation might come up, and how you might be systematic about them.

## Augmentation

We didn't do code for image augmentation in the lab, but it's actually pretty simple. In your Homework 1 notebook, after you've created your `train_dataset`, create an augmentation pipeline. Refer to Chapter 8 of the book, or look at the [Data Augmentation section](https://keras.io/guides/keras_cv/classification_with_keras_cv/#data-augmentation) of the Keras CV guide.

Then, assuming you called your augmentation pipeline `augment`, you can apply it to your `train_dataset` like this:

```python
train_dataset_with_aug = train_dataset.map(
  lambda inputs, labels: (augment(inputs), labels),
  num_parallel_calls=tf.data.AUTOTUNE)
```

> It turns out that this does actually apply different augmentations on each epoch.

I suggest looking at example batches from `train_dataset_with_aug` to make sure the augmentation is working as you expect.

When you fit the model, use `train_dataset_with_aug` instead of `train_dataset`.

## Errata

None yet this year.
