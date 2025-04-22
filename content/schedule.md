---
title: "Schedule - CS376"
revised: 2025
toc: true
---

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
- Define *perplexity*, and describe how it relates to log-likelihood and cross-entropy (and the general concept of partial credit and/or surprise in classifiers)


(next year: add a question about how to use a language model as the backend of a chatbot)

{{% /details %}}
{{% details summary="Objectives" %}}
This week will address course objectives on LM-SelfSupervised, MS-LLM-Tokenization, and MS-LLM-TokenizationImpact.

- Explain what generative modeling is and its uses
- Describe the high-level idea of three basic approaches to generative models: autoregressive, latent variable, and diffusion
- Describe the inputs and outputs of an autoregressive language model
  - tokens -> embeddings
  - next-token conditional probability distribution

We will also discuss how a language model can be used for a chatbot. (TODO: this needs a course objective and a link to some Chat Templating documentation)

{{% /details %}}
{{% details summary="Prep and Readings" %}}
Before starting this unit, you should already know the basics of supervised learning. Specifically, you should be comfortable with training a fully-connected neural network on a classification task.

I recommend the following readings (in Perusall):

- [Large Language Models explained briefly (3blue1brown)](https://www.youtube.com/watch?v=LPZh9BOjkQs&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi&index=5)
- the Hugging Face Transformers course, chapter 1:
    - 1.2 [Natural Language Processing - Hugging Face NLP Course](https://huggingface.co/learn/nlp-course/en/chapter1/2)
    - 1.3 [Transformers, what can they do? - Hugging Face NLP Course](https://huggingface.co/learn/nlp-course/en/chapter1/3)
    - 1.4 [How do Transformers work? - Hugging Face NLP Course](https://huggingface.co/learn/nlp-course/en/chapter1/4)
- [Artificial Intelligence Then and Now – Communications of the ACM](https://cacm.acm.org/opinion/artificial-intelligence-then-and-now/)
    
If you need some additional background, I recommend [Understanding Deep Learning](https://udlbook.github.io/udlbook/)

{{% /details %}}
{{% details summary="Extension Opportunities" %}}
- Activity: [Optional Extension: Token Efficiency Analysis](/units/08generative-intro/extension-tokenization)

{{% /details %}}
{{% details summary="Notes" %}}
### Language Models

- Language models (LMs) are trained to predict the next word in a document.
- Next-word prediction = classification
  - Input: document up to the current word
  - Output: probability distribution over all possible words
- Training set: a huge set of documents from the Internet
- Trained to minimize "surprise" (cross-entropy loss)
  - Model predicts a distribution P(word | document so far)
  - Surprise = how much probability mass the model gave to the actual next word
    - Low surprise = it made a really good guess
    - High surprise = its guess was bad (or perhaps the model was rightly unsure)
- Mathematically:
  - the model assigns a probability distribution to all possible documents.
  - P(document) = P(word 1) * P(word 2 | word 1) * P(word 3 | word 1, word 2) * ...
  - These probabilities would be tiny, so we take the log:
    - log P(document) = log P(word 1) + log P(word 2 | word 1) + log P(word 3 | word 1, word 2) + ...
    - The log of a product is the sum of the logs
    - This is the log-likelihood of the document under the model. The negative of this (NLL for negative log-likelihood) is also called the cross-entropy loss.
    - Dividing this by the number of words in the document gives the average log-likelihood per word, or average cross-entropy loss per word
  - The model is a function that outputs log P(word | document so far) for each word in the vocabulary
    - Typically the model outputs *logits*, which are then passed through a softmax to get probabilities.
  - The model is trained to minimize cross-entropy loss by stochastic gradient descent on a training set of documents.


### Text as Input

How to represent text as input to a neural network?

- Input: a sequence of token ids. Output: a probability distribution over all possible tokens.
- Token: a single unit. Can be a word, a character, a subword, etc.
- Classical approaches:
  - Character-level language models
    - Input: a sequence of characters
    - Output: probability distribution over all possible characters
  - Word-level language models
    - Input: a sequence of words
    - Output: probability distribution over all possible words
- Pros and cons
  - Character-level models:
    - Pros: robust to spelling variations or unknown words
    - Cons: each word requires many tokens, so requires more computation. Difficult to learn long-range dependencies (many tokens away, info is spread over many tokens). Internals of the model are hard to interpret.
  - Word-level models:
    - Pros: each word requires only one token, so requires less computation. Relationships between words are easier to learn. Internals of the model are easier to interpret.
    - Cons:
      - no sharing between obviously related words (e.g., "dog" and "dogs" are completely separate tokens; can only learn their relationship by example)
      - any word that doesn't appear in the training set is completely unknown (even if its spelling is similar to a word that does appear in the training set, e.g., "dog" vs. "dogg")
- Modern approach: sub-word tokenization (e.g., Byte-Pair Encoding, SentencePiece, etc.)
  - Common words are represented by a single token
  - Less common words are represented by a sequence of tokens
    - e.g., "dogg" might be represented by "dog" + "##g" (where "##" is a special token that indicates a sub-word)
    - Alternative to marking sub-words with "##" is to include the leading space in the first token of the sub-word sequence (e.g., "dogg" might be represented by " dog" + "g")
- Effects of tokenizer choice: Most modern models use some sort of sub-word tokenization, but even so they differ by tokenization strategy (e.g., does each digit get its own token?) and vocabulary size (e.g., how many tokens are used to represent the vocabulary). This affects:
  - how much memory is required to store all of the token embeddings
  - how much computation is required to do dot products with all of them (for computing logits)
  - How efficiently the model can handle morphological variations and generalize across languages
  - The total number of tokens that a model needs to process and generate in the course of working with a given text

### Sampling from a Language Model

- How to generate text from a language model?
  - Start with a prompt (e.g., "Every morning I wake up and")
  - Use the model to predict the next word
  - Use the predicted distribution to choose the next word
  - Keep adding words until the end-of-text token is generated
- This corresponds to the left-to-right factorization of the joint probability distribution over documents:
  - P(document) = P(word 1) * P(word 2 | word 1) * P(word 3 | word 1, word 2) * ...
  - To sample from that, we can start by sampling P(word 1) from the model, then sample P(word 2 | word 1) from the model, and so on.
  - At each step, we're sampling from a conditional distribution
  - That distribution only depends on the words that came before it
  - So we can sample from it independently of the words that come after it
- Implications:
  - the model never "looks ahead" to see what words come after the current word.
  - We can get the model to "rationalize" a statement by including that statement as part of its prompt. The model's "memory" is externalized in the words it's already generated, so we can "edit" that memory by changing the document so far.
  - We could have factored the joint distribution in a different way, depending on what we want to do. For example, some models are trained to "Fill In the Middle" (FIM), where the model is given context after the section to generate as well. But in practice this is actually implemented by transforming the input into a left-to-right sequence with special marker tokens for the section "<before>", "<after>", and "<to fill in>".
  - We could also train the model to "reconstruct" any given token from the tokens around it; this is the idea of masked language modeling (MLM) used in models like BERT. It turns out that this allows the model to "cheat" a lot, so tweaks are needed to make it work for generation tasks. But it's reasonably good at learning representations (embeddings) of whole sequences, so it's sometimes used in vector databases.
- Temperature
  - The model's predictions are a probability distribution over all possible words
  - We can control how much randomness is in the distribution by changing the temperature
  - Can be used to control the "creativity" or "diversity" of the model's output
    - Higher temperature = more randomness. Extreme: infinite temperature = uniform distribution over all words
    - Lower temperature = less randomness. Extreme: 0 temperature = always choose the most likely word
  - Computed by dividing the logits by the temperature before passing them through the softmax
  - Temperature = 1.0 means no change to the logits before sampling
  - In practice, it's a balance between predictability and interestingness
    - Too high temperature = output isn't dependable. With some probability, the model will output something highly unusual.
    - Too low temperature = output is unusually dull. Human communication rarely chooses the single most likely thing (otherwise why would we bother communicating?), so always picking the most likely word yields text that is unusually flat.
  - Other ways to control the randomness of the output:
    - Nucleus sampling (top-p): instead of sampling from the whole distribution, sample from the smallest set of words that add up to some threshold probability (e.g., 90% of the probability mass)
    - Top-k sampling: sample from the top k most likely words

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2025-03-17" %}}
- Slides: [376 Unit 1: Generative Modeling Introduction](/slides/w08-generative.html)
- Topics:
    - Intro
    - Logistics for 376 vs 375
    - Projects
    - Intro to Generative Modeling
- Handout: [What do you already know about generative modeling?](/handouts/2025_03_17.pdf)
- Activity: [Exploring Language Models](/units/08generative-intro/exploring-lm)
- Resources:
    - [OpenAI Tokenizer](https://platform.openai.com/tokenizer)

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2025-03-19" %}}
- Slides: [376 Unit 1: Generative Modeling Introduction](/slides/w08-generative.html)
  - Scripture: Proverbs
  - Readings, Moodle participation activity
  - Ways of Setting Up Generative Modeling (Autoregressive, Latent Variable, Diffusion)
    - Autoregressive Language Models as Classifiers
    - Perplexity as cumulative surprise
    - Implications of Autoregressive Generation
  - Text <-> Numbers
- Handout: [Review tokenization and chat docs; next-token prediction](/handouts/2025_03_19.pdf)
- Activity: [Generation Activity](/units/08generative-intro/generation-handout)
    - Next-Token Predictions Activity

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2025-03-21" %}}
- Handout: [GenAI problem setup, LLM as next-token classifier](/handouts/2025_03_21.pdf)
- Slides: [376 Unit 1: Generative Modeling Introduction](/slides/w08-generative.html)
- Activity: [CS 376 Lab 1: Tokenization](/units/08generative-intro/lab)

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 2: Language Modeling

{{% calendar-week-header %}}
This week start to take off the covers of NLP models, just like we took off the covers of image models in CS 375. In particular, we'll get our first taste of the Transformer model, the most important model in machine learning today.

Advising is this week, so we won't get to a lot of new content.

{{% details summary="Key Questions" %}}
- What is a token embedding? What is an output (or context) embedding? How do these relate to the input and output of a language model?
- How does a causal language model use embeddings of contexts (e.g., sentence prefixes)?
- How can we use a language model to generate text?

{{% /details %}}
{{% details summary="Objectives" %}}
This week we start work on these objectives:

- I can identify the shapes of data flowing through a Transformer-style language model. [NC-TransformerDataFlow]
- I can identify various types of embeddings (tokens, hidden states, output, key, and query) in a language model and explain their purpose. [NC-Embeddings]

{{% /details %}}
{{% details summary="Notes" %}}
- token and output embeddings work almost exactly like https://cs.calvin.edu/courses/cs/375/cur/notebooks/u07n1-image-embeddings.html

### Q&A

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
{{% calendar-day dow="Monday" date="2025-03-24" %}}
Logistics:

- Scripture: [Jeremiah 17:7-8](https://www.biblegateway.com/passage/?search=Jeremiah%2017%3A7-8&version=NIV&interface=print)
- Reminders:
    - Complete "Reflections Week 1"
    - Discussion 1
- [Highlight-Edits example](https://huggingface.co/spaces/CalvinU/writing-prototypes)

Tokenization:

- [How many 'r's in 'strawberry'?](https://www.google.com/search?client=firefox-b-1-d&sca_esv=3c1b2768c64ab720&sxsrf=AHTn8zqr1yqtAe04PcmPoM3OBrPIoS64Lw:1742827820765&q=how+many+r+in+strawberry&udm=2&fbs=ABzOT_CWdhQLP1FcmU5B0fn3xuWpA-dk4wpBWOGsoR7DG5zJBsxayPSIAqObp_AgjkUGqenLclubdwP4zrQWfEJDEVVFVXswA8wQATANG0VCCiWAMmuVVrQFXoYq-dEjWCUw79bWt_4W_Qj_zS4V-wsygQmRTZOioV_ypugMcmPraR5llR8mvXy0mnMZr0gSbcsx14gEjIdWHa4xM4x-LfMTH6rdIOS-0A&sa=X&ved=2ahUKEwik-KTJ-6KMAxXuHTQIHcAfJDEQtKgLegQIFRAB&biw=1728&bih=966&dpr=1#vhid=dSxCuYIjQ5n3LM&vssid=mosaic)
- [stable diffusion can't spell](https://www.google.com/search?q=stable+diffusion+can%27t+spell&client=firefox-b-1-d&sca_esv=3c1b2768c64ab720&udm=2&biw=1728&bih=966&sxsrf=AHTn8zoDf4_bOZNuVgi_y-1gxQapxCsItQ%3A1742827834099&ei=OnHhZ8fdBfTG0PEPiOyUgAo&ved=0ahUKEwjH4tLP-6KMAxV0IzQIHQg2BaAQ4dUDCBQ&uact=5&oq=stable+diffusion+can%27t+spell&gs_lp=EgNpbWciHHN0YWJsZSBkaWZmdXNpb24gY2FuJ3Qgc3BlbGxIzSVQ0QdY6SNwBXgAkAECmAFZoAHZDqoBAjMwuAEDyAEA-AEBmAIdoAKhDMICChAAGIAEGEMYigXCAgYQABgHGB7CAggQABgHGAoYHsICBRAAGIAEwgIIEAAYgAQYsQPCAg0QABiABBixAxhDGIoFwgILEAAYgAQYsQMYigXCAgsQABiABBixAxiDAcICDhAAGIAEGLEDGIMBGIoFwgIHEAAYgAQYCsICChAAGIAEGLEDGArCAgQQABgewgIGEAAYChgewgIGEAAYCBgewgIIEAAYCBgKGB6YAwCIBgGSBwIyOaAHm50BsgcCMjS4B4AM&sclient=img#vhid=0imS1LbUWQKuKM&vssid=mosaic)


Activity: [Lab 376.2: Logits in Causal Language Models](/units/09lm/lab)

Supplemental material: [list comprehensions in Python](https://cs.calvin.edu/courses/cs/106/24fa/units/14bonus/slides.html#/list-comprehensions)

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2025-03-26" %}}
- Advising




{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2025-03-28" %}}
- Project Inspirations
  - An example related to our topic today: [How to make a racist AI without really trying | ConceptNet blog](https://concepts.arborelia.net/posts/2017/how-to-make-a-racist-ai-without-really-trying/)
  - An idea: use a pretrained autoregressive model as if it were a diffusion LM by simply instructing it to "fill in the blanks" in a document (and then giving the blanked document as input)
- Lab review
  - For reference:
  - Notebook: {{% notebook name="Probe an Image Classifier" nbname="u07n1-image-embeddings.ipynb" %}}
- Handout: [Token and Context Embeddings](/handouts/2025_03_28.pdf)
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
- [NC-SelfAttention](objective)
- [NC-Architectures](objective)
- [NC-TransformerDataFlow](objective)

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
This week's reading includes a brand new result from Anthropic that looks really helpful for getting an accurate intuition about what's going on inside an LLM. We're looking at the high-level overview article this week; if people are interested we can dig into the technical report in a future week.

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

News (in Perusall library, not officially assigned)

- [Music publishers ‘remain very confident’ of winning Anthropic case and will ‘vigorously pursue’ monetary damages - Music Business Worldwide](https://www.musicbusinessworldwide.com/music-publishers-remain-very-confident-of-winning-anthropic-case-and-will-vigorously-pursue-monetary-damages1/)
- [DOGE Plan to Push AI Across the US Federal Government is Wildly Dangerous | TechPolicy.Press](https://www.techpolicy.press/doge-plan-to-push-ai-across-the-us-federal-government-is-wildly-dangerous/)

{{% /details %}}
{{% details summary="Supplemental Resources" %}}
- A video course on [How Transformer LLMs Work - DeepLearning.AI](https://learn.deeplearning.ai/courses/how-transformer-llms-work/lesson/nfshb/introduction)
- Wanna code it? [Zero to Hero](https://karpathy.ai/zero-to-hero.html) part 6: [Let's build GPT: from scratch, in code, spelled out. - YouTube](https://www.youtube.com/watch?v=kCc8FmEb1nY) (go back to [prior parts](https://karpathy.ai/zero-to-hero.html) if you need to)
- [HandsOnLLM/Hands-On-Large-Language-Models: Official code repo for the O'Reilly Book - "Hands-On Large Language Models"](https://github.com/HandsOnLLM/Hands-On-Large-Language-Models)

{{% /details %}}
{{% details summary="Q&A" %}}
> Is there a limit to how far back a transformer can look? And how are they improving it? For example, in a chatbot with more context, you can feel that it is getting dumber.

"how far back a transformer can look" = its "context window". Things that limit that:

1. the architecture. if position embeds are absolute (not, say, RoPE), then we need to set a limit before we even start training.
2. computation. Plain self-attention is quadratic in squence length. So long attention takes way more computation time. This has seen lots of effort to optimize recently.
3. Training. Gotta actually give the models examples of documents / conversations / etc. where long-range attention is needed, otherwise it won't learn it.

> How does increased communication [via self-attention] actually translate to better token generation?

Consider the case of asking an LLM to fix up a paragraph that you wrote. It needs to basically copy what you gave as input, but with some edits / changes at some places. Self-attention lets the network basically keep a running pointer to where you are in the input, grab what you said next, and repeat that or something similar in the output. A recurrent network (like LSTM), in contrast, would somehow have to encode your entire input into a single vector, and then decode that into the output, which is really challenging to learn to do reliably.

> How else to improve transformers, besides more training and more heads / layers / dimensions?

There's so many little tweaks that people do (read the tech report of any new model release). Common things people play with are how to encode position (RoPE is big now), playing with how keys/queries/values mix and match (Grouped Query Attention etc.), and the data, loss functions, etc. (e.g., reinforcement learning from various kinds of rewards).

> What does the [Anthropic article](https://www.anthropic.com/research/tracing-thoughts-language-model) mean by "Claude wasn't designed as a calculator—it was trained on text, not equipped with mathematical algorithms"?

The Transformer architecture is hugely inefficient and unreliable if all you want to do is addition or multiplication. But it had to learn to do that anyway, even with unreliable building blocks, because being able to add and multiply make the Internet a bit less surprising.

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2025-03-31" %}}
- Slides: [Neural Architectures](/slides/w10-nn-arch.html)
  - Intro
  - Review
- Review handout activity from Friday
  - How does the Gemma model actually represent these tokens and contexts? (See logits-demo notebook)
  - Let's write the sampling algorithm together.
- Handout: [Self-Attention By Hand](/handouts/2025_03_31.pdf)

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2025-04-02" %}}
- Review
  - Go over key questions from past 2 weeks
  - Reminder: Quiz 1 Friday
  - Exercises posted
- [Transformer Explainer](https://poloclub.github.io/transformer-explainer/)
- Slides: [Neural Architectures](/slides/w10-nn-arch.html)
  - Fixed wiring: Feed-forward (MLP)
  - Current sample wired to previous sample:
    - Recurrent Networks ([Elman](https://en.wikipedia.org/wiki/Recurrent_neural_network#Architectures); [LSTM and GRU](http://colah.github.io/posts/2015-08-Understanding-LSTMs/))
  - Current sample wired to surrounding samples: Convolutional Networks (CNN)
    - What convolution does to an image: [Image Kernels explained visually](https://setosa.io/ev/image-kernels/)
    - How to use convolutions in a neural network: [CS231n Convolutional Neural Networks for Visual Recognition](https://cs231n.github.io/convolutional-networks/)
    - What they learn: [Feature Visualization](https://distill.pub/2017/feature-visualization/)
  - Wiring computed dynamically based on "self-attention": Transformer
- Tricks
  - Residual Connections
  - Dropout
- Review: Self-Attention = conditional information flow
  - Software: describe the wiring, then what flows through the wires.
  - Hardware: compute queries, keys, and values, then compute the attention matrix, then compute the output.
- For Friday, please start working on:
  - Activity: [Lab 376.3](/units/10arch/lab)
- Notebook: {{% notebook name="Demo of Logits and Embeddings from a Language Model" nbname="u09n0-logits-demo.ipynb" %}}
- Notebook: {{% notebook name="Translation as Language Modeling" nbname="u09n2-decoding.ipynb" %}}

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2025-04-04" %}}
- Activity: [Lab 376.3](/units/10arch/lab)
  - Slides: [376 Lab 3: Implementing Self-Attention](/slides/w10-lab.html)
- Quiz 1: Looking for evidence of learning about:
  - [MS-LLM-Tokenization](objective)
  - [MS-LLM-Generation](objective)
  - [LM-SelfSupervised](objective)
  - [NC-Embeddings](objective)
  - [NC-SelfAttention](objective) *(basic intuition only)*

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

- [MS-LLM-API](objective)
- [MS-LLM-Prompting](objective)
- [MS-LLM-Advanced](objective)
- [MS-LLM-Train](objective)

Review objectives:

- [MS-LLM-Tokenization](objective)
- [MS-LLM-TokenizationImpact](objective)
- [MS-LLM-Generation](objective)

Extension objectives:

- [MS-LLM-Compute](objective)

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
{{% calendar-day dow="Monday" date="2025-04-07" %}}
- Review quiz 1
  - Solutions available for those who have completed it
  - Grading by objectives
    - Revised the MS-LLM-API objective to match what the quiz assessed. (question 4 also addressed it, forgot to mark that)
- Handout: [Self-Attention Shapes](/handouts/2025_04_07.pdf)
- Review lab 3
- Project encouragements
  - Be the ones who can *measure* AI performance



Reference:

- {{% notebook name="Demo of Logits and Embeddings from a Language Model" nbname="u09n0-logits-demo.ipynb" %}}
- {{% notebook name="Translation as Language Modeling" nbname="u09n2-decoding.ipynb" %}}

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2025-04-09" %}}
- Review attention via the [Transformer Explainer](https://poloclub.github.io/transformer-explainer/)
- Motivational examples:
  - [Claude Plays Pokemon](https://www.twitch.tv/claudeplayspokemon)
  - [Capture-the-Flag traces](https://docent.transluce.org/picoCTF)
  - [Reinforcement Learning for Long-Horizon Interactive LLM Agents | Abstract](https://arxiv.org/abs/2502.01600)
- Activity: [Lab 376.4: Dialogue Agents, Prompt Engineering, Retrieval-Augmented Generation, and Tool Use](/units/11generation/lab)
  - Prompt Engineering
  - Instruction Tuning
  - Retrieval-Augmented Generation

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2025-04-11" %}}
- Slides: [Generation by Prompting](/slides/w11-prompting.html)
- Quiz 2: An opportunity to demonstrate your understanding of some of the following objectives:
  - [MS-LLM-Generation](objective)
  - [MS-LLM-API](objective)
  - [LM-SelfSupervised](objective)
  - [NC-Embeddings](objective)
  - [NC-SelfAttention](objective)
  - [NC-TransformerDataFlow](objective)


Note: I dropped the intro to Streamlit for time reasons, but I highly recommend you check it out. It's a great way to make your models accessible to others. The [next-token demo](https://huggingface.co/spaces/kcarnold/next-token) that we used in Week 2 was a Streamlit app; click the [Files](https://huggingface.co/spaces/kcarnold/next-token/tree/main) tab on the Hugging Face Space to see the code.

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 5: Review

{{% calendar-week-header %}}
Since this is a short week, we'll slow down to review and reinforce (1) how Transformers work inside and (2) how we can use them to make conversational agents that can interact with the world.

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
{{% calendar-day dow="Monday" date="2025-04-14" %}}
- Quiz 2 review
- Feedback / checkin activity
- Q&A

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2025-04-16" %}}
- Results of feedback activity:
  - Biggest hope (by far): good projects
  - Biggest things we want to learn: *How to make a (semi-autonomous) agent that improves its behavior from feedback*
  - Biggest thing to review *how self-attention works*
- Project Work Time!
  - Deliverable: what's your project? What's success look like (sketch an example)? What are two next steps that you can take to make progress?
- Review (see [Summary](/units/12review/))
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

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2025-04-18" %}}
- Good Friday

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 6: Multimodal Models and Diffusion

{{% calendar-week-header %}}
What if we want to have AI conversations that include images or audio? -- both as input and output?

This week we'll look at models that can process (and sometimes generate) multiple types of data at once, such as images and text. We'll also look at diffusion modeling, a powerful generative modeling technique.

{{% details summary="Objectives" %}}
By the end of this week you should be able to:

- Describe how autoregressive generation works
- Describe how generative adversarial networks work
- Describe how diffusion models work


- Compare and contrast the process and results of generating sequences using three different algorithms: greedy generation, sampling, and beam search.
- Explain the concept of a *generator network*.
- Explain how a Generative Adversarial Network is trained.

{{% /details %}}
{{% details summary="Key Questions" %}}
- How is noise useful for diffusion models for image generation?
- Why does diffusion require multiple time steps?

{{% /details %}}
{{% details summary="Terms" %}}
- **Multimodal**: Combining multiple modes of input, such as text, images, and sound.
- Denoising **Diffusion**: Sampling from a conditional distribution by iteratively denoising a noisy sample.
- **Embedding**: A vector representation of an object, such as a caption or an image. (In some contexts, also called *latent space* or *latent representation*.)
- **Manifold**: The high-probability region of a distribution
  - e.g., almost all possible images look like random noise; the manifold is the region of images that look like images in the training data

{{% /details %}}
{{% details summary="Readings" %}}
- the rest of the ethics chapter from [Understanding Deep Learning](https://udlbook.github.io/udlbook/)
- [Scheming reasoning evaluations — Apollo Research](https://www.apolloresearch.ai/research/scheming-reasoning-evaluations)
- [Stanford 2025 AI Index Report](
- [Artificial intelligence learns to reason _ Science](https://www.science.org/doi/10.1126/science.adw5211)
- [Turning Employees Into AI Janitors - by Cassie Kozyrkov](https://decision.substack.com/p/turning-employees-into-ai-janitors)
- [Technical Report: Prompt Engineering is Complicated and Contingent - Wharton AI & Analytics Initiative](https://ai-analytics.wharton.upenn.edu/generative-ai-labs/research-and-technical-reports/tech-report-prompt-engineering-is-complicated-and-contingent/)
- [22365_3_Prompt Engineering_v7](https://drive.google.com/file/d/1AbaBYbEa_EbPelsT40-vj64L-2IwUJHy/view)

Another nice reading (about training data), but the server seems down: [Models All the Way Down](https://knowingmachines.org/models-all-the-way) until Part 3

{{% /details %}}
{{% details summary="Resources" %}}
- A [minimalist diffusion model](https://ggx-research.github.io/publication/2023/05/10/publication-iadb.html) (just two tricky concepts, but after that it's pretty accessible; check out the two tutorials linked at the top)
- A video on the [Manifold Hypothesis](https://www.youtube.com/watch?v=BePQBWPnYuE)
- [Generative Modeling by Estimating Gradients of the Data Distribution | Yang Song](http://yang-song.net/blog/2021/score/) (mathy, but has good animated diagrams)

(some of these are drawn from the replies to [this X/twitter post](https://twitter.com/srush_nlp/status/1740756730307629530))

Also, many people refer to [this blog post](https://lilianweng.github.io/posts/2021-07-11-diffusion-models/) by Lilian Weng.

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2025-04-21" %}}
- Easter Monday

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2025-04-23" %}}
- Activity: [Lab 5: Stable Diffusion](/units/13multimodal/lab)
  - Stable Diffusion

- Finish [last week Slides](/slides/w11-prompting.html): How to learn from feedback
  - Example: [RLHF dataset](https://huggingface.co/datasets/Dahoas/full-hh-rlhf)
- Generative Models, Diffusion [Slides](/slides/w12%20Multimodal%20Generation.pdf)
  - Try the [SigLIP demo](https://colab.research.google.com/github/google-research/big_vision/blob/main/big_vision/configs/proj/image_text/SigLIP_demo.ipynb) that embeds images and text together. Try computing the dot products between a few texts that you write by hand. Does the dot product reflect the similarity of the texts? Repeat with images. What do you find?



- STALE: Sharing Homework 2 results
- Interpretability and Explanation ([slides](/slides/w13-Explainable%20and%20Usable.pdf))
- Project Work Time

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2025-04-25" %}}
- Project Work Time
- Quiz 3

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 7

{{% calendar-week-header %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2025-04-28" %}}


{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2025-04-30" %}}
- Activity: [Lab: RL, Transformers, or other topics](/units/14misc/lab)
    - optional choose-your-own-adventure Lab on reinforcement Learning or other topics

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2025-05-02" %}}
- Fairness and Wrap-Up [slides](/slides/w13-Fairness%20and%20Wrap-Up.pdf)

Slides: [A Final Commission](/slides/w14-conclusion.html)
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

