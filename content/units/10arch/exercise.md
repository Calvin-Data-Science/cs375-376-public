---
title: "Exercise 376.2: Perplexity"
revised: 2026
---

## Overview

In the [u09 logits notebook](/notebooks/u09n1-lm-logits.html), you implemented perplexity for a single model on short texts. In this assignment, you will extend that work to compare multiple language models of different sizes, analyzing how performance scales with model size.

## Learning Objectives

This assignment addresses the following course objectives:

- [TM-LLM-Generation](objective)
- [OG-LLM-Eval](objective)
- [TM-Scaling](objective)
- [OG-Eval-Experiment](objective)

Students may also use this exercise to demonstrate additional objectives, such as:

- [TM-LLM-Compute](objective)
- [OG-LLM-Tokenization](objective)

## Task

Your goal is to evaluate how language model performance (measured by perplexity) changes with model size:

1. Select **two or more language models from the Qwen2.5 family** (e.g., 0.5B, 1.5B, 3B parameters)
2. Evaluate these models on a set of short stories by computing **perplexity** for each model on the same stories
3. Create a **plot showing how perplexity changes with model size**
4. Analyze which stories or which parts of stories are most challenging for the models

### Model Options

Use models from the [Qwen2.5 family](https://huggingface.co/collections/Qwen/qwen25-66e81a666513e518adb90d9e), which are available on the Hugging Face model hub:

- [`Qwen/Qwen2.5-0.5B`](https://huggingface.co/Qwen/Qwen2.5-0.5B) (0.5 billion parameters)
- [`Qwen/Qwen2.5-1.5B`](https://huggingface.co/Qwen/Qwen2.5-1.5B) (1.5 billion parameters)
- [`Qwen/Qwen2.5-3B`](https://huggingface.co/Qwen/Qwen2.5-3B) (3 billion parameters, if your system can handle it)

All Qwen2.5 sizes share the same tokenizer, which makes perplexity comparison across sizes fair.

**Memory tip:** Load models with `torch_dtype=torch.float16` (or `torch.bfloat16`) to reduce memory usage:

```python
from transformers import AutoModelForCausalLM, AutoTokenizer

model_name = "Qwen/Qwen2.5-0.5B"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(model_name, torch_dtype=torch.float16)
```

### Dataset

Use the [TinyStories dataset](https://huggingface.co/datasets/roneneldan/TinyStories), which contains short stories. You can load it from the Hugging Face hub using the `datasets` library:

```python
from datasets import load_dataset
dataset = load_dataset("roneneldan/TinyStories", split="train[:100]")
# Take a sample of stories for evaluation
stories = dataset.select(range(50))
```

## Computing Perplexity

Adapt your work from the [u09 logits notebook](/notebooks/u09n1-lm-logits.html), where you began implementing perplexity. **I still recommend computing the loss manually** (extracting logits, indexing the correct token probabilities, averaging) rather than using shortcut approaches like passing `labels` to the model. The main addition here is running it across multiple models and stories.

Here's a suggested function signature (you may want to return additional values for token-level analysis, or take additional arguments for context to prepend):

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

**Caution about indexing**: Pay careful attention to token positions! Remember that when predicting the token at position `i`, you use the logits from position `i-1`. This off-by-one error is easy to make.

For data collection, consider creating a structure like:

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
   - Which stories had the highest/lowest perplexity across models? (look at their full text, don't make assumptions)
   - Optional: Identify specific tokens or sentence positions that were most challenging for the models

## Grading Rubric

| Objective | Level P (Progressing) | Level M (Met) | Level E (Excellent) |
|-----------|----------------------|---------------|---------------------|
| **TM-LLM-Generation** (extracting logits) | Loads at least one model and extracts logits to compute perplexity | Correctly computes perplexity for all chosen models | Performs token-level analysis showing which specific tokens contribute most to perplexity |
| **OG-LLM-Eval** (evaluation strategy) | Computes perplexity for at least one model on the dataset | Compares perplexity across multiple models; identifies which model performs best | Critically analyzes what perplexity captures and misses as an evaluation metric |
| **TM-Scaling** (size vs. performance) | Reports perplexity values for different model sizes | Creates a clear plot of perplexity vs. model size and describes the trend | Connects findings to scaling laws; analyzes whether improvement is linear, logarithmic, etc.; discusses diminishing returns |
| **OG-Eval-Experiment** (experimental design) | Runs the comparison on a small sample | Uses a sufficient sample of stories and reports results systematically | Controls for confounds (e.g., story length, genre); reports variance or confidence intervals |

## Extension (for E-level work)

Implement *context*: instead of just computing perplexity on the full story, only compute it on part of the story while providing the previous sentences as context.

- Compare perplexity when computing it with different prompt lengths (e.g., using first 1, 2, or 3 sentences as context).
- Prepend an "instruction", like "Write a story about ___", to see how it affects perplexity. 
    - Does this vary between base models vs instruction-tuned variants (e.g., `Qwen2.5-0.5B` vs `Qwen2.5-0.5B-Instruct`)? For the Instruct models, you may want to use the [chat template](https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct?chat_template=default) to format the input as a conversation.
    - Try a few different variants of the instruction. Does more specific instructions (e.g., "Write a story about a dragon and a princess") lead to lower perplexity than vague instructions ("Write a story")--and can you disentangle *specificity* from *keyword overlap* (e.g., asking for a story about a "dragon" vs about a "mythical flying creature")?
- Analyze perplexity on different categories of text (e.g., stories vs. news vs. code)
- Implement a token-level analysis that highlights exactly where models struggle most. Can you identify any patterns?

