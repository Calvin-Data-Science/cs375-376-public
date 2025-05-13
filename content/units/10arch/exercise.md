---
title: "Exercise 376.2: Perplexity"
revised: 2025
---

## Overview

In this assignment, you will evaluate language models by computing perplexity - a key metric that reveals how well models predict text. You'll analyze how performance scales with model size, connecting to fundamental concepts in language model evaluation.

## Learning Objectives

This assignment addresses the following course objectives:

- [MS-LLM-Generation](objective)
- [MS-LLM-Eval](objective)
- [NC-Scaling](objective)
- [MS-LLM-API](objective)

Students may also use this exercise to demonstrate additional objectives, such as:

- [MS-LLM-Tokenization](objective)
- [MS-Eval-Experiment](objective)
- [MS-Eval-Visualize](objective)

## Task

Your goal is to evaluate how language model performance (measured by perplexity) changes with model size:

1. Select **two or more language models from the SmolLM2 family** (e.g., 135M, 360M, 1.7B parameters)
2. Evaluate these models on **ROCStories dataset** of short stories by computing **perplexity** for each model on the same set of stories
3. Create a **plot showing how perplexity changes with model size**
4. Analyze which stories or which parts of stories are most challenging for the models

### Model Options

Use models from the [SmolLM2 family](https://huggingface.co/collections/HuggingFaceTB/smollm2-6723884218bcda64b34d7db9), which are available on the Hugging Face model hub:

- [`HuggingFaceTB/SmolLM2-135M`](https://huggingface.co/HuggingFaceTB/SmolLM2-135M) (135 million parameters)
- [`HuggingFaceTB/SmolLM2-360M`](https://huggingface.co/HuggingFaceTB/SmolLM2-360M) (360 million parameters)
- [`HuggingFaceTB/SmolLM2-1.7B`](https://huggingface.co/HuggingFaceTB/SmolLM2-1.7B) (1.7 billion parameters, if your system can handle it)

### Dataset

Use the [ROCStories dataset](https://cs.rochester.edu/nlp/rocstories/), which contains short five-sentence stories. You can load an unofficial mirror from the Hugging Face hub using the `datasets` library:

```python
from datasets import load_dataset
dataset = load_dataset("roneneldan/TinyStories", split="train[:5000]")
# Take a sample of stories for evaluation
stories = rocstories["train"].select(range(50))
```

## Computing Perplexity: Strategy

Here's the recommended approach for computing perplexity:

1. Create a function with this signature (you may want to return additional values for token-level analysis, but start with this):
   ```python
   def compute_perplexity(model, tokenizer, text):
       """
       Compute the perplexity of a model on a given text.
       
       Args:
           model: A language model that returns logits
           tokenizer: The tokenizer associated with the model
           text: The text to evaluate
           
       Returns:
           float: The perplexity of the model on the text
       """
       # Your implementation here
   ```

2. Key implementation steps:
   - Tokenize the full text
   - Get model predictions (logits)
   - For each token position (except the first), compute the negative log probability of the actual next token
   - Average these values and compute perplexity as exp(mean_loss)

3. **Note**: Refer to Lab 2 for examples of how to extract and work with logits from language models.

4. **Caution about indexing**: Pay careful attention to token positions! Remember that when predicting the token at position `i`, you use the logits from position `i-1`. This off-by-one error is easy to make.

5. For data collection, consider creating a structure like:
   ```python
   results = []
   
   # For each model and story
   for model_name in model_names:
       for story_idx, story in enumerate(stories):
           # Compute perplexity
           perplexity = compute_perplexity(model, tokenizer, story["text"])
           
           # Store results
           results.append({
               "model_name": model_name,
               "story_idx": story_idx,
               "perplexity": perplexity
           })
   
   # Convert to DataFrame for easier analysis
   import pandas as pd
   results_df = pd.DataFrame(results)
   ```

## Analysis and Submission

Create a Jupyter notebook that includes:

1. Implementation of the perplexity calculation
2. A table showing perplexity for each model on each story
3. A plot showing how perplexity changes with model size
4. Analysis of results:
   - Which models performed best?
   - Is there a consistent relationship between model size and perplexity?
   - Which stories had the highest/lowest perplexity across models?
   - Optional: Identify specific tokens or sentence positions that were most challenging for the models

## Grading Rubric

| Criterion | Level P (Progressing) | Level M (Met) | Level E (Excellent) |
|-----------|------------------------|---------------|---------------------|
| Implementation | Correctly implements perplexity calculation for at least one model | Correctly implements perplexity for all models and shows proper scaling analysis | Implements additional analyses (e.g., token-level perplexity, visualizations of challenging tokens) |
| Analysis | Presents basic comparison between models | Provides substantive analysis of the relationship between model size and performance | Connects findings to broader concepts in LLM scaling laws and performance patterns |
| Visualization | Creates basic table of results | Creates clear plot showing relationship between model size and perplexity | Creates multiple informative visualizations that effectively communicate patterns in the data |

## Extension (for E-level work)

- Compare perplexity when computing it with different prompt lengths (e.g., using first 1, 2, or 3 sentences as context)
- Analyze perplexity on different categories of text (e.g., stories vs. news vs. code)
- Implement a token-level analysis that highlights exactly where models struggle most