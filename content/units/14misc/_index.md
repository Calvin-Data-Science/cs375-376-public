---
title: "376 Unit 6: Miscellaneous Topics"
weight: 12
---


- Explainable AI (XAI)
- Human-Centered AI
- ethics of training data

{{% details summary="Reading" %}}

### Background

Review my blog post on [Mapping to Mimicry](https://kenarnold.org/posts/map-to-mimic/). I wrote it in one short sprint; feedback welcome!

- More resources: [Ai generative art tools](https://pharmapsychotic.com/tools.html)

### Robotics

Rather than study theory, let's look at two recent blog advances:

- An upgrade on a classic RL approach (Q-learning): [Pre-training generalist agents using offline reinforcement learning – Google AI Blog](https://ai.googleblog.com/2023/02/pre-training-generalist-agents-using.html)
- A new kind of approach: just use Transformers for everything. [PaLM-E: An embodied multimodal language model – Google AI Blog](https://ai.googleblog.com/2023/03/palm-e-embodied-multimodal-language.html)

### Explainable and Human-Centered AI

[ACM Selects: Trustworthy AI in Healthcare #02](https://selects.acm.org/selections/trustworthy-ai-in-healthcare-02)

{{% /details %}}

{{% details summary="Supplemental" %}}

What happens when AI meets people? How can we ensure that AI results are:

- Correct,
- Just, and
- Useful?

The first two are the subject of a subfield called Fairness, Accountability, and Transparency; the last is the subject of much research in human-computer interaction (HCI) and computer-supported cooperative work (CSCW). We'll explore all three in these last two weeks of class.

### Correctness and Transparency / Explainability

Read one or more of these:

- [Explainable AI Guide](https://ex.pegg.io/) ("Your high-level guide to the set of tools and methods that helps humans understand AI/ML models and their predictions.")
- **Interpreting Neural Nets**: Skim one of these articles:
  - [The Building Blocks of Interpretability](https://distill.pub/2018/building-blocks/)
  - [Activation Atlas](https://distill.pub/2019/activation-atlas/)
  - [Visualizing Neural Networks with the Grand Tour](https://distill.pub/2020/grand-tour/)
  - [Multimodal Neurons in Artificial Neural Networks](https://distill.pub/2021/multimodal-neurons/)
- [Interpretable Machine Learning: Fundamental Principles and 10 Grand Challenges | Abstract](https://arxiv.org/abs/2103.11251)
- Techniques and limitations of post-hoc interpretability
  - [Problems with Shapley-value-based explanations as feature importance measures](http://proceedings.mlr.press/v119/kumar20e.html)
  - [The Science Behind InterpretML: SHAP - YouTube](https://www.youtube.com/watch?v=-taOhqkiuIo)
- Built-in interpretability: [imodels: leveraging the unreasonable effectiveness of rules – The Berkeley Artificial Intelligence Research Blog](https://bair.berkeley.edu/blog/2022/02/02/imodels/)
- [Hundreds of AI tools have been built to catch covid. None of them helped. | MIT Technology Review](https://www.technologyreview.com/2021/07/30/1030329/machine-learning-ai-failed-covid-hospital-diagnosis-pandemic)
  > Many unwittingly used a data set that contained chest scans of children who did not have covid as their examples of what non-covid cases looked like. But as a result, the AIs learned to identify kids, not covid.

Watch:

- Watch: [Stop doing "explainable" ML](https://www.youtube.com/watch?v=I0yrJz8uc5Q)

#### Supplemental Material

- See the "Hall of Fame" list at [5th VISxAI Workshop at IEEE VIS 2022](https://visxai.io/) (also the list of examples under the Call for Participation)
- [PyTorch implementation for Transformer Interpretability Beyond Attention Visualization](https://github.com/hila-chefer/Transformer-Explainability)

### Justice (Fairness, Bias)

- Read one of the articles in [ACM Selects on Algorithmic Fairness](https://selects.acm.org/selections/why-algorithmic-fairness)
- Prefer to watch something? [21 fairness definitions and their politics](https://www.youtube.com/watch?v=jIXIuYdnyyk)

Supplemental: [The Effects of Regularization and Data Augmentation are Class Dependent | Abstract](https://arxiv.org/abs/2204.03632)

### Usability

Read or watch something from [Human-Centered Artificial Intelligence](https://hcil.umd.edu/human-centered-ai/).

{{% /details %}}


## Reinforcement Learning


Recommended but not essential:

- Watch MIT 6.S191 Lecture 5: Deep Reinforcement Learning: \[[Slides](http://introtodeeplearning.com/2021/slides/6S191_MIT_DeepLearning_L5.pdf)\], \[[Video](https://www.youtube.com/watch?v=93M1l_nrhpQ&list=PLtBw6njQRU-rwp5__7C0oIVt26ZgjG9NI&index=6)\]


### Supplemental Material

- Contextual
  - [AlphaGo Documentary](https://www.youtube.com/watch?v=WXuK6gekU1Y)
  - [ACM Selects: AI for Robotics](https://selects.acm.org/selections/ai-for-robotics)
- Technical
  - Using Sequence Models for RL
    - Overview: [Hugging Face blog post](https://huggingface.co/blog/decision-transformers)
    - [Sequence Modeling Solutions for Reinforcement Learning Problems](https://bair.berkeley.edu/blog/2021/11/19/trajectory-transformer/) (a simple and clever approach)
      - See also: [Decision Transformer: Reinforcement Learning via Sequence Modeling | Papers With Code](https://paperswithcode.com/paper/decision-transformer-reinforcement-learning?from=n11)
  - [Spinning Up in Deep RL](https://spinningup.openai.com/en/latest/) - a hands-on introduction to reinforcement learning in PyTorch by OpenAI
  - Creativity and Exploration
    - one example paper: [BeBold: Exploration Beyond the Boundary of Explored Regions | Abstract](https://arxiv.org/abs/2012.08621)


Reinforcement Learning (learning from feedback)

- Reward Discounting, quantifying the good life, and value alignment
  - Jesus’s discount factor: he endured the cross for the joy set before him. Infinite time horizon, no convergence problems.
- Types of learning: Supervised, Self-Supervised, Reinforcement
- Challenges of RL
  - Exploration
  - Credit assignment
- RL formalism: Markov Decision Process
- What functions can we learn: value, Q, policy (see [lab](lab/))
- (Didn't get to) How does [MuZero](https://deepmind.com/blog/article/muzero-mastering-go-chess-shogi-and-atari-without-rules) work?
