---
title: "Lab 376.2: Logits in Causal Language Models"
weight: 2
revised: 2026
---

Objectives addressed:

- [OG-LLM-Tokenization](objective): the tokenization process in language models, including how text is converted into tokens
- [TM-LLM-Generation](objective): the architecture and data flow of a causal language model, including how it generates outputs one token at a time based on previous tokens
- [OG-SelfSupervised](objective): the optimization game of minimizing surprise (cross-entropy loss) on next-token prediction

Work through this notebook today to learn about what the outputs of a language model look like. You'll see how it's a token-by-token classification model.

The main objective is for us to understand the output of a language model. We'll see that the output is a probability distribution over the vocabulary for each token in the sequence.

We'll also consider what optimization game this model is playing: minimizing the average surprise (negative log-probability) of next tokens in its training data. This is a form of self-supervised learning, where the model learns to predict parts of the input from other parts.

{{% notebook name="Logits in Causal Language Models" nbname="u09n1-lm-logits.ipynb" %}}
