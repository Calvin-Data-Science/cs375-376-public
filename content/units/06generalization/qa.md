---
title: "Week 6 Q&A"
date: 2022-02-16
---

## Chapter 3

Some stragglers:

### Why are darker faces harder for CV to recognize?

- Mostly: lack of training data. Most datasets of faces were heavily biased towards light-colored skin.
- Also: Early film was designed to reproduce light-colored skin well; wasn't really tested on dark-colored skin.

### Is it too late to fix the ethical issues in technology?

1. Yes, in one sense: the Fall already happened, and that's the ultimate cause of these problems. Humans are broken, and the systems we make will always be broken.
2. No, in an important sense: **you**.

### Is every ethical problem in AI about race and gender?

Critical Theory has monopolized ethical discussions in many areas of society lately, so many ethics researchers tend to highlight aspects of their work that relate to power differentials across race and gender. But other aspects are also important; just a few examples include the relationship of AI moderation to freedom of speech, the environmental impact of AI, the existential risks that we may be taking in developing more powerful AI technology, and systems that optimize themselves to hold our attention.

## Chapter 5

### Why am I saying to skim or skip certain topics?

There are some things in our book that the fastai people make a much bigger deal about than most researchers and practitioners. It's a lot of reading and stuff to understand, so I'm trying to help you focus on the parts that are going to pay most dividends down the line.

### Do the concepts of loss functions and optimization apply to other ML models besides image classifiers?

Yes!

- language (NLP): basically the same loss functions (typically cross-entropy on picking the next word), similar optimization approach.
- regression: see chapter 6; just use MSE or MAE instead of cross-entropy.
- generative models: sometimes use contrastive losses, which are just classification losses where the model has to distinguish true from generated data.

### How transferrable models are between physical machines?

Generally very much so. They're trained with lots of noise added intentionally, so little differences in floating point behavior don't tend to matter much.

### Guidelines for how cleaning relates to modeling?

- Garbage in, garbage out.
- Focus time making sure the labels are what you want, rather than including and excluding specific examples. You'll get lots of weird examples in the wild, so the weirder your training set examples are the better (though perhaps include an "ignore" category, so your system learns when to not even try to make a decision)

### How do people actually choose learning rates?

- First pass: just use Adam with the default parameters, it often works well enough.
  - I've never seen the "LR Finder" used outside of FastAI.
- General wisdom is that if you have time to tune it, SGD with the right learning rate schedule will give best results.

### Why relu and not absolute value?

The abs function should work as a nonlinearity, but my intuition is it would be harder to learn (because the effect of increasing an activation *flips* when you're on the other side of 0).

### How do we actually fix clf errors?

- Don't worry about individual errors; make sure you're focusing on systematic issues.
- Make sure your training is converging and your model has actually fit your training data well. Beyond that, trace it back to the training data. Get more examples like the ones that fail. Augment more so your existing examples look more like the failing examples. etc.

### Where does the score come from that gets fed into softmax?

A linear layer.

### Why does cross-entropy need negative-log?

The [Wikipedia article](https://en.wikipedia.org/wiki/Cross_entropy) is actually pretty good here.

### Do all the images really have to be the same size?

They used to have to be, but modern networks can work with any size. It's still more efficient to run a batch of images at the same size through at the same time though.

### Why ReLU?

Piecewise linear approximation.

### I'm still fuzzy about SGD.

See the Glossary.
