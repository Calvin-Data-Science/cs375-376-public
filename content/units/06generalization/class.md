---
title: "From Class Week 6"
weight: 2
revised: 2024
---

## Monday Class

- [Slides](../../../slides/w06-generalization.html)
- Showed an example of an embedding space from a version of the Lab 5 notebook where I added some code; see the output immediately above the "Softmax and Cross-Entropy" section of [this notebook](https://cs.calvin.edu/courses/cs/375/25sp/fundamentals/u05n02-probe-clf-projected-features.html). The x's are the prototypes; the dots are the image feature vectors.
  - Thinking through it more now: I could have used a [linear discriminant analysis (LDA)](https://scikit-learn.org/stable/modules/lda_qda.html#lda-qda) to project the features down to 2D in a way that best preserved the class separation. The factor analysis was unaware of the task so it made a projection where many classes overlapped.


## Wednesday Class

- Continue [Monday slides](../../../slides/w06-generalization.html).
  - From review question 3, we distinguished "metric" from "loss function".
- In section B, we demonstrated bias vs variance with this example: {{% notebook name="Bias-Variance Decomposition" nbname="u06s01-bias-variance.ipynb" %}}

## Friday Lab

[Lab 6: The Remix](lab/)

<!--

Next year: the diagram of overconfidence kinda worked, but:

- more visuals would have helped
- I'm getting a lot of mileage out of 1D function approximation, but it might also be too limiting. Perhaps working with dot products from the start would be a better intuitive framework? Rotate (Linear), then selectively squish (ReLU)?

-->