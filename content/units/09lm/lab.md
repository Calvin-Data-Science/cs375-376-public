---
title: "Lab 376.2: Logits in Causal Language Models"
weight: 2
revised: 2025
---

Objectives addressed:

- [MS-LLM-Tokenization](objective)
- [MS-LLM-API](objective)
- [OG-SelfSupervised](objective)

Work through this notebook today to learn about what the outputs of a language model look like. You'll see how it's a token-by-token classification model.

The main objective is for us to understand the output of a language model. We'll see that the output is a probability distribution over the vocabulary for each token in the sequence.

{{% notebook name="Logits in Causal Language Models" nbname="u09n1-lm-logits.ipynb" %}}
