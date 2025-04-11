---
title: "Exercise 376.1: LM Evaluation"
weight: 4
revised: 2025
---

## Outcomes

- Conduct a quantitative experiment comparing openly available language models

We're going to do the same task as Discussion 1, but in code.

**Start by picking one specific example from your Discussion 1 task**. We'll hard-code it for simplicity.

## Part 1: LLM APIs

Write code that runs the "FlipFlop" experiment for your one example by calling an LLM API. Run the experiment 5 times (in a loop) and report the average initial accuracy and average accuracy after the "are you sure?".

Notes:

- Make sure to handle the conversation context correctly.
- Instruct the model to provide its final answer as a single word, e.g., "You may think as much as necessary, but end your response with either 'Answer: yes' or 'Answer: no'".

## Part 2: Local Models (optional)

Repeat the same experiment but running the model within your own notebook. Follow instructions on [Hugging Face Chat Basics](https://huggingface.co/docs/transformers/conversations).

You might choose models like:

- https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct
- [One of the SmolLM2 models](https://huggingface.co/collections/HuggingFaceTB/smollm2-6723884218bcda64b34d7db9)
- https://www.kaggle.com/models/google/gemma-3
- https://www.kaggle.com/models/metaresearch/llama-3.2


## Submit

Write a Jupyter notebook with your code and experiment results.
