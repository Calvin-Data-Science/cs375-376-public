---
title: "Discussion 12: A State-of-the-Art Language Model"
date: 2022-04-08
due: 2022-04-13
---

This week's Discussion is a slightly different format.

The goal is:

- Reflect on what went into a state-of-the-art large language model.

Since there's many different aspects to engage with, and different people will have different interests and perspectives, I've made this a Discussion so you can benefit from chatting about it with each other.

## State-of-the-Art in Sequence Modeling

Google recently released a paper on an enormous language model that they built. First, **skim their [blog post](https://ai.googleblog.com/2022/04/pathways-language-model-palm-scaling-to.html)**. Then, open up the [paper](https://arxiv.org/abs/2204.02311). Don't read all of it. Instead, **pick one or two of the following items** and **write a short response**.

- **Architecture**: How does this model relate with the models we have been studying (Transformers in general, or specific models like GPT-2 or MarianMT that we used in notebooks)? Specifically, section 2 describes various modifications to the standard architecture.
  - What aspects of the model architecture or training setup (e.g., vocabulary) do you think you understand? Make a sketch of that part of the model, either on paper or in code.
  - What aspects do you not quite understand?
- **Infrastructure**: What technical problems did they have to solve to get this model to train quickly and correctly? What considerations came up that you might not have expected? How big of a model could you train on infrastructure you can access free (our lab machines, Borg, Google Colab)?
- **Training setup**: You should be able to read much of Section 5. What do you find interesting? What length of documents do you expect this model to be able to handle?
- **Experiments**: pick one or two experiments (sections 6 through 9). What is the experiment meant to test? What input was provided to the model? What output did it generate? Was any fine-tuning required? What do you think about the example results given?
- **Bias, Fairness, and Ethics**: See sections 10 and 11, and Appendices B--E. What do we learn from this model? Is it good that this model exists? Was it worth the environmental cost to train? Should Google deploy anything based on it in their products?
- **Vocation**: Read Appendix A (Contributions). Which part could you see yourself doing?

## Post

Post in this week's discussion forum about what you observed. Your post should be about two paragraphs in length, which can be either (1) one paragraph about each of two things from the paper, or (2) a longer reflection about one thing from the paper.

Then, reply to one other post.

Guidelines:

- A good initial post will include enough background to be understandable to someone who hasn't read that part of the paper. (You can assume that your reader has skimmed the blog post though.)
- A good reply might ask a relevant question or make a connection with a different topic (such as the one you posted about).
