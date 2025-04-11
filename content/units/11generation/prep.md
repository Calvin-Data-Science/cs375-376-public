---
title: "376 Preparation 4"
weight: 1
revised: 2024
---

Find answers to the following questions; the articles below should be helpful.

1. How can a causal language model be used to power a dialog agent? (What does a "document" look like?)
2. What is "few-shot learning", aka "in-context learning", and how is it helpful for getting a LM to do what you want?
3. How does "chain of thought" prompting help a model reason better? (What does that have to do with autoregressive generation?)
4. How does "tool use" work in LMs?
5. How could you get a model to give an output in a specific structure that you could use in a program?
6. In general, how can you use a "chat" API to do useful things?
7. Are LM outputs always accurate? How can you tell?

Some resources:

- Azure Prompt Engineering Tips: [Chat-Style](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/advanced-prompt-engineering?pivots=programming-language-chat-completions) and [Completions-Style](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/advanced-prompt-engineering?pivots=programming-language-completions)
- [What Makes a Dialog Agent Useful?](https://huggingface.co/blog/dialog-agents)
  - You may also want to skim [Illustrating Reinforcement Learning from Human Feedback (RLHF)](https://huggingface.co/blog/rlhf)
- [Chat Templates: An End to the Silent Performance Killer](https://huggingface.co/blog/chat-templates)
- [Prompt Engineering Guide | Learn Prompting: Your Guide to Communicating with AI](https://learnprompting.org/docs/intro). Some highlights:
  - [🟢 Build ChatGPT from GPT-3](https://learnprompting.org/docs/applied_prompting/build_chatgpt)
  - [🟡 LLMs Using Tools](https://learnprompting.org/docs/advanced_applications/mrkl) or [🟡 Math](https://learnprompting.org/docs/reliability/math)
- [How Chain-of-Thought Reasoning Helps Neural Networks Compute | Quanta Magazine](https://www.quantamagazine.org/how-chain-of-thought-reasoning-helps-neural-networks-compute-20240321/)

## Supplemental Material

- **Read** A basic introduction to *decoding*: [How to generate text: using different decoding methods for language generation with Transformers](https://huggingface.co/blog/how-to-generate)
- **Watch** Lecture 4 of [MIT 6.S191](http://introtodeeplearning.com/) (skim Lecture 3 if needed)

We probably won't get to this until next week, but:

[The Illustrated Stable Diffusion – Jay Alammar – Visualizing machine learning one concept at a time.](https://jalammar.github.io/illustrated-stable-diffusion/)


- [Some slides](https://web.stanford.edu/class/cs224n/slides/cs224n-2019-lecture15-nlg.pdf)
- An extensive collection of notebooks on generative models: [Hitchhiker's Guide To The Latent Space: Community Notebook Document - Google Docs](https://docs.google.com/document/d/1ON4unvrGC2fSEAHMVb4idopPlWmzM0Lx5cxiOXG47k4/edit)
- Here's a good intro to text-guided image generation and manipulation: [StyleCLIP: Text-Driven Manipulation of StyleGAN Imagery](https://github.com/orpatashnik/StyleCLIP) ([paper](https://arxiv.org/abs/2103.17249))




I found the [Foreward](https://link.springer.com/content/pdf/bfm%3A978-3-030-93158-2%2F1.pdf) to this [book on Deep Generative Modeling](https://link.springer.com/book/10.1007/978-3-030-93158-2) (Available through Calvin library) to be reasonably accessible, but you may prefer the author's [blog posts](https://jmtomczak.github.io/blog.html). ([github](https://github.com/jmtomczak/intro_dgm)).

Now, how do you control *what* gets generated?

- Controlling generated text
  - [Prefix-Tuning: Optimizing Continuous Prompts for Generation](https://arxiv.org/abs/2101.00190); extension: [Control Prefixes for Text Generation](https://arxiv.org/abs/2110.08329)
- Captioning images
  - [Multimodal Few-Shot Learning with Frozen Language Models](https://arxiv.org/abs/2106.13884); extension: [MAGMA -- Multimodal Augmentation of Generative Models through Adapter-based Finetuning](https://arxiv.org/abs/2112.05253)
- Generating images
  - [GLIDE: Towards Photorealistic Image Generation and Editing with Text-Guided Diffusion Models | Abstract](https://arxiv.org/abs/2112.10741)
  - *probably the best starting point for a project like this*: [Autoregressive Image Generation using Residual Quantization | Papers With Code](https://paperswithcode.com/paper/autoregressive-image-generation-using?from=n28) - pretrained models in the [official implementation](https://github.com/kakaobrain/rq-vae-transformer), nice clean implementation in [lucidrains/vector-quantize-pytorch: Vector Quantization, in Pytorch](https://github.com/lucidrains/vector-quantize-pytorch)

