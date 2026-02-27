---
title: "Schedule - CS375"
revised: 2026
toc: true
---

See also: [CS 376 Schedule](/schedule-376)

Any content in the future should be considered tentative and subject to change.


<div class="calendar-week">

## Week 1: Introduction

{{% calendar-week-header %}}
Getting started with ML: impacts of AI, running Python in notebooks, training an image classifier using off-the-shelf code.

{{% details summary="Key Questions" %}}
- What is the essence of modern approaches to AI?
- What optimization games are AI systems playing?
- Can AI systems be smarter than humans?

{{% /details %}}
{{% details summary="Objectives" %}}
- Describe the goals of artificial intelligence and machine learning
- Describe how learning-based AI learns from data, in contrast with rule-based (symbolic) AI
- [OG-ProblemFraming-Paradigms](objective): Contrast supervised learning, self-supervised learning, and reinforcement learning
- Write and execute basic Python code using Jupyter Notebooks

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Wednesday" date="2026-01-21" %}}
- Welcome discussion: hopes and concerns
- Course logistics
    - Assessments: skills, effort, and community
    - Weekly journals, quizzes every other Friday
    - Perusall
- Slides: [Welcome to CS 375](/slides/w01-intro.html)
    - My story and stance:
        - how God brought me to learn about ML/AI
        - how it's a gift that will definitely be in the new creation but we abuse it
    - We need to work to discern AI together.
        - Importance
            - Divisiveness
            - Economic impacts
            - Existential angst
            - Identity, desires, and relationships
            - You need to be able to discern it fundamentally, not just from external behavior
        - This class:
            - This class will be about how it works at a fundamental level and what that fundamental understanding helps us understand about how it fits into God's story
    - Tweakable Machines playing Optimization Games
        - board games
        - hook-the-human games
        - predict protein folding, guess the weather, design a molecule, ...
        - imitation games: mimicking decisions, conversations, images, ...
        - exploration games: control a robot, ...
    - Problem framing
        - programmed vs learned
        - supervised learning: mimicry
        - self-supervised learning: reducing surprise
        - reinforcement learning: learning by trial and error

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-01-23" %}}
- [Lab 1](/units/01introduction/lab/)

[Recording](https://calvincollege.sharepoint.com/:v:/r/sites/Section_COURSE_SECTION-3-116692/Shared%20Documents/General/Recordings/Cold-Day%20Class%20Meeting%20123-20260123_155343UTC-Meeting%20Recording.mp4?csf=1&web=1&e=z2LhCH&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D)

- Tech update: Qwen-TTS

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 2: Array Programming & Regression

{{% calendar-week-header %}}
Introduction to numerical computing with NumPy/PyTorch: element-wise operations, reductions, dot products, MSE. First taste of sklearn regression.

{{% details summary="Key Questions" %}}
- How do we represent data as arrays/tensors?
- What is a dot product and how is it used in ML?
- What does it mean to "fit" a model?

{{% /details %}}
{{% details summary="Objectives" %}}
This week we'll make progress towards the following objectives:

- [TM-TensorOps](objective): Implement basic array-computing operations (element-wise operations, reductions, dot products)
- [OG-LossFunctions](objective): Compute MSE loss
- [OG-ProblemFraming-Paradigms](objective): Contrast different types of learning machines (supervised learning, unsupervised learning, RL)
- If you didn't take DATA 202: use the sklearn API for basic regression tasks

{{% /details %}}
{{% details summary="Resources" %}}
Additionally, you may find these interactive articles helpful (by Amazon's Machine Learning team):

- [Linear Regression](https://cs.calvin.edu/courses/info/602/resources/linreg-explainer/) (originally by Amazon Web Services, some [edits by Prof Arnold](https://github.com/kcarnold/aws-mlu-explain))

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-01-26" %}}
- **Assumptions of AI**: Experience ("IID" amnesia vs continual life; our mistakes matter but Jesus gives us grace)
- Handout: [Lab 1 review, intro to dot product](/handouts/2026_01_26.pdf)
- Lab 1 review
- Intro to dot product

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-01-28" %}}
- Handout: [Supervised Learning](/handouts/2026_01_28.pdf)
- Slides: [CS 375 Week 2](/slides/w02.html)
    - Landscape of AI/ML (supervised, unsupervised, RL)

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-01-30" %}}
- Handout: [Problem framing, dot products review, Lab notes](/handouts/2026_01_30.pdf)
- [Lab 2](/units/02supervised/lab-array/)
    - Notebook: {{% notebook name="PyTorch Warmup" nbname="u02n1-pytorch.ipynb" %}}
- Intro to array programming, regression losses
- If time:
    - Notebook: {{% notebook name="Regression in `scikit-learn`" nbname="u02n2-sklearn-regression.ipynb" %}}

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 3: Linear Models for Regression and Classification

{{% calendar-week-header %}}
Linear regression and classification from the ground up. Introduction to classification models and metrics.

{{% details summary="Key Questions" %}}
- How is linear regression an optimization game played by a tuneable machine?
- How do we evaluate a classification model?

{{% /details %}}
{{% details summary="Objectives" %}}
- [TM-LinearLayers](objective): Fit a linear regression model "by hand" using numerical computing primitives
- [OG-ProblemFraming-Supervised](objective): Identify regression vs classification tasks and select appropriate loss functions
- [OG-LossFunctions](objective): Compute and interpret cross-entropy loss
- [OG-LLM-APIs](objective): Use an LLM API to build an AI-powered application

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-02-02" %}}
- Handout: [PyTorch, dot products, regression metrics](/handouts/2026_02_02.pdf)
- **Assumptions of AI**: What's the objective?
    - ML: optimize single numbers at huge scale
    - Reality:
        - " The thief comes only to steal and kill and destroy; I have come that they may have life, and have it to the full." (John 10:10)
        - the objective is *life*
            - Many wise paths
            - passing on good to children (unbounded richness)
- Logistics:
    - Homework 1
    - Journals
    - Quiz opportunity on Wednesday
- Slides: [CS 375 Week 3](/slides/w03.html)
- Lab recap: PyTorch (and sklearn notebooks)

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-02-04" %}}
- First quiz opportunity [OG-ProblemFraming-Paradigms](objective), [OG-ProblemFraming-Supervised](objective), [TM-DotProduct](objective), [OG-LossFunctions](objective), [TM-TensorOps](objective)
- Starting ["Linear Regression the Hard Way"](/units/03fundamentals/linreg/)
    - Building intuition for linear regression using [UDL figure](https://udlbook.github.io/udlfigures/) or [linreg explainer](https://cs.calvin.edu/courses/info/602/resources/linreg-explainer/)
- Notebook: {{% notebook name="Linear Regression the Hard Way" nbname="u03n1-linreg-manual.ipynb" %}}

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-02-06" %}}
- Tech update: [Opus 4.6 release](https://www.anthropic.com/news/claude-opus-4-6)
- Handout: [Matrix product, Elo intuition](/handouts/2026_02_06.pdf)
- Slides: [CS 375 Week 3](/slides/w03.html)
- Reviewing notebooks:
    - Notebook: {{% notebook name="Train a simple image classifier" nbname="u01n1-train-clf.ipynb" %}}
- (we didn't get to...)
    - Notebook: {{% notebook name="PyTorch Warmup" nbname="u02n1-pytorch.ipynb" %}}
    - Notebook: {{% notebook name="Linear Regression the Hard Way" nbname="u03n1-linreg-manual.ipynb" %}}
    - Notebook: {{% notebook name="Regression in `scikit-learn`" nbname="u02n2-sklearn-regression.ipynb" %}}
    - Notebook: {{% notebook name="Classification in `scikit-learn`" nbname="u03n2-sklearn-classification.ipynb" %}}

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 4: Multi-input Models & Softmax

{{% calendar-week-header %}}
Extending linear models to multiple inputs. Understanding softmax and cross-entropy loss.

{{% details summary="Key Questions" %}}
- How does linear regression extend to multiple input features?
- What is softmax and why do we use it for classification?
- What is cross-entropy loss?

{{% /details %}}
{{% details summary="Objectives" %}}
- [TM-TensorOps](objective): Work with multi-dimensional tensors, predict shapes of matrix operations
- [TM-DataFlow](objective): Trace data shapes through a multi-input linear model
- [TM-Softmax](objective): Implement softmax and explain why it produces a valid probability distribution
- [OG-LossFunctions](objective): Describe and compute cross-entropy loss

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-02-09" %}}
- Assumptions of AI: framed problems
- Handouts - review, then new:
    - Handout: [Matrix product, Elo intuition](/handouts/2026_02_06.pdf)
    - Handout: [Cross-entropy loss, linear layer shapes](/handouts/2026_02_09.pdf)
- Review
    - Slides: [CS 375 Week 3](/slides/w03.html)
    - Quiz 1 (and how [objectives](/objectives-375) grading will work)
- Classification metrics (accuracy, cross-entropy)
    - Slides: [CS375 Week 4](/slides/w04.html)
- Notebook: {{% notebook name="Multiple Linear Regression, the Hard Way" nbname="u04n1-multi-linreg-manual.ipynb" %}}

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-02-11" %}}
- Handout: [Shapes for Linear and Logistic Regression; Cross-Entropy](/handouts/2026_02_11.pdf)
- Slides: [CS375 Week 4](/slides/w04.html)
- [Interactive softmax demo](https://observablehq.com/@kcarnold/softmax)
    - Try to match the example given in the handout (3 classes, probs `[0.25, 0.25, 0.5]`).
    - What happens if you shift all the scores up and down (+/- 0.5)? What happens if you multiply?
- Notebook: {{% notebook name="Softmax, part 1" nbname="u04n2-softmax.ipynb" %}}

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-02-13" %}}
- Quiz 2
- When you're done, one person set up on each monitor around the room and go through:
    - Notebook: {{% notebook name="From Linear Regression in NumPy to Logistic Regression in PyTorch" nbname="u04n3-logreg-pytorch.ipynb" %}}

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 5: Feature Extraction / Embeddings; MLP Architecture

{{% calendar-week-header %}}
Understanding feature extraction with ReLU. Introduction to classifier heads and bodies. The multi-layer perceptron (MLP) architecture.

{{% details summary="Key Questions" %}}
- Why are good features important for neural networks?
- What is a classifier "head" vs "body"?
- How does ReLU create useful features?

{{% /details %}}
{{% details summary="Objectives" %}}
- [TM-RepresentationLearning](objective): Explain why good features make classification easier
- [TM-ActivationFunctions](objective): Implement ReLU and explain what it does
- [TM-DataFlow](objective): Trace the data flow through an MLP, labeling shapes at each layer
- [TM-MLPParts](objective): Identify and explain the components of an MLP (linear layers, activations, output layer)

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-02-16" %}}
- Quiz 2 Redo
- Reviewing [Logistic Regression notebook](/units/04structures/pytorch-logreg/)

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-02-18" %}}
- Assumptions of AI: perception
    - Internal representations collapse "irrelevant" distinctions ("noise reduction")
    - But in God's world, nothing is "noise". Every detail can show God's glory, and we can learn from even the smallest things ("Go to the ant, you sluggard; consider its ways and be wise!" [Proverbs 6:6](https://www.biblegateway.com/passage/?search=Proverbs%206%3A6&version=NIV)).
    - Other examples:
        - meditating on texts
        - faith looks at what is unseen
        - learning to look again, to change our perception
        - "the eye is the lamp of the body. If your eyes are healthy, your whole body will be full of light. But if your eyes are unhealthy, your whole body will be full of darkness. If then the light within you is darkness, how great is that darkness!" (Matthew 6:22-23)
- How objective grading works; [course objectives](/objectives-375)
- Feature extractors intro, also reviewing logistic regression / softmax / cross-entropy
  - Handout: [Logistic regression review, ReLU intro](/handouts/2026_02_18.pdf)
- Possible resources:
    - [YouTube: tiny neural net](https://www.youtube.com/watch?v=dES5Cen0q-Y)
    - 0byte [Intro to PyTorch](https://0byte.io/articles/pytorch_introduction.html)

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-02-20" %}}
- Quiz 2 return and walkthrough. Most common mistakes:
    - Q1: remember matmul shapes: to do `X @ W`, then `X.shape[-1] == W.shape[0]`.
    - Q2: softmax takes _vectors_ and returns _vectors_.
    - Q3: cross-entropy is *not* "differences from true class probabilities".
- Intro to ReLU features:
    - Notebook: {{% notebook name="ReLU Regression Interactive" nbname="u05n00-relu.ipynb" %}}
    - handout example
- Mini-lecture on MLP architecture:
    - tax brackets example as an MLP (with ReLU activations) we can do by hand
- Handout: [ReLU features, MLP architecture, feature extraction intuition](/handouts/2026_02_20.pdf)
- MLP shapes practice

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 6: Gradient Descent, Generalization, and LLM APIs

{{% calendar-week-header %}}
MLP mastery and quiz. Learning by gradient descent. Understanding why generalization matters. First look at LLM APIs.

{{% details summary="Key Questions" %}}
- How does gradient descent work?
- What is overfitting vs underfitting?
- What can we build with LLM APIs?

{{% /details %}}
{{% details summary="Objectives" %}}
- [TM-Implement-TrainingLoop](objective): Train an MLP classifier by gradient descent and understand each step
- [OG-Theory-SGD](objective): Describe how SGD uses gradients and batches to improve performance
- [TM-Autograd](objective): Explain what loss.backward() and optimizer.step() do
- [OG-Generalization](objective): Diagnose overfitting and underfitting from learning curves
- [OG-DataDistribution](objective): Explain how data augmentation expands the effective training distribution
- [OG-Implement-Validate](objective): Explain the importance of evaluating models on unseen data
- [OG-LLM-APIs](objective): Use an LLM API to build an AI-powered application

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-02-23" %}}
First half: MLP review and practice

- Handout: [MLP review, training loop, and gradient intuition](/handouts/2026_02_23.pdf)
    - Review: ReLU creates useful features → representations → why this matters

Second half: Quiz 3

- Quiz 3: [TM-ActivationFunctions](objective), [TM-RepresentationLearning](objective); redo opportunities for [TM-Softmax](objective), [OG-LossFunctions](objective)

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-02-25" %}}
- 10 min opportunity to finish Quiz 3
- Slides: [CS 375 Week 6](/slides/w06.html)
- [udlbook figure](https://udlbook.github.io/udlfigures/)
- Mini-lecture: "How does the machine learn?" SGD intuition
    - Gradient = direction of steepest increase; we go opposite to reduce loss
    - Learning rate: too big overshoots, too small is slow
    - Why batches (stochastic): noise helps escape local minima, plus efficiency
- No new handout today; review last time.
    - What would happen if we didn't have ReLU?
- [Gradient game activity](https://ds100.org/su21/resources/assets/lectures/lec18/gradient_game_v3.html)
- gradient intuition: suppose a dot b is 0. How can we change each element of b (in isolation) to make the dot product 0.1 instead?
- Live coding / notebook: training an MNIST classifier
    - Walk through: forward pass → loss → loss.backward() → optimizer.step() → zero_grad()
    - Notebook: {{% notebook name="MNIST with PyTorch" nbname="u06n1-mnist-torch.ipynb" %}}

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-02-27" %}}
- Review Quiz 3
- Handout: [SGD Lingo, Generalization, Data Augmentation](/handouts/2026_02_27.pdf)
- Generalization, based on MNIST notebook results
    - Show learning curves: identify overfitting vs underfitting
    - Adversarial examples as a dramatic illustration
    - Brief: data augmentation (Notebook: u06s2-mnist-torch-augmentation.ipynb)
- Slides: [CS 375 Week 6](/slides/w06.html)
- Also a brief review of why ReLU works (regions)
    - Slides: [Week 5](/slides/w05.html)
- Review SGD concepts
    - gradients, learning rates, batches
    - [Interactive demo](https://claude.ai/public/artifacts/41c1d9d2-56c2-4a90-9c13-c93d486e70fd)
    - Enable "show components". What are the shapes of each component?
    - What happens if you increase the learning rate? What happens if you decrease it?
    - What happens if you increase the batch size? What happens if you decrease it?

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 7: Embeddings & RL

{{% calendar-week-header %}}
Embeddings as the data structures of neural computation. Introduction to reinforcement learning.

{{% details summary="Key Questions" %}}
- What are embeddings and how are they used in ML?
- How does reinforcement learning differ from supervised learning?
- What is the difference between learning to mimic vs learning by exploring?

{{% /details %}}
{{% details summary="Objectives" %}}
- [TM-Embeddings](objective): Explain what embeddings are and how they represent similarity
- [OG-Pretrained](objective): Explain how a pretrained model can be repurposed using the body + head pattern
- [OG-ProblemFraming-Paradigms](objective): Contrast supervised learning and reinforcement learning
- [OG-DataDistribution](objective): Contrast how data distribution is given (supervised) vs shaped by exploration (RL)

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-03-02" %}}
- Embeddings Day: words, sentences, images
- Slides: [Computing](/slides/computing.html#/embeddings)
- Notebook: {{% notebook name="Probe an Image Classifier" nbname="u07n1-image-embeddings.ipynb" %}}

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-03-04" %}}
- Reinforcement Learning intro
- Notebook: {{% notebook name="A Reinforcement Learning Example" nbname="u07n2-rl.ipynb" %}}
- Optional: Notebook: u07n1-image-ops.ipynb

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-03-06" %}}
- Slides: [CS 375: Wrap-Up](/slides/wrapup-375.html)
- Learning to Mimic vs Learning by Exploring
- Course wrap-up

{{% /calendar-day %}}


</div>


