---
title: "Embeddings"
revised: 2026
---

- Analogy: like a map: each object has its GPS coordinates, similar objects are neighbors
- Definition: a vector representation of an object, constructed to be useful for some task (not necessarily human-interpretable)
- Examples: words, sentences, images, movies, users, etc.

## Key Concepts

- **Body and Head**: A pretrained model can be split into a feature extractor (body) that produces embeddings and a classifier (head) that maps embeddings to predictions
- **Similarity**: Dot products and cosine similarity measure how close two embeddings are — similar items should have similar embeddings
- **Embeddings vs raw pixels**: Learned embeddings capture semantic meaning (what's in the image), while raw pixels capture surface appearance (color, brightness)
- **Prototypes**: The classifier's weight matrix contains a prototype vector for each class; prediction is just comparing an embedding to each prototype

[Slides](/slides/w07.html) (including graphics)

## Notebooks

- {{% notebook name="Image Embeddings" nbname="u07n1-image-embeddings.ipynb" %}}

Another Example: {{% notebook name="Sentence Embeddings" nbname="u08s1-sentence-embeddings.ipynb" %}}

## Further Exploration

We'll discuss this much more in CS 376, but here are some ideas for further exploration:

- Try the [SigLIP demo](https://colab.research.google.com/github/google-research/big_vision/blob/main/big_vision/configs/proj/image_text/SigLIP_demo.ipynb) that embeds images and text together. Try computing the dot products between a few texts that you write by hand. Does the dot product reflect the similarity of the texts? Repeat with images. What do you find? (Use Colab for this one.)

