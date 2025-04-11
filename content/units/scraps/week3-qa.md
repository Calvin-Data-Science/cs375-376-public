---
title: "Week 3 Q&A"
date: "2022-01-27"
---

## Q&A

### What aspects of the reading should we focus on?

Use the prep instructions, prep quizzes, and learning objectives as a guide. (Unfortunately, when faced with a potential digression, the book tends to always take it.)

Important concepts will come back again in lab, homework, and future readings, so don't fret over missing something.

### Why did we learn the dot product in Lab 1?

Because it's a core building block to neural net modeling. You'll see in Lab 4 and beyond how we build on it!

### How much math needed?

Depends!

- For training models out-of-the-box, almost no math at all, just like you don't need to know about how hash tables work to write SQL queries against databases.
- For pushing the envelope of machine learning, we need all the creativity we can get, coming from any corner of math, physics, CS, statistics, etc. For example, one very promising new kind of neural network, [S4](https://srush.github.io/annotated-s4/), uses state-space models from physics and signal processing.
- Most of our work will be somewhere between these two extremes.

### What's a test set?

In the hierarchy of data purity:

- Training set: our playground. Mess with it all you want.
- Validation set: strength tests. Use occasionally to check that you're getting stronger. But not too much or you'll start learning how to game it! (20% is a reasonable size but a wide range is reasonable.)
- Test set: don't touch this. Until you're basically done.

### How much augmentation?

See chapter 5. You can get pretty outlandish.

### Are there laws that safeguard our information?

Yes, see the EU's [GDPR](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation) and subsequent legislation like California's [CCPA](https://en.wikipedia.org/wiki/California_Consumer_Privacy_Act).

### What's gradient boosting?

The book mentions gradient-boosted trees in Chapter 2 as an alternative approach to tabular data. File it away as an alternative approach (along with software names: XGBoost and LightGBM) but we won't be discussing it in this class.

### Do we really need labels?

**No**: a big area of growth now is in *self-supervised* learning, where the model learns overall patterns in the data independent of labels, then only needs a small amount of labeled data (or none at all, in some cases) to make conclusions. For example, consider learning to predict what text ends up near an image on a website... or blanking out part of an image and learning to fill it in.

### Predictions vs Recommended Actions

Imagine Amazon's if-you-liked-this product recommender. It's probably seeded by trying to predict what product people actually bought. But you can only buy things that you're already aware of. So they probably tweaked it to recommend products that they think people will be interested in and *wouldn't* already know about.

### Why does fast.ai `import *`?

I wish they didn't.

### Any real-life examples of overfitting?

See an example in slides. Also, have a look at "adversarial examples".

### Could we still "overfit" if we had infinite data?

Yes, if the data were from a different *distribution*. For example, if you trained on an infinite set of black cats and white dogs, your model would struggle with white cats or black dogs.
