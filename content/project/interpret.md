---
title: "Interpretability Initiative"
---

## Introduction

- [The Mechanistic Interpretability Hackathon - itch.io](https://itch.io/jam/mechint)  
  - [TraCR-Supported Mechanistic Interpretability by Esben Kran, ElliotJDavies, h6](https://esbenkc.itch.io/tracr)  
- [200 Concrete Open Problems in Mechanistic Interpretability: Introduction - AI Alignment Forum](https://www.alignmentforum.org/s/yivyHaCAmMJ3CqSyj/p/LbrPTJ4fmABEdEnLf#:~:text=researcher%E2%80%99s%20opinions%20too!-,Introduction,And%20I%20think%20that%20this%20would%20be%20a%20profound%20scientific%20accomplishment.,-Purpose)  
  - https://colab.research.google.com/drive/1dYQjd8996qcoHiUpEfUgCwRQASc2w2cO  
- [(1) Neel Nanda on Twitter: "I've spent the past few months exploring @OpenAI's grokking result through the lens of mechanistic interpretability. I fully reverse engineered the modular addition model, and looked at what it does when training. So what's up with grokking? A 🧵... (1/17) https://t.co/AutzPTjz6g" / Twitter](https://twitter.com/NeelNanda5/status/1559060507524403200)  
- [We Found An Neuron in GPT-2 - Clement Neo](https://clementneo.com/posts/2023/02/11/we-found-an-neuron)  
- [Discovering Latent Concepts Learned in BERT | OpenReview](https://openreview.net/forum?id=POTMtpYI1xH)  
- [Interpretability in the Wild: a Circuit for Indirect Object Identification in GPT-2 small | Abstract](https://arxiv.org/abs/2211.00593)  
- A cool example: [Othello-GPT](https://thegradient.pub/othello/)

## Projects

### Learning to compress a prompt

Suppose a prompt is given as an instruction, like "Rewrite this in limerick form." Can we replace that instruction with a single word or phrase?

Recent work has learned soft prompts to do this. But it's hard to understand why these prompts work. So: what if we give the soft prompts a bottleneck: they have to be a simple function of a linear combination of tokens, and we have to be able to generate those tokens from the full prompt.

Resources:

- [Guiding Frozen Language Models with Learned Soft Prompts – Google AI Blog](https://ai.googleblog.com/2022/02/guiding-frozen-language-models-with.html)
- [🔴 Interpretable Soft Prompts | Learn Prompting](https://learnprompting.org/docs/trainable/discretized)
- [prompt_learning - prompt_learning.pdf](https://people.cs.umass.edu/~miyyer/cs685/slides/prompt_learning.pdf)


### What training data is used for a prompt?

It's often hard to understand *why* a LM can perform, or fail at, a particular task. But we know that it learns these abilities from training data?

Could we find a set of training examples that the model might have used to construct the behaviors that make that task work?

One metric of success: if we make some change to the model that makes it not work as well on that specific training data (hm, maybe by gradient *ascent*?), its performance on that task is hindered but not its performance on other tasks? (Or vice versa: worsen its performance on a specific task, see which training data it's now more perplexed about.)

Related idea: find gradient ascent directions that worsen performance on one task while not affecting performance on related tasks.


### What unusual ways can get LMs to "speak"?

Examples:

- saying each word twice
- spelling out each word
- alliterating

Questions:

- What its representation looks like for this sort of task?
- How to get it into that "mode"?
- How the success of different ways of getting it into that mode change with size or training

Resources:

[EleutherAI/pythia: Pythia: Interpreting Autoregressive Transformers Across Time and Scale](https://github.com/EleutherAI/pythia)
