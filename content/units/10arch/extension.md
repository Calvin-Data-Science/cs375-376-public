---
title: "Optional Extension: Architectural Experimentation"
revised: 2025
---

## Outcomes

- Experiment with architectural choices for a causal language model.
- Compare the performance of different models on a specific task.

You can use this exercise to demonstrate the following course objectives:

- [TM-LLM-Compute](objective)
- [OG-LLM-ContextAndTools](objective)
- [OG-Eval-Experiment](objective)
- [OG-LLM-Tokenization](objective)

## Task

Run and report on a controlled experiment where you change one thing about a Transformer-based language model and plot the results. Your report should have at least 2 plots, one for each of the two y axes you choose (see below). You may have more than 2 plots if you pick two x axes, which you'll need to do if you pick change a parameter already implemented in Lab 3.

I suggest starting with the simple Transformer implementation in Lab 3. Train the model for a bit longer than we did in the lab, though, since that the model clearly hadn't converged. (Also, rather than going through the existing training set multiple times, you should probably just use a bigger training set. You can use the same TinyStories dataset, but just use more of it.) You can also use a different dataset if you prefer.

### x axes: things to change

Here are some suggested possible x axes (things to change) - pick one or two:

- Things that are already implemented in Lab 3 (if you pick from these, pick two or more to change):
  - Number of attention heads (1, 2, 4, 8, ...)
  - Embedding dimension
  - MLP hidden dimension
  - Context length
  - Number of training tokens
- Things that would require a bit of straightforward implementation
  - Tokenizer (character-level vs gpt2 tokenizer vs ...?)
  - Dataset (TinyStories vs Shakespeare vs Wikipedia text vs ...)
  - Activation function (ReLU vs GELU vs ...)
  - Multiple layers (possibly sharing weights between layers?)
  - Use a different activation function on the *attention weights* (e.g., sigmoid instead of softmax)
  - Use a different optimizer (e.g., AdamW) and/or add a learning rate schedule
  - Dropout (see comments for where to add it) (*note: modern Transformers instead seem to just train on more data*)
- Things that would require more implementation work but would pay off (you may need to ask for help for these)
  - Multi-query attention (use one set of keys and values, but each attention head provides a different query)
  - Switch to rotary position embeddings ([RoPE](https://blog.eleuther.ai/rotary-embeddings/))
  - Speed up the training using something like Flash Attention
  - Speed up generation by caching past keys and values
  - Residualize the computations of keys / queries / values (use the same head dim as embedding dimension, and compute each value as `x + self.value(x)` for some learned `self.value` function etc.)
  - Hard-code one head to always attend to the previous token (or the first token)
  - Smear attention weights forward by an amount that's learnable by attention head (i.e., if token i attended to token j, then token i+1 should attend to token j+1)
  - Apply causal mask only to part of the attention weights (e.g., allow the "prompt" tokens to all attend to each other)
  - Try any of the variations discussed in [this tutorial](https://www.borealisai.com/research-blogs/tutorial-17-transformers-iii-training/), e.g., ways of removing layer normalization


### y axes: things to measure

Here are some suggested y axes (things to measure). Everyone should do the first one, and then also pick one other:

- Loss / perplexity on unseen data. **Everyone should do this**. (The Lab 3 code implements this for the training data; you'll need to implement it for unseen data; you can use the validation dataset.) <!-- Next year: there is a TinyStories test set too; should they use that? -->
  - Use the loss/perplexity that your model reaches at the *end of training*, i.e., after the last epoch has complete.
  - To evaluate faster, you should turn off gradient computation during evaluation by wrapping the evaluation code in a `with torch.no_grad():` block.
  - If you're comparing tokenization strategy, the loss will be in different units for each model, so report mean loss *per character* instead of per token.
- Speed (tokens per second) - training and/or generation
- Average length of words or sentences generated
- How many misspelled words are generated
- What Gemma's perplexity is on the generated text
- Some other metric of your choice

Run multiple trials if you can. Your plots should have at least 3 data points, ideally more.

## Analysis and Submission

Write a Jupyter notebook that includes:

- An introduction that summarizes what you did and what you found.
- A clear explanation of experiment you ran.
- The plots you generated.
  - Make sure that you have at least two plots (one for each of the two y axes you chose), perhaps 4 (if you have two x axes and two y axes). Make these as separate plots, in separate code chunks, unless you are comfortable with subplots.
  - Make sure that the axes are clearly labeled
- A clear interpretation of the results.
- A conclusion that summarizes what you found and interprets what the results mean.

Include all code needed to reproduce your results. Your notebook need not re-run all of the experiments; use saved results to make the plot. Example:

```python
import matplotlib.pyplot as plt
import pandas as pd

results_nheads = [
  {"num_heads": 1, "train_loss": 3.2, "val_loss": 3.5, "tokens_per_sec": 400},
  {"num_heads": 1, "train_loss": 3.5, "val_loss": 3.4, "tokens_per_sec": 400},
  {"num_heads": 2, "train_loss": 2.8, "val_loss": 3.0, "tokens_per_sec": 400},
  {"num_heads": 2, "train_loss": 2.8, "val_loss": 3.0, "tokens_per_sec": 400},
  {"num_heads": 4, "train_loss": 2.5, "val_loss": 2.7, "tokens_per_sec": 400},
  {"num_heads": 4, "train_loss": 2.5, "val_loss": 2.7, "tokens_per_sec": 400},
  {"num_heads": 8, "train_loss": 2.3, "val_loss": 2.9, "tokens_per_sec": 400},
  {"num_heads": 8, "train_loss": 2.3, "val_loss": 2.9, "tokens_per_sec": 400},
]
pd.DataFrame(results_nheads).plot(x="num_heads", y="val_loss")
plt.xlabel("Number of attention heads")
plt.ylabel("Validation loss")

# and then in another code chunk
pd.DataFrame(results_nheads).plot(x="num_heads", y="tokens_per_sec")
```

### Tips

#### `fsspec` errors

> This is a drastic step to fix an issue with the Kaggle image. It will probably not be necessary for you.

If you get strage errors about `fsspec` when importing `datasets`, you may need to blow away and reinstall `fsspec`. Put this at the top of the very first code chunk:

```python
!rm -rfv /opt/conda/lib/python3.10/site-packages/fsspec-2024.3.0.dist-info/
```

#### Progress Bar

You can add a progress bar to your training loop by using the `tqdm` library. Here's how you can use it:

```python
import tqdm
```

and then in yor training loop:

```python
for example in tqdm.tqdm(train_tokenized):
```

#### Gradient Accumulation

You can speed up your Transformer training by using *gradient accumulation*. This simply means that instead of stepping the optimizer every iteration, you step it every N iterations. In code, instead of this:

```python
loss.backward()
optimizer.step()
optimizer.zero_grad()
losses.append(loss.item())
```

You would do this (which would give an effective batch size of 4, since each step only used a single sequence):

```python
loss.backward()
if sample_counter % 4 == 0:
    optimizer.step()
    optimizer.zero_grad()
losses.append(loss.item())
```

There's a trade-off between speed and learning here: the more you accumulate gradients, the faster your training will be, but the less often you'll be updating your model, so it might not actually learn faster. So you may need to change the learning rate a bit, depending how many iterations you accumulate gradients over. It reduces time per epoch, but I haven't checked whether this actually improves time to *convergence*.