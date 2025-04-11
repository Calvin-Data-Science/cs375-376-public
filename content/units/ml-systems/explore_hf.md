---
title: "Exploring open-weights models on Hugging Face"
revised: 2025
---

Today we're going to try out some of the open-weights models that are available on Hugging Face.

Objectives:

- I've used a high-level API to run a neural network model.
- I've generated an array of class probabilities.
- I've computed the similarity between two embeddings and compared that with another pairwise similarity.

## Background

Hugging Face is a company that provides a platform for sharing and using pre-trained models. They provide:

- A [model hub](https://huggingface.co/models) where you can find and download models.
- A hosting service called [Spaces](https://huggingface.co/spaces) where people can share their models.
- Python libraries for working with models, including:
  - `transformers` for working with models.
  - `datasets` for working with datasets.

## Explore

Let's start by playing with a few Spaces, then we'll try out some models.

### Spaces

Go to the [Spaces](https://huggingface.co/spaces) page. Try out two or three different Spaces:

- One that's highlighted or trending
- One that is designed for a task that you might be interested in exploring for a project
- One that is designed for a task that you're not familiar with

A few that I tried out in February 2025:

- RL
    - [Interactive DeepRL Demo - a Hugging Face Space by flowers-team](https://huggingface.co/spaces/flowers-team/Interactive_DeepRL_Demo)
- Sound / Music
    - [MusicGen Web - a Hugging Face Space by Xenova](https://huggingface.co/spaces/Xenova/musicgen-web)
    - [Riffusion • Spectrogram To Music - a Hugging Face Space by fffiloni](https://huggingface.co/spaces/fffiloni/spectrogram-to-music)
- Images
    - [FLUX.1 [dev] - a Hugging Face Space by black-forest-labs](https://huggingface.co/spaces/black-forest-labs/FLUX.1-dev)
- Agents
    - [Travel Planning Agent - a Hugging Face Space by acidtib](https://huggingface.co/spaces/acidtib/Travel-Planning-Agent) (from an index at [smolagents and tools gallery - a Hugging Face Space by davidberenstein1957](https://huggingface.co/spaces/davidberenstein1957/smolagents-and-tools) -- see the "execution logs" in the chat results)

### Embedding Models

- Explore {{% notebook name="Sentence Embeddings" nbname="u08s1-sentence-embeddings.ipynb" %}} (**this one needs Colab**; Kaggle doesn't seem to support the tensorboard viewer that this uses.). Try computing the embeddings for some sentences that you create by hand, and then computing the cosine similarity between them. What do you find? Are similar sentences closer together in the embedding space?
- Try the [SigLIP demo](https://colab.research.google.com/github/google-research/big_vision/blob/main/big_vision/configs/proj/image_text/SigLIP_demo.ipynb) that embeds images and text together. Try computing the dot products between a few texts that you write by hand. Does the dot product reflect the similarity of the texts? Repeat with images. What do you find? (This one definitely needs Colab.)
