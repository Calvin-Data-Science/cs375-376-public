---
title: "Preparation 5"
weight: 1
revised: 2024
---

{{% perusall %}}

- {{% chollet sec="4" %}}

{{% /perusall %}}

## Optional Material

The optional Perusall assignment called "Additional Resources" includes some material that you might find helpful.

## Equivalence of Softmax+Categorical Cross-Entropy and Sigmoid+Binary Cross-Entropy

A two-output softmax layer with categorical cross-entropy loss...

```python
model = layers.Dense(2, activation='softmax')
model.compile(loss='categorical_crossentropy')
```

... is equivalent to a single-output sigmoid layer with binary cross-entropy loss:

```python
model = layers.Dense(1, activation='sigmoid')
model.compile(loss='binary_crossentropy')
```

To see why, notice that for the first model the output is `softmax([dot(x,w1)+b1, dot(x,w2)+b2])`. But since softmax is unchanged when adding/subtracting the same thing from every input, we might as well subtract `dot(x,w2)+b2`, which gives us `softmax([dot(x,(w1-w2))+(b1-b2), 0])`. Since we only needed one dot-product for that, we can use a single output. The rest is just a difference in names:

1. `softmax([q,0])` has another name: `sigmoid(q)`.
2. Binary cross-entropy loss `bce(p)` is just a convenient way to write categorical-cross-entropy `cce([p, 1-p])`. (This explains the confusing formula you'll see for binary cross-entropy loss which has `1-y` and `1-p` in it.)

Aside: regularization and optimizer issues may mean that these models are not *exactly* equivalent in practice, but the differences will probably be small.
