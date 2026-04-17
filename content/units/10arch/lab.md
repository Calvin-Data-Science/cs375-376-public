---
title: "Lab 376.3: Implementing Self-Attention"
revised: 2026
---

In this lab, you'll trace through parts of the implementation of a Transformer language model, focusing on the self-attention mechanism. We'll compare the performance of a Transformer model with a baseline that only uses a feedforward network (MLP).

This lab addresses the following course objectives:

- [TM-LLM-Embeddings](objective)
- [TM-SelfAttention](objective)
- [TM-TransformerDataFlow](objective)
- [TM-LLM-Generation](objective)
- [OG-SelfSupervised](objective)


## Task

Start with this notebook:

{{% notebook name="Implementing self-attention" nbname="u10n1-implement-transformer.ipynb" %}}

You may find it helpful to refer to [The Illustrated GPT-2 (Visualizing Transformer Language Models) – Jay Alammar – Visualizing machine learning one concept at a time.](https://jalammar.github.io/illustrated-gpt2/)


Extension idea

- measure how much this network speeds up when you move it to a GPU (you may need to `torch.compile` it first)
- Other extensions are described on the [Architectural Experimentation](../extension/) page.
