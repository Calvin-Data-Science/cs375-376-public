---
title: "Softmax"
weight: 4
revised: 2026
---

## Background

- Analogy: softmax takes skill scores and turns them into probabilities of winning.
- Example:
    - equal skill scores -> 50-50 chance of winning.
    - one player has much higher skill score -> much higher chance of winning.
- Plain-English: (1) make sure scores aren't negative, (2) make sure they add up to 1.
- Technical definition:
    - `softmax` input: a vector `x` of shape `(n,)` 
    - `softmax` output: a vector `y` of shape `(n,)` where `y[i]` is the probability that `x` is in class `i`.
    - `y[i] = exp(x[i]) / sum(exp(x))`

Jargon:

- **Logits** or **scores**: the inputs to the softmax function.
- **probabilities** or **probs**: the outputs of the softmax function.
- **logprobs**: the log of the probabilities.


## Warm-Up Activity

Open the [softmax and cross-entropy interactive demo](https://observablehq.com/@kcarnold/softmax) that Prof Arnold created.

Try adjusting the logits (the inputs to softmax) and get a sense for how the outputs change. Describe the outputs when:

1. All of the inputs are the same value. (Does it matter what the value is?)
2. One input is much bigger than the others.
3. One input is much smaller than the others.

Finally, describe the input that gives the largest possible value for output 1.

## Notebooks

{{% notebook name="Softmax, part 1" nbname="u04n2-softmax.ipynb" %}}
