---
title: "Notes: Introduction to Generative Modeling"
weight: 2
revised: 2026
---

These notes are reference material for Unit 1. Read through them before class and annotate on Perusall with questions or connections.

## What is a Language Model?

A **language model** (LM) is a probability distribution over sequences of tokens. It assigns a probability to every possible document:

- P("tell me a joke") = 0.0001
- P("tell me a story") = 0.0002
- etc.

In practice, language models are trained to **predict the next word** (or token) in a document. This is a classification task:

- **Input**: the document up to the current position
- **Output**: a probability distribution over all possible next tokens

The training set is a huge collection of documents (web pages, books, code, etc.), and the model learns by minimizing **surprise** --- how much probability mass it put on the token that actually came next.

### Self-Supervised Learning

Notice what's *not* required here: labels. Nobody has to annotate each document with "the correct next word" --- the next word *is already there* in the text. The model creates its own training signal from the structure of the data itself. This is called **self-supervised learning**, and it's the key insight that lets language models train on essentially the entire internet without any human annotation.

This is what makes foundation models possible: because the training signal is free, we can scale to datasets that would be impossible to label by hand.

## Conditional Distributions

A **conditional distribution** is a probability distribution of one thing given another:

- P(next word | words so far)
- P(ambient temperature at time *t* | temperature at time *t*−1)
- P(rest of image | part of image)
- P(image | text prompt)

Language models give us P(next token | context). This is the building block for everything else.

## Three Approaches to Generative Modeling

There are three main ways to set up a generative model. Each answers the question "how do we sample from a complex distribution?" differently.

### Autoregressive

Generate one piece at a time, left to right. Each step predicts the next token given everything before it. This is how most language models (GPT, Claude, Gemma, etc.) work.

- **Strengths**: Conceptually simple (it's just classification, repeated), scales well, great for sequential data like text.
- **Limitations**: Can't "look ahead" or plan the ending before writing the beginning. Generation is inherently sequential --- you can't parallelize it.
- **Examples**: GPT, Claude, Gemini, Llama, Gemma --- essentially all modern chatbots.

### Latent Variable

Sample a compact "code" **z** from a simple distribution (like a Gaussian), then decode it into the full output. The key idea is that high-dimensional data (like images) actually lives on a lower-dimensional *manifold* --- a latent variable model tries to learn that manifold.

- **Strengths**: Can generate in one shot (no sequential steps), the latent space can capture meaningful variation --- smoothly interpolating between latent codes produces smooth variation in the output.
- **Limitations**: Can be hard to train. Variational Autoencoders (VAEs) often produce blurry outputs. Generative Adversarial Networks (GANs) can suffer from mode collapse (only generating a subset of possible outputs).
- **Examples**: VAEs, GANs. See [StyleGAN interpolations](https://www.youtube.com/watch?v=K8jY-GmvcAY) for a striking demo of smoothly blending between faces by moving through latent space.

### Diffusion

Start with pure noise and iteratively remove it, guided by a learned model. The model is trained to predict "what noise was added?" at each step, and generation works by repeatedly denoising.

- **Strengths**: Produces very high-quality images, training is stable (unlike GANs).
- **Limitations**: Slow --- requires many denoising steps (typically 20-50+), making generation much more expensive than a single forward pass. Each step is also computationally expensive.
- **Examples**: FLUX, Stable Diffusion, DALL-E 3, Midjourney. For a text example, see [InceptionLabs Diffusion LM](https://www.inceptionlabs.ai/news).
- **Interactive**: [Diffusion Explainer](https://poloclub.github.io/diffusion-explainer/) walks through the process step by step.

We'll focus primarily on autoregressive models in this course, since they power most modern LLMs.

## Autoregressive (Causal) Language Modeling

An autoregressive model factors the probability of a whole document into a product of next-token predictions:

> P(tell, me, a, joke) = P(tell) × P(me | tell) × P(a | tell, me) × P(joke | tell, me, a)

This is called **causal** language modeling because each prediction only depends on what came *before* --- the model never looks ahead.

Intuition: imagine someone constantly trying to finish your sentence. At each position, they have a distribution over what word might come next. Some positions are highly constrained ("the United States of ___"); others are wide open ("Once upon a ___").

### The Classifier Inside

The next-token prediction works like a classifier we'd recognize from CS 375:

1. A neural network processes the context and produces a **context vector** (embedding)
2. For each word in the vocabulary, compute a score: **logit** = dot product of word embedding and context vector
3. Apply **softmax** to get probabilities: P(word | context)

This is the same structure as logistic regression on learned features: the neural net builds a feature vector, then we score each class by how well it "matches."

### Implications of Left-to-Right Generation

Because the model generates left to right:

- It **never looks ahead**. It can't plan the ending of a sentence before writing the beginning.
- Its "memory" is **externalized** in the tokens it has already generated. We can manipulate that memory by editing the document so far.
- When you press "Retry" on ChatGPT, you're drawing another sample from the same conditional distribution. You'll almost certainly get a different response.
- Some models are trained to "fill in the middle" (FIM), but internally this is still implemented as a left-to-right sequence with special markers.

### Chat as Document

How does a chatbot work if the model just predicts the next token in a document? The trick: a conversation *is* a document. A multi-turn chat gets formatted with special markers like:

```
<|user|> Tell me a joke about atoms.
<|assistant|> Why don't scientists trust atoms? Because they make up everything!
<|user|> Now make it about chemistry.
<|assistant|>
```

The model generates the assistant's reply by continuing this document left to right, one token at a time. It doesn't "know" it's in a conversation --- it's just predicting what comes next in a document that happens to look like a conversation. Even tool calls, system prompts, and multi-turn context are just more text in the document.

This means the model's behavior is shaped entirely by what's in the document so far. Change the system prompt, and you change the "character" of the document the model is continuing.

<details>
<summary>Aside: Masked language modeling</summary>

Not all language models are autoregressive. **Masked language models** (like BERT) are trained to reconstruct randomly hidden tokens from their surrounding context, rather than predicting left to right. This lets the model "see" context in both directions, which turns out to be useful for learning good embeddings of whole sequences (used in vector databases and search). However, masked models can "cheat" in ways that make them less suited for generation tasks, so most modern generative models are autoregressive.
</details>

## Tokenization: Text to Numbers and Back

Neural networks work with numbers. How do we convert text into numbers?

**Tokenization** has two parts:

1. **Splitting** a string into tokens (substrings)
2. **Mapping** each token to a number via a fixed **vocabulary** (a lookup table)

### Approaches to Splitting

| Approach | Pros | Cons |
|----------|------|------|
| **Characters** | Handles any word, small vocabulary | Many tokens per word, hard to learn long-range patterns |
| **Whole words** | One token per word, easy to interpret | Can't handle unknown words, no sharing between "dog" and "dogs" |
| **Subwords** (modern) | Best of both: common words get one token, rare words split into pieces | Tokenizer choice affects model behavior |

Modern models use **subword tokenization** (e.g., Byte-Pair Encoding). Common words like "the" get a single token; rare words like "fearsome" might split into "fears" + "ome".

You can explore this yourself: [OpenAI Tokenizer](https://platform.openai.com/tokenizer)

### Why Tokenizer Choice Matters

The tokenizer affects:

- **Memory**: how many embeddings the model must store
- **Computation**: the cost of computing logits over the vocabulary
- **Efficiency**: how many tokens are needed to represent a given text (more tokens = more computation and more of the context window used up)
- **Generalization**: how well the model handles morphological variations and multiple languages
- **Capabilities**: e.g., whether each digit gets its own token affects math ability

## Sampling: Generating Text from a Model

The model gives us a distribution over the *next* token. To generate a whole sequence:

1. Start with a prompt
2. Compute P(next token | context)
3. Pick a token from that distribution
4. Append it to the context
5. Repeat until a stop token is generated

### Sampling Strategies

- **Greedy**: always pick the most likely token. Deterministic but often flat and repetitive.
- **Random sampling**: draw from the full distribution. Can produce surprising or incoherent output.
- **Temperature**: divide logits by a temperature *T* before softmax.
  - *T* = 1: no change (standard sampling)
  - *T* → 0: approaches greedy (always the top token)
  - *T* → ∞: approaches uniform random (all tokens equally likely)
- **Top-k**: only sample from the *k* most likely tokens
- **Top-p (nucleus sampling)**: only sample from the smallest set of tokens whose cumulative probability exceeds *p* (e.g., 90%)

<details>
<summary>Code: sampling from a discrete distribution</summary>

This isn't specific to ML --- it's a general technique for sampling from any discrete probability distribution:

```python
import numpy as np

def sample(probs):
    """Sample a token index from a probability distribution."""
    return np.random.choice(len(probs), p=probs)
```

Under the hood, this works by computing cumulative probabilities and drawing a uniform random number:

```python
cumulative_probs = np.cumsum(probs)
r = np.random.uniform()
for i, cp in enumerate(cumulative_probs):
    if r < cp:
        return i
```

</details>

In practice, human language rarely picks the single most likely next word (otherwise, why communicate at all?), so greedy generation produces text that feels unusually dull. But too much randomness produces nonsense. Temperature and top-p give us a knob to balance predictability and interestingness.

## Evaluating Language Models

A good language model should assign high probability to text that actually occurs. We measure this with:

- **Likelihood**: P(word₁, word₂, ...) = product of all next-token probabilities. This number is tiny for long sequences.
- **Log-likelihood**: sum of log probabilities. More numerically stable.
- **Cross-entropy**: the average negative log-likelihood per token. Lower is better.
- **Perplexity**: e^(cross-entropy). Intuition: a perplexity of 10 means the model is, on average, as uncertain as if it were choosing uniformly among 10 options at each step.

For reference: a fair coin has perplexity 2; a fair six-sided die has perplexity 6. Modern LLMs on English text typically achieve perplexities in the single digits.

## Log-Likelihood: The Math

The model assigns a probability to a document by factoring it as a product of conditionals:

P(document) = P(word₁) × P(word₂ | word₁) × P(word₃ | word₁, word₂) × ...

Since these probabilities are tiny, we take the log:

log P(document) = log P(word₁) + log P(word₂ | word₁) + log P(word₃ | word₁, word₂) + ...

The negative of this sum is the **cross-entropy loss** (also called negative log-likelihood, NLL). Dividing by the number of tokens gives the **average cross-entropy per token**.

The model outputs **logits** (raw scores), which are passed through softmax to get probabilities. Training minimizes cross-entropy loss via stochastic gradient descent.
