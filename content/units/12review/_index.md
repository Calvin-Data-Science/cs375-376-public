---
title: "Review"
revised: 2025
---

- LLMs view the world as a sequence of tokens
  - tokenization approach and vocabulary size is chosen before training
  - which tokens to use are determined by some training data
- LLMs learn to mimic sequences of tokens
  - by learning to predict the next token
    - by learning conditional distributions `P(next token | sequence so far)`
    - by learning to maximize the probability given to the actual next token (minimizing cross-entropy loss / perplexity)
- LLMs compute next-token distributions by asking "what sort of token usually comes next in this context?"
  - computes a score for each token in the vocabulary
    - by computing a dot product between the token embedding and the context embedding
      - a table of token embeddings is learned during training to put tokens that occur in similar contexts close together
  - context embeddings are computed based on the embeddings of prior tokens
    - for each token, we need to compute a context vector for predicting the next token
    - we could:
      - use the embedding of the current token (but then the model would just repeat itself)
      - use a neural network ("feed-forward network") to transform each token's embedding (but then we lose the information about the other tokens)
      - average the embeddings of all previous tokens (but then we're overwhelmed by irrelevant information)
      - use a weighted average of the embeddings of all previous tokens (but then we need to learn the weights)
      - use a neural network to compute the weights for the averaging (but then we can't change the information that each token carries)
      - use another neural network to compute *what* information each token shares with each other token (and now we get self-attention)
      - add more layers (alternating self-attention and feed-forward layers) to make it more expressive
      - add lots of tweaks to make it easier to learn (e.g., residual connections, layer normalization, etc.)
