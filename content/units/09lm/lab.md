---
title: "Lab 376.2: Logits in Causal Language Models"
weight: 2
revised: 2026
---

Objectives addressed:

- [MS-LLM-Tokenization](objective)
- [MS-LLM-API](objective)
- [OG-SelfSupervised](objective)

Work through this notebook today to learn about what the outputs of a language model look like. You'll see how it's a token-by-token classification model.

The main objective is for us to understand the output of a language model. We'll see that the output is a probability distribution over the vocabulary for each token in the sequence.

We'll also consider what optimization game this model is playing: minimizing the average surprise (negative log-probability) of next tokens in its training data. This is a form of self-supervised learning, where the model learns to predict parts of the input from other parts.

{{% notebook name="Logits in Causal Language Models" nbname="u09n1-lm-logits.ipynb" %}}
