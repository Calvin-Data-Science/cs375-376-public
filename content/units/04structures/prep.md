---
title: "Preparation 4"
weight: 1
revised: 2024
---

{{% perusall %}}

- {{% chollet sec="3" %}}

{{% /perusall %}}

Additionally, work through the following interactive articles:

- [Neural Networks](https://mlu-explain.github.io/neural-networks/)
  - Note: when they draw a box with an activation function in it, they actually mean a linear layer with that activation function on the output


### Prep Notes

- For this week, focus on how things are *used* rather than the underlying math
- The book uses "rank" to refer to the number of axes of a tensor, but "rank" means something different in linear algebra. To avoid confusion, let's call it "number of axes", or perhaps "number of dimensions" (abbreviated "ndim" in PyTorch).
  - For example, a length-5 column vector times a length-4 row vector would give a matrix (tensor) with two axes (2-dimensional), with shape (5, 4) and rank 1 in the linear algebra sense. See [this notebook](https://nbviewer.jupyter.org/github/kcarnold/cs344/blob/main/src/Number_of_Dimensions_is_not_Rank.ipynb).



## Optional Material

Watch [Zero to Hero](https://karpathy.ai/zero-to-hero.html) part 1: [The spelled-out intro to neural networks and backpropagation: building micrograd](https://www.youtube.com/watch?v=VMj-3S1tku0)

- First, watch the video and take conceptual notes.
- Then, do [these exercises](https://colab.research.google.com/drive/1FPTx1RXtBfc4MaTkf7viZZD4U2F9gtKN?usp=sharing#scrollTo=qXaH59eL9zxf)
- Then, re-watch and write the code along with him.

There are too many videos out there on deep learning to list here, but here's a few very different styles:

- (MIT) [Lecture 1 of MIT 6.S191 Deep Learning](https://www.youtube.com/watch?v=5tvmMX8r_OM&list=PLtBw6njQRU-rwp5__7C0oIVt26ZgjG9NI&index=1)
- (elementary) [CrashCourse AI Playlist](https://www.youtube.com/playlist?list=PL8dPuuaLjXtO65LeD2p4_Sb5XQ51par_b)
- (mathy) [3Blue1Brown Neural Networks](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi) (highly recommended channel for math, but these particular videos seem less intuitive than their typical videos)

I made a [video walking through backpropagation](https://www.youtube.com/playlist?list=PLYvyo-La3zBMsd_9WAF7MrfjwmkxuXrTb) on a simple example.

## Elo Notes

We're using Elo scores for intuition a few times this week, but we're intentionally not diving deep on it. If you do want to dive deep:

- [Elo as a statistical learning model | Steven Morse](https://stmorse.github.io/journal/Elo.html)
- [FiveThirtyEight's Elo Ratings and Logistic Regression – Nic Dobson – half a thought in the head](https://nicidob.github.io/nba_elo/)
