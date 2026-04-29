---
title: "Schedule - CS376"
revised: 2026
toc: true
---

See also: [CS 375 Schedule](/schedule-375)

Any content in the future should be considered tentative and subject to change.


<div class="calendar-week">

## Week 1: Intro to Generative Modeling

{{% calendar-week-header %}}
Some of the most impactful developments in AI recently have come from modeling and generating *sequences*.
How do we model sequences? How do we generate them?
This unit will introduce some of the basic concepts and methods for sequence modeling and generation, with a focus on natural language processing (NLP).

{{% details summary="Terms" %}}
- Generative AI
- Language model
- Tokenization
- Vocabulary
- Autoregressive model
- Conditional distribution
- Latent variable model
- Diffusion model
- Perplexity

{{% /details %}}
{{% details summary="Key Questions" %}}
- What is one implication of the fact that LMs generate text sequentially (i.e., that most language models are causal)?
- What is a conditional distribution, in the context of language modeling (or another example we looked at in class)?
- How is a chat conversation (even with multiple turns, tool calls, etc.) just a document?

{{% /details %}}
{{% details summary="Objectives" %}}
This week will address course objectives on OG-SelfSupervised and OG-LLM-Tokenization.

- Explain what generative modeling is and its uses
- Describe the high-level idea of three basic approaches to generative models: autoregressive, latent variable, and diffusion
- Describe the inputs and outputs of an autoregressive language model
  - tokens -> embeddings
  - next-token conditional probability distribution
- Describe how a language model can be used for a chatbot.

{{% /details %}}
{{% details summary="Prep and Readings" %}}
Before starting this unit, you should already know the basics of supervised learning. Specifically, you should be comfortable with training a fully-connected neural network on a classification task.

I recommend the following readings (in Perusall):

- [Large Language Models explained briefly (3blue1brown)](https://www.youtube.com/watch?v=LPZh9BOjkQs&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi&index=5)
- the Hugging Face Transformers course, chapter 1:
    - 1.2 [Natural Language Processing - Hugging Face NLP Course](https://huggingface.co/learn/nlp-course/en/chapter1/2)
    - 1.4 [How do Transformers work? - Hugging Face NLP Course](https://huggingface.co/learn/nlp-course/en/chapter1/4)
- [Artificial Intelligence Then and Now – Communications of the ACM](https://cacm.acm.org/opinion/artificial-intelligence-then-and-now/)
    
If you need some additional background, I recommend [Understanding Deep Learning](https://udlbook.github.io/udlbook/)

You may also appreciate the following more technical resources, but these are not required:

- [OpenAI Tokenizer](https://platform.openai.com/tokenizer)

{{% /details %}}
{{% details summary="Extension Opportunities" %}}
- Activity: [Optional Extension: Token Efficiency Analysis](/units/08generative-intro/extension-tokenization)
- See: [SuperBPE](https://superbpe.github.io/): *multi-word tokens* (!)

{{% /details %}}
{{% details summary="Notes" %}}
[Notes page](/units/08generative-intro/notes/) for reference material on language models, tokenization, sampling, and evaluation.

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-03-16" %}}
- Scripture: [Psalm 23](https://www.biblegateway.com/passage/?search=Psalm%2023&version=NIV&interface=print)
- Slides: [376 Unit 1: Generative Modeling Introduction](/slides/w08-generative.html)
- Topics:
    - Intro
    - Logistics for 376 vs 375
    - Projects
    - Intro to Generative Modeling
- Handout: [What do you already know about generative modeling?](/handouts/2026_03_16.pdf)
- Surprise - fire alarm! (moving exploring-lm activity to Wednesday)

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-03-18" %}}
- Handout: [Exploring Language Models](/handouts/2026_03_18.pdf)
- This uses the [LM Internals tool](/lm-internals.html).
- Slides: [376 Unit 1: Generative Modeling Introduction](/slides/w08-generative.html)
  - Scripture: Proverbs
  - Readings, Moodle participation activity
  - Ways of Setting Up Generative Modeling (Autoregressive, Latent Variable, Diffusion)
    - Autoregressive Language Models as Classifiers
    - Perplexity as cumulative surprise
    - Implications of Autoregressive Generation
  - Text <-> Numbers

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-03-20" %}}
- Slides: [376 Unit 1: Generative Modeling Introduction](/slides/w08-generative.html)
  - Three approaches to generative modeling (autoregressive, latent variable, diffusion)
  - Tokenization
  - LLM APIs overview
- Intro [Discussion 376.1: Probing LLM Sycophancy](/units/08generative-intro/discussion/)
- Intro [Exercise 376.1: LM Evaluation](/units/09lm/homework/)
- Activity: [CS 376 Lab 1: Language Model Inputs and Outputs](/units/08generative-intro/lab)

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 2: Language Modeling

{{% calendar-week-header %}}
This week start to take off the covers of NLP models, just like we took off the covers of image models in CS 375. In particular, we'll get our first taste of the Transformer model, the most important model in machine learning today.

Advising is this week, so we won't get to a lot of new content.

{{% details summary="Key Questions" %}}
- Define *perplexity*, and describe how it relates to log-likelihood and cross-entropy (and the general concept of partial credit and/or surprise in classifiers)
- What is a token embedding? What is an output (or context) embedding? How do these relate to the input and output of a language model?
- How does a causal language model use embeddings of contexts (e.g., sentence prefixes)?
- How can we use a language model to generate text?

{{% /details %}}
{{% details summary="Objectives" %}}
This week we start work on these objectives:

- I can identify the shapes of data flowing through a Transformer-style language model. [TM-TransformerDataFlow]
- I can identify various types of embeddings (tokens, hidden states, output, key, and query) in a language model and explain their purpose. [TM-LLM-Embeddings]

{{% /details %}}
{{% details summary="Notes" %}}
- token and output embeddings work almost exactly like https://cs.calvin.edu/courses/cs/375/cur/notebooks/u07n1-image-embeddings.html

### Q&A

> How do models deal with really long conversations?

The system can cache the internal representation ("k-v cache") so it doesn't have to recompute the whole thing each time. But that takes RAM.

> Does autoregressive generation mean that the model can't plan ahead?

Not exactly. See [Tracing the thoughts of a large language model \ Anthropic](https://www.anthropic.com/research/tracing-thoughts-language-model): "Claude will plan what it will say many words ahead, and write to get to that destination.".

> Does committing to a direction mean that text might be incoherent?

Not necessarily. Better pre-training will mean that it gets examples of plausible continuations of even rare prefixes. And post-training (RLHF and other techniques) can help steer the model to put higher probability on paths that are likely to be coherent.

> How does the tokenizer decide where to split words?

The most common technique is called Byte Pair Encoding (BPE). It starts with a vocabulary of all the individual characters, and then iteratively merges the most common pairs of tokens into new tokens until it reaches the desired vocabulary size. For a deep dive, see [Byte-Pair Encoding tokenization · Hugging Face](https://huggingface.co/learn/llm-course/chapter6/5) or [Let's build the GPT Tokenizer - video by Andrej Karpathy](https://www.youtube.com/watch?v=zduSFxRajkE).

> Why are modern LMs so fast?

Some things that have helped make modern language models so fast are: quantization, which reduces memory bandwidth needed, specialized compute unit units like Google's TPUs, which just do memory multiplies really fast, and some algorithmic improvements like Flash Attention where researchers carefully thought through what memory access is actually required during inference and made an implementation that is highly optimized to the kind of hardware that we have.

> What do the human fine-tuners actually do?

Human fine tuners often do the kinds of tasks that you sometimes see ChatGPT asking: labeling which of these two options is better. Some of them also write reference answers that model should learn to imitate. The role of these sorts of labeling and feedback mechanisms will probably be changing as we see a shift to learning from computationally-generated feedback.

> Why do commercial LLMs not actually have much trouble with misspellings?

This has actually been one of the things that challenged my understanding the most over the past few years. I would have expected modern language models to have more trouble with misspellings and typos then they empirically seem to do. I think there are two explanations for this: first, and probably the main explanation is that at the scale of the Internet most typos have happened before. Second is that model providers may be introducing some deliberate errors, such as typos or misspellings into the pre-training process as a kind of data augmentation. I don't have any evidence that they're actually doing that though.

{{% /details %}}
{{% details summary="Terms" %}}
- language modeling
- n-gram
- token embeddings (sometimes called word embeddings)
- output embeddings (sometimes called hidden states or contextual embeddings)
- token logits
- temperature

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-03-23" %}}
Logistics:

- Scripture:
  - [Psalm 1](https://www.biblegateway.com/passage/?search=Psalm+1&version=NIV&interface=print)
  - [Jeremiah 17:7-8](https://www.biblegateway.com/passage/?search=Jeremiah%2017%3A7-8&version=NIV&interface=print)
- Reminders:
    - Complete "Reflections Week 1"
    - Discussion 1
- [Highlight-Edits example](https://huggingface.co/spaces/CalvinU/writing-prototypes)
- Project
  - NanoGPT [speedrun](https://github.com/karpathy/nanochat) -- or [Slowrun](https://github.com/qlabs-eng/slowrun)
  - do an active [Kaggle Competitions](https://www.kaggle.com/competitions)
- Signups sheet: devos, tech updates, leading discussion, pair programming

- Handout: [GenAI problem setup: approaches, LLM-as-classifier, chat-as-document, next-token distribution](/handouts/2026_03_23.pdf)

Tokenization:

- Run Google Image searches for: "how many r in strawberry" and "stable diffusion can't spell".

Activity: [Lab 376.2: Logits in Causal Language Models](/units/09lm/lab)

Supplemental material: [list comprehensions in Python](https://cs.calvin.edu/courses/cs/106/24fa/units/14bonus/slides.html#/list-comprehensions)

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-03-25" %}}
- Advising




{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-03-27" %}}
- Tech Update: [current Transformers release](https://github.com/huggingface/transformers/releases/tag/v5.4.0)
- Project Discussions
- Project Inspirations
  - An example related to our topic today: [How to make a racist AI without really trying | ConceptNet blog](https://concepts.arborelia.net/posts/2017/how-to-make-a-racist-ai-without-really-trying/)
- Review handout from last time
- Lab review
  - For reference:
  - Notebook: {{% notebook name="Image Embeddings" nbname="u07n1-image-embeddings.ipynb" %}}
- Handout: [Token and Context Embeddings, and Sampling Algorithm](/handouts/2026_03_27.pdf)
- Resources: the [softmax/cross-entropy interactive](https://observablehq.com/@kcarnold/softmax)

Topics:
- Token and Context Embeddings

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 3: Architectures

{{% calendar-week-header %}}
Now that we've seen the basic capabilities of NLP models, let's start getting under the hood. How do they work? How do we measure that?

The Transformers architecture (sometimes called *self-attention networks*) has been the power behind many recent advances not just in NLP but also vision, audio, etc.
That's because they're currently one of the best tools we have for representing *high-dimensional joint distributions*, such as the distribution over all possible sequences of words or images.
This week we'll see how they work!

We'll also look at other architectures that have been popular in the past, such as convolutional networks (CNNs) and recurrent networks (RNNs), and maybe even look at how some new architectures bring in ideas from those older architectures.

{{% details summary="Objectives" %}}
- [TM-SelfAttention](objective)
- [TM-TransformerDataFlow](objective)
- [TM-Architectures](objective) *(extension)*

{{% /details %}}
{{% details summary="Key Questions" %}}
By the end of this week you should be able to answer the following questions:

- What is a *layer* in a self-attention network: what goes in, what comes out, and what are the shapes of all those things?
- How do embeddings for words (or tokens) represent similarity / difference?
- Why are variable-length sequences challenging for neural nets? How do self-attention networks handle that challenge?
- How does data flow between tokens and between layers in a self-attention network? In what sense does it use *conditional logic*?
- What does an *attention head* do? Specifically, what are queries, keys, and values, and what do they do? And how does this relate with the *dot product* and *softmax*? (Wait, is this logistic classification yet again?)

Things we didn't explicitly get to this week:

- How do self-attention networks keep track of *position*?
- How does the data flow in Transformer networks differ from Convolutional or Recurrent networks?
- What are *encoder*s and *decoder*s? Why does that matter? What impact does that have on what you can do with the model?

{{% /details %}}
{{% details summary="Terms" %}}
- **attention**, especially self-attention
- **query**, **key**, and **value** vectors
- **attention weights**
- **multi-head attention**
- **feed-forward network** (MLP)
- **residual connection**
- **layer normalization** (bonus topic)

{{% /details %}}
{{% details summary="Prep and Reading" %}}
This week's reading includes a result from Anthropic that looks helpful for getting an accurate intuition about what's going on inside an LLM. We're looking at the high-level overview article this week; if people are interested we can dig into the technical report in a future week.

- 3blue1brown articles (you may prefer to watch the linked video at the top)
  - [3Blue1Brown - Visualizing Attention, a Transformer's Heart | Chapter 6, Deep Learning](https://www.3blue1brown.com/lessons/attention)
  - [3Blue1Brown - How might LLMs store facts | Chapter 7, Deep Learning](https://www.3blue1brown.com/lessons/mlp)
- [LLM Visualization](https://bbycroft.net/llm): an interactive article, take your time to walk through it over several sessions. It's very detailed, so don't expect to understanding everything at this point. The most important parts to pay attention to are:
  - What's the input look like (we've already studied this)
  - The attention mechanism
  - The MLP / Feed-Forward part (which should be familiar from CS 375)
  - The Output (again, we've already studied this, but it has a few more details)
- [Tracing the thoughts of a large language model \ Anthropic](https://www.anthropic.com/research/tracing-thoughts-language-model)
- Ethics: [Understanding Deep Learning book](https://udlbook.github.io/udlbook/) chapter 21, stopping at section 21.2.

News (in Perusall library, not officially assigned):

- [Vibe Coding (and Autonomous Agents) will bite you](https://decision.substack.com/p/vibe-coding-will-bite-you-heres-exactly)

{{% /details %}}
{{% details summary="Supplemental Resources" %}}
- Other neural network architectures (compare with self-attention):
  - Recurrent Networks: [Elman](https://en.wikipedia.org/wiki/Recurrent_neural_network#Architectures); [LSTM and GRU](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
  - Convolutional Networks:
    - What convolution does to an image: [Image Kernels explained visually](https://setosa.io/ev/image-kernels/)
    - How to use convolutions in a neural network: [CS231n Convolutional Neural Networks for Visual Recognition](https://cs231n.github.io/convolutional-networks/)
    - What they learn: [Feature Visualization](https://distill.pub/2017/feature-visualization/)
- A video course on [How Transformer LLMs Work - DeepLearning.AI](https://learn.deeplearning.ai/courses/how-transformer-llms-work/lesson/nfshb/introduction)
- Wanna code it? [Zero to Hero](https://karpathy.ai/zero-to-hero.html) part 6: [Let's build GPT: from scratch, in code, spelled out. - YouTube](https://www.youtube.com/watch?v=kCc8FmEb1nY) (go back to [prior parts](https://karpathy.ai/zero-to-hero.html) if you need to)
- [HandsOnLLM/Hands-On-Large-Language-Models: Official code repo for the O'Reilly Book - "Hands-On Large Language Models"](https://github.com/HandsOnLLM/Hands-On-Large-Language-Models)

{{% /details %}}
{{% details summary="Q&A" %}}
> Is there a limit to how far back a transformer can look? And how are they improving it? For example, in a chatbot with more context, you can feel that it is getting dumber.

"how far back a transformer can look" = its "context window". Things that limit that:

1. the architecture. if position embeds are absolute (not, say, RoPE), then we need to set a limit before we even start training.
2. computation. Plain self-attention is quadratic in sequence length. So long attention takes way more computation time. This has seen lots of effort to optimize recently.
3. Training. Gotta actually give the models examples of documents / conversations / etc. where long-range attention is needed, otherwise it won't learn it.

> How does increased communication [via self-attention] actually translate to better token generation?

Consider the case of asking an LLM to fix up a paragraph that you wrote. It needs to basically copy what you gave as input, but with some edits / changes at some places. Self-attention lets the network basically keep a running pointer to where you are in the input, grab what you said next, and repeat that or something similar in the output. A recurrent network (like LSTM), in contrast, would somehow have to encode your entire input into a single vector, and then decode that into the output, which is really challenging to learn to do reliably.

> How else to improve transformers, besides more training and more heads / layers / dimensions?

There's so many little tweaks that people do (read the tech report of any new model release). Common things people play with are how to encode position (RoPE is big now), playing with how keys/queries/values mix and match (Grouped Query Attention etc.), and the data, loss functions, etc. (e.g., reinforcement learning from various kinds of rewards).

> What does the [Anthropic article](https://www.anthropic.com/research/tracing-thoughts-language-model) mean by "Claude wasn't designed as a calculator—it was trained on text, not equipped with mathematical algorithms"?

The Transformer architecture is hugely inefficient and unreliable if all you want to do is addition or multiplication. But it had to learn to do that anyway, even with unreliable building blocks, because being able to add and multiply make the Internet a bit less surprising.

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-03-30" %}}
- Slides: [Neural Architectures](/slides/w10-nn-arch.html)
  - Intro
  - Review
- Review handout activity from Friday
  - Handout: [Token and Context Embeddings, and Sampling Algorithm](/handouts/2026_03_27.pdf)
  - Pair up, compare answers (5-10 min), then debrief
  - How does the model actually represent these tokens and contexts?
  - Let's write the sampling algorithm together.
- Notebook: {{% notebook name="Demo of Logits and Embeddings from a Language Model" nbname="u09n0-logits-demo.ipynb" %}}
  - Vector analogies, logit lens — what does the model "think" at each layer?
  - Concretely grounds embeddings before we move to self-attention
- Tease Wednesday: "Now that we know *what* embeddings are — how does the model decide which information to pay attention to?"
- Hand out the "Self-Attention By Hand" activity for Wednesday
  - Handout: [Self-Attention By Hand](/handouts/2026_04_01.pdf)

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-04-01" %}}
- [Mr. Chatterbox is a (weak) Victorian-era ethically trained model you can run on your own computer](https://simonwillison.net/2026/Mar/30/mr-chatterbox/) - a project idea?
  - Combine with [The assistant axis: situating and stabilizing the character of large language models \ Anthropic](https://www.anthropic.com/research/assistant-axis)?
- Slides: [Neural Architectures](/slides/w10-nn-arch.html) (self-attention section)
  - Birthday analogy exercises → Q/K/V intuition
  - Self-Attention: One Attention Head (formal definition)
  - Transformer block diagrams
- Handout: [Self-Attention By Hand](/handouts/2026_04_01.pdf)
  - Students work in pairs/teams, debrief
- [Transformer Explainer](https://poloclub.github.io/transformer-explainer/) (if time; otherwise assign as explore-over-break)
- Review: Self-Attention = conditional information flow
  - Software: describe the wiring, then what flows through the wires.
  - Hardware: compute queries, keys, and values, then compute the attention matrix, then compute the output.
- Start / preview self-attention lab:
  - Activity: [Lab 376.3: Implementing Self-Attention](/units/10arch/lab)
  - See "before next class"

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-04-03" %}}
- Good Friday

### Before next class (Wed Apr 8)

- Complete Self-Attention By Hand handout if not finished in class
- u10n1-implement-transformer notebook: work through Setup → Tokenization → MLP → "Trace the Simple Model" sections (stop before Self-Attention section)
- Reading: [3Blue1Brown attention video](https://www.3blue1brown.com/lessons/attention) + [Anthropic tracing-thoughts article](https://www.anthropic.com/research/tracing-thoughts-language-model)
- Study for Quiz 1 (Wed Apr 8)

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 4: Generation and Prompting

{{% calendar-week-header %}}
How can a model trained to mimic become a helpful, capable, mostly-harmless(?), and even semi-autonomous agent? We'll discuss how prompting techniques can get us partway there, but modern LLMs use extensive post-training from human and automated feedback to get the rest of the way.

{{% details summary="Key Questions" %}}
- How can each of the following be represented in a "document":
  - A conversation between a user and a model (assistant)
  - An action to take in the world (e.g., calling an API or running code)
- How might a helpful and harmless response differ from a mimicry response?
- How can we use feedback to tune a model's behavior?

{{% /details %}}
{{% details summary="Terms" %}}
- dialog agents
- prompting
- post-training (e.g., instruction tuning, Reinforcement Learning from Human Feedback (RLHF))

{{% /details %}}
{{% details summary="Objectives" %}}
Core objectives:

- [OG-LLM-Prompting](objective)
- [OG-LLM-ContextAndTools](objective)
- [OG-LLM-Train](objective)

Review objectives:

- [OG-LLM-Tokenization](objective)
- [TM-LLM-Generation](objective)

Extension objectives:

- [TM-LLM-Compute](objective)

{{% /details %}}
{{% details summary="Readings" %}}
All readings are posted on Perusall, copied here for reference.

- The [Tülu blog post](https://allenai.org/blog/tulu-3-technical) gives a great summary of the current state-of-the-art post-training process.
  - Make sure that you can identify the main steps in the overall process and what the main point of each one was.
  - Also pay attention to wear human input steers the model.
  - If you're curious beyond this, find the optional reading of the [OLMo2 article](https://allenai.org/blog/olmo2).
- The [Hugging Face article on agents](https://huggingface.co/blog/ethics-soc-7) provides a summary of how LLMs can become agents and what some of the implications of that are.
- The Google / Gemma API docs ([Function Calling with Gemma](https://ai.google.dev/gemma/docs/capabilities/function-calling)) provide some examples of how we can actually use some of these functionalities.
- What's "prompt injection"? A new kind of vulnerability—skim a few of the [blog posts about this](https://simonwillison.net/tags/prompt-injection/). Pay attention to how LLM-based agents are uniquely vulnerable to it.

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-04-06" %}}
- Easter Monday

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-04-08" %}}
- Reminder: [Discussion 376.2: Training Data as Stewardship](/units/10arch/discussion/) posts due today (replies due Fri Apr 11)
- Tech update: [Anthropic Glasswing](https://www.anthropic.com/glasswing)
- Quiz 1: Looking for evidence of learning about:
  - [OG-LLM-Tokenization](objective)
  - [TM-LLM-Generation](objective)
  - [OG-SelfSupervised](objective)
  - [TM-LLM-Embeddings](objective)
  - [TM-SelfAttention](objective) *(basic intuition only)*
- If you finish early:
  - {{% notebook name="Self-Attention By Hand (in Code)" nbname="u10s1-attention-by-hand.ipynb" %}}
  - Work on the lab we'll be doing next class. See the slides:
  - Slides: [376 Lab 3: Implementing Self-Attention](/slides/w10-lab.html)

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-04-10" %}}
- Handout: [Self-Attention Shapes](/handouts/2026_04_10.pdf)
  - Class exercise: given model dimensions, what are the shapes of Q, K, V, attention matrix?
  - Reference: the [Qwen 2.5 tech report](https://arxiv.org/abs/2407.10671) and [model page](https://huggingface.co/Qwen/Qwen2.5-0.5B?show_file_info=model.safetensors)
- And do: {{% notebook name="Self-Attention By Hand (in Code)" nbname="u10s1-attention-by-hand.ipynb" %}}
- Lab 3 ([Self-Attention in Code](/units/10arch/lab/))
  - Slides: [376 Lab 3: Implementing Self-Attention](/slides/w10-lab.html)
  - Implementing self-attention (trace through transformer implementation)
  - Continue u10n1-implement-transformer: Self-Attention section
- Project encouragements
  - Be the ones who can *measure* AI performance
- Motivational examples:
  - [Claude Plays Pokemon](https://www.twitch.tv/claudeplayspokemon)
  - [Capture-the-Flag traces](https://docent.transluce.org/picoCTF)
  - [Reinforcement Learning for Long-Horizon Interactive LLM Agents | Abstract](https://arxiv.org/abs/2502.01600)

Reference:

- {{% notebook name="Demo of Logits and Embeddings from a Language Model" nbname="u09n0-logits-demo.ipynb" %}}

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 5: Agents and Tool Use

{{% calendar-week-header %}}
How can we turn LLMs into agents that interact with the world? This week we'll explore tool use, function calling, and context engineering for multi-turn agents.

{{% details summary="Resources" %}}
If you're feeling fuzzy about any of the concepts we've covered so far, I recommend going back to these resources:

- Videos / articles
  - [3Blue1Brown - Visualizing Attention, a Transformer's Heart | Chapter 6, Deep Learning](https://www.3blue1brown.com/lessons/attention)
  - [3Blue1Brown - How might LLMs store facts | Chapter 7, Deep Learning](https://www.3blue1brown.com/lessons/mlp)
- Interactive
  - [Transformer Explainer](https://poloclub.github.io/transformer-explainer/)
  - [LLM Visualization](https://bbycroft.net/llm): an interactive article, take your time to walk through it over several sessions.
  - [Softmax and Cross-Entropy](https://observablehq.com/@kcarnold/softmax)
- Notebooks
  - Notebook: {{% notebook name="Demo of Logits and Embeddings from a Language Model" nbname="u09n0-logits-demo.ipynb" %}}

Supplemental resources:

- [Tracing the thoughts of a large language model \ Anthropic](https://www.anthropic.com/research/tracing-thoughts-language-model)
- [OpenAI Tokenizer](https://platform.openai.com/tokenizer)
- [Zero to Hero](https://karpathy.ai/zero-to-hero.html) part 6: [Let's build GPT: from scratch, in code, spelled out. - YouTube](https://www.youtube.com/watch?v=kCc8FmEb1nY) (go back to [prior parts](https://karpathy.ai/zero-to-hero.html) if you need to)

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-04-13" %}}
- Assign [Discussion 376.3: When Agents Go Wrong](/units/11generation/discussion/) (posts due Fri Apr 17, replies due Mon Apr 20)
- Review quiz 1 (brief, ~10 min)
- Tool use / function calling — live demo with API
  - See Tools in [LM-Internals](/lm-internals.html)
    - Example: "Location: Grand Rapids, MI, 49546; Do I need an umbrella today?"
  - Example flow: call API with tool definition → model returns tool_use → execute → feed result back
  - Reference: [Qwen2.5 chat template](https://huggingface.co/Qwen/Qwen2.5-0.5B?chat_template=default)
- Feedback / check-in activity

We ended up referring to:

- [LLM Architecture Gallery](https://sebastianraschka.com/llm-architecture-gallery/)

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-04-15" %}}
- Note: revised [Project description](/project) up, feedback welcome.
- Self-Attention Shapes handout debrief (~20 min): pairs fill/correct the table for Qwen2.5-0.5B; whole-class walk-through input → Q/K/V → scores → weights → concatenated output. Hits [TM-SelfAttention](objective) *(deeper)* and [TM-TransformerDataFlow](objective).
  - Reference: the [Qwen 2.5 tech report](https://arxiv.org/abs/2407.10671) and [model page](https://huggingface.co/Qwen/Qwen2.5-0.5B?show_file_info=model.safetensors)
- [Lab 376.4](/units/11generation/lab/) kickoff (~50 min): {{% notebook name="LLM Prompting and Tool Use" nbname="u11n1-prompt-engineering.ipynb" %}}
  - Using Qwen2.5-0.5B (base) vs Qwen2.5-0.5B-Instruct — same model students saw in u08n1 and on the Apr 10 handout.
  - Focus on: few-shot, chain-of-thought, chat-templating, RAG, tool-use. Base-vs-tuned contrast is load-bearing for [OG-LLM-Train](objective).
- Take-home: complete through the Tool Use section (stop before "⚠️ Friday material") + write answers for those sections. Posts for [Discussion 376.3](/units/11generation/discussion/) due Fri.

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-04-17" %}}
- Review earlier handout on generation loop
  - Handout: [Token and Context Embeddings, and Sampling Algorithm](/handouts/2026_03_27.pdf)
- Hand back Quiz 1
- Logistics:
  - [Discussion 376.3: When Agents Go Wrong](/units/11generation/discussion/) posts due today (replies due Mon Apr 20)
  - [Project](/project/) Milestone 2 ("What Success Looks Like") due "soon" (Monday ideally, but flexible)
  - walkthroughs: probably best after next week.
- Prompting and agents:
  - Define these terms: context engineering, few-shot, retrieval-augmented generation (RAG), reasoning models, tool use, agent loop
  - Agent failures: incorrect tool use, prompt injection ([lethal trifecta](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/))
  - Why is LLM eval harder than evaluating a classifier?
- Reference: [Slides w11](/slides/w11-prompting.html)
- Debrief Wed + walkthrough the unfolded agent loop cells (~10 min): cells show build → template → generate → parse → dispatch → append → loop.
- Happy-case agent task: wamerican word count (~15 min): run `run_agent` with `run_bash` on install + count task; observe multi-step execution.
- Scenario 1 — Prompt injection (~15 min): model summarizes a file planted with malicious instructions; observe exfiltration of fake credentials. [OG-LLM-ContextAndTools](objective)
- Scenario 2 — Helpful cleanup (~10 min): innocent-sounding request that may trash the runtime. Contrast with Scenario 1.
- Context engineering takeaways + Quiz 2 preview (~15 min): anchor to [OG-LLM-ContextAndTools](objective); map observed failures to attack-surface criteria; objective-by-objective map to quiz prep artifacts.

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 6: Training Pipeline and Projects

{{% calendar-week-header %}}
How are modern LLMs trained? This week covers the training pipeline (pretraining → SFT → RLHF) and Quiz 2.

{{% details summary="Objectives" %}}
- [OG-LLM-Train](objective)
- [OG-Theory-Feedback](objective)

{{% /details %}}
{{% details summary="Key Questions" %}}
- What are the three main stages of training a modern dialogue LLM, and what does each stage accomplish?
- Where does human judgment enter the training process at each stage?
- What is a reward signal, and why is designing one hard?
- What is reward hacking, and how can you mitigate it?

{{% /details %}}
{{% details summary="Readings" %}}
- the rest of the ethics chapter from [Understanding Deep Learning](https://udlbook.github.io/udlbook/)
- [Scheming reasoning evaluations — Apollo Research](https://www.apolloresearch.ai/research/scheming-reasoning-evaluations)
- [Stanford 2025 AI Index Report](https://hai.stanford.edu/ai-index/2025-ai-index-report)
- [Artificial intelligence learns to reason _ Science](https://www.science.org/doi/10.1126/science.adw5211)
- [Turning Employees Into AI Janitors - by Cassie Kozyrkov](https://decision.substack.com/p/turning-employees-into-ai-janitors)
- [Technical Report: Prompt Engineering is Complicated and Contingent - Wharton AI & Analytics Initiative](https://ai-analytics.wharton.upenn.edu/generative-ai-labs/research-and-technical-reports/tech-report-prompt-engineering-is-complicated-and-contingent/)
- [22365_3_Prompt Engineering_v7](https://drive.google.com/file/d/1AbaBYbEa_EbPelsT40-vj64L-2IwUJHy/view)

Another nice reading (about training data), but the server seems down: [Models All the Way Down](https://knowingmachines.org/models-all-the-way) until Part 3

- [An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale | Abstract](https://arxiv.org/abs/2010.11929)

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-04-20" %}}
- Assign [Discussion 376.4: Fans and Skeptics](/units/13multimodal/discussion/) (posts due Mon Apr 27, replies due Thu Apr 30; we'll share in class W7 Fri)
- Guest lecture from Prof Santos (Ken is traveling)

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-04-22" %}}
- Quiz 2 (proctored — Ken traveling): Looking for evidence of learning about:
  - [OG-LLM-Prompting](objective)
  - [OG-LLM-Eval](objective)
  - [TM-SelfAttention](objective) *(deeper)*
  - [TM-TransformerDataFlow](objective)

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-04-24" %}}
- Tech Update
- Can you do [this lab](https://cs.calvin.edu/courses/cs/108/26sp/units/13/lab/)?
- Training Pipeline and Reward Design:
  - [Slides](/slides/w13.html)
  - More details: [rlhfbook.com Ch. 6](https://rlhfbook.com/c/06-policy-gradients)
- Handout: [Training from Rollouts](/handouts/2026_04_24.pdf)
  - Addresses [OG-LLM-Train](objective), [OG-Theory-Feedback](objective), and (somewhat) [Overall-LLM-Failures](objective)
- [How LLMs work](https://ynarwal.github.io/how-llms-work/) interactive
  - Also see the [softmax/cross-entropy interactive](https://observablehq.com/@kcarnold/softmax)

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 7

{{% calendar-week-header %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-04-27" %}}
Course wrap-up, Part 1 — and Quiz 3 prep.

- Quiz 2 review
- Slides: [CS 376 Review, Part 1](/slides/wrapup-376.html)
  - From 375 to 376: one tunable machine, two stacked games
  - Inside the LLM: [OG-LLM-Tokenization](objective), [TM-LLM-Embeddings](objective), [TM-SelfAttention](objective), [TM-TransformerDataFlow](objective), [TM-LLM-Generation](objective)
  - Training the LLM: [OG-LLM-Train](objective), [OG-SelfSupervised](objective), [OG-Theory-Feedback](objective)
  - Using the LLM: [OG-LLM-ContextAndTools](objective)
  - Trusting the LLM: [OG-LLM-Eval](objective), then a discussion of when evaluation lies — Goodhart's Law, the layers problem, horror stories — [Overall-LLM-Failures](objective)
  - One more for color: [An AI agent deleted our production database. The agent's confession is below](https://x.com/lifeof_jer/status/2048103471019434248) [(hn)](https://news.ycombinator.com/item?id=47911524)
- Handout: [Objectives Reflection](/handouts/2026_04_27.pdf)

<!-- Pivoted from a fairness-as-eval handout to a wrap-up-style review mirroring wrapup-375.qmd. The discussion of when evaluation lies is the planned student-driven break in an otherwise teacher-centered review session — trigger is the OG-LLM-Eval slide. Handout was generated via src/gen_objectives_handout.py. -->

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-04-29" %}}
- Reminder about Discussion 376.4: Fans and Skeptics (posts due Mon Apr 27, replies due Thu Apr 30; we'll share in class on Fri)
- Review Handout from last week on training and reward design
  - Handout: [Training from Rollouts](/handouts/2026_04_24.pdf)
- Quiz 3
  - [OG-LLM-Eval](objective)
  - [OG-LLM-ContextAndTools](objective)
  - [Overall-LLM-Failures](objective)
  - [OG-LLM-Train](objective)
  - possibly also: OG-LLM-Tokenization, TM-LLM-Embeddings, TM-TransformerDataFlow, TM-SelfAttention

<!-- Interpretability dropped as its own topic; Monday's eval-critique surfaces the relevant concerns. The Explainable-and-Usable-AI slides remain as optional reference for curious students. -->

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-05-01" %}}
Course wrap-up, Part 2 — synthesis.

- [Overall-Impact](objective): stakeholders, distribution mismatch, feedback loops, recourse
- Discussion 376.4 (Fans and Skeptics) sharing — compare with the [Pew Research survey](https://www.pewresearch.org/internet/2025/04/03/how-the-us-public-and-ai-experts-view-artificial-intelligence/)
- Christian framing ([Overall-PhilNarrative](objective) / [Overall-Faith](objective)): stewardship, shalom, imago Dei, what it means for the machine to imitate us
- Closing commission

<!-- Part 2 deck still to draft — can extend wrapup-376.qmd or split into wrapup-376-pt2.qmd. Existing material to draw from: w13-Fairness and Wrap-Up.pdf, 2025_05_02 wrap-up handout (adapt for 26sp). -->

Final Discussion topics

- Personal Impacts
  - How AI has impacted my life in the past few years. For better? For worse?
  - How AI has impacted the lives of people unlike me.
  - How AI might impact our lives in the next 5 years.
- Development
  - Something useful or cool that has recently become possible thanks to AI.
  - What are some things that AI systems are already better than humans at?
  - What are some things that humans are still much better at than AI systems?
- Broader impacts
  - Is AI good for the environment? Bad?
  - Is AI good for society? Bad?
  - Is AI good for human creativity? is it bad?
- Christian perspective
  - Something that Christians should consider as people who *consume* AI-powered products
  - ...As people who *use* AI in their organizations
  - ...as people who *develop* AI?

{{% /calendar-day %}}


</div>


Additional items:

- Tuesday, May 6, 9am: Final Project Presentations during our class's [final exam time slot](https://calvin.edu/registrars-office/exam-schedule)
- Slides: [A Final Commission](/slides/w14-conclusion.html)

