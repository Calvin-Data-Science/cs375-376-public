---
title: "Token and Context Embeddings"
revised: 2024
weight: 3
---

In this activity, we will manually come up with token and context embeddings for family relationships.

## Token Embeddings

The token embeddings are the vectors that represent the words in the vocabulary. We will use the following words for our vocabulary:

| Word     | x | y |
|----------|---|---|
| father   |   |   |
| mother   |   |   |
| son      |   |   |
| daughter |   |   |
| brother  |   |   |
| sister   |   |   |
| uncle    |   |   |
| aunt     |   |   |
| his      |   |   |
| her      |   |   |

Instructions:

1. Sketch a 2D coordinate system. Label each axis by some attribute that separates some of these words from others (e.g., generation).
2. Place each word somewhere in this space. You should find that similar words are close together. (You might start with the first 4.)
3. Write down the coordinates of each word in your space a table like the one above.

## Vector Arithmetic

Subtract the vector for "father" from the vector for "son". Add the result to the vector for "daughter". What word is closest to the resulting vector?

Repeat this process for "brother" and "sister". What word is closest to the resulting vector?

Repeat this process, but instead of looking for the *closest* word, look for the token with the largest *dot product* with the resulting vector. What word is that?

## Context Embeddings

In a next-token prediction task, the context embeddings are the vectors that represent the words that come before the token you are trying to predict. Consider the following sentence prefixes:

- "Martin Jr. was named after his"
- "At the parent-teacher conference, the boy's"
- "If Alice is my aunt, then my mother is her"
- "If Bob is my uncle, then my father is his"
- *Write two more sentence prefixes of your own.*

Start by writing one or two possible tokens (from the list above) that could follow those prefixes. 

Suppose we use *dot products* to compute next-token logits. For each of the sentence prefixes above, construct a *context embedding* where the dot product gives reasonable next-token logits, given the token embeddings that you constructude above.

| Prefix | Next Token(s) | Context Embedding |
|--------|---------------|-------------------|
| "Martin Jr. was named after his" | | |
| "If Alice is my aunt, then my mother is her" | | |
| "If Bob is my uncle, then my father is his" | | |
| "At the parent-teacher conference, the boy's" | | |
| *your prefix* | | |
| *your prefix* | | |


## Dimensionality

In the above, you constructed 2D embeddings. However, you probably found that 2D couldn't capture all the relationships you wanted. Could you do better if you had a third dimension? Update your embeddings to include a third dimension, and see if you can better capture the relationships you want.

