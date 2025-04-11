---
title: "Scraps Week 3"
---

- {{% notebook name="Classification in scikit-learn" nbname="u03n1-sklearn-classification.ipynb" %}}

<!--

- great!
- (Revise) oops: *accuracy* is good if it's *high*, so logistic regression is *worst*.
- This affects your answer to Q4 also.
- remember that the log loss (cross-entropy) considers not just the classifier's decision but the *confidence* of that decision. The decision tree was **confidently wrong** so it got high log loss.
- The decision tree was the classifier that *overfit*. It does really well on the training set but overly relied on happenstance features of that training set.
- The logistic regression *underfit*: it was not able to capture meaningful patterns even in the training set.
- While the high cross-entropy is a symptom of overfitting, that was not sufficient by itself to determine if underfitting or overfitting occurred. For that, we need to compare the training set and test set performance (the optional extension).

## Overall

- Restart and Run All before submitting. Your notebooks include outputs that don't correspond to the code.
- 

-->

## From last year

- [Feedback](../feedback/) and [Q&A](../qa/), especially on Homework 2
- Continuing intro to AI Tech Questions: [slides](/slides/w3/w3-data-and-ethics.html)
- How to evaluate a classifier? Accuracy and confusion matrices
- *time permitting* loss functions and the importance of partial credit

Examples:

- If the classifier was actually just looking at the first letter of the image filename, it could get 100% accuracy but it wouldn't actually be learning to recognize images.
