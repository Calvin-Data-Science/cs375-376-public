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
- Describe the goals of artificial intelligence and machine learning.
- Describe the overall approach of how learning-based AI learns from data, in contrast with rule-based (symbolic) AI
- Contrast supervised learning, unsupervised/self-supervised learning, and reinforcement learning
- Write and execute basic Python code using Jupyter Notebooks
- Understand the grading system

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
        - how it’s a gift that will definitely be in the new creation but we abuse it
    - We need to work to discern AI together.
        - Importance
            - Divisiveness
            - Economic impacts
            - Existential angst
            - Identity, desires, and relationships
            - You need to be able to discern it fundamentally, not just from external behavior
        - This class:
            - This class will be about how it works at a fundamental level and what that fundamental understanding helps us understand about how it fits into God’s story
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
- **Moved to Monday** Handout introduction to the dot product
- [Lab 1](/units/01introduction/lab/)

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
- Implement basic essential array-computing operations (element-wise operations, reductions, dot products, MSE)
- Contrast different types of learning machines (supervised learning, unsupervised learning, RL)
- Use the sklearn API for basic regression tasks

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

## Week 3: LLM APIs & Classification

{{% calendar-week-header %}}
Using LLM APIs to build AI-powered applications. Introduction to classification models and metrics.

{{% details summary="Key Questions" %}}
- How do we call an LLM API?
- What's the difference between regression and classification?
- How do we evaluate a classification model (accuracy, precision, recall)?

{{% /details %}}
{{% details summary="Objectives" %}}
- Use an LLM API to build an AI-powered application
- Fit a linear regression model "by hand" using numerical computing primitives
- Describe two different ways of measuring how good a classification is
- Use basic linear and tree models for classification with sklearn
- Quantify classifier performance using accuracy, precision, recall, and cross-entropy

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-02-02" %}}
- Lab recap: PyTorch and sklearn notebooks
- LLM API intro: "use an AI to make an AI"

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-02-04" %}}
- Notebook: {{% notebook name="Linear Regression the Hard Way" nbname="u03n1-linreg-manual.ipynb" %}}
- Context discussion: AI fairness and bias

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-02-06" %}}
- Slides: [Learning Machines](/slides/learning-machines.html#/metrics)
- Notebook: {{% notebook name="Classification in `scikit-learn`" nbname="u03n2-sklearn-classification.ipynb" %}}
- Classification metrics (accuracy, precision, recall, cross-entropy)

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
- Extend understanding of linear regression to multiple input features (thinking through shapes)
- Explain the purpose and mathematical properties of the softmax operation
- Practice logistic regression and learn how to fit simple models in PyTorch
- Describe and compute cross-entropy loss

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-02-09" %}}
- Notebook: {{% notebook name="Multiple Linear Regression, the Hard Way" nbname="u04n1-multi-linreg-manual.ipynb" %}}
- Multilingual chat application demo

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-02-11" %}}
- Slides: [Computing](/slides/computing.html#/linear-regression)
- Notebook: {{% notebook name="Softmax, part 1" nbname="u04n2-softmax.ipynb" %}}
- Interactive softmax demo

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-02-13" %}}
- Notebook: {{% notebook name="From Linear Regression in NumPy to Logistic Regression in PyTorch" nbname="u04n3-logreg-pytorch.ipynb" %}}
- Hw2 soft-due: demo an AI-powered application

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 5: Features & Review

{{% calendar-week-header %}}
Understanding feature extraction with ReLU. Introduction to classifier heads and bodies. Review and preparation for gradient descent.

{{% details summary="Key Questions" %}}
- Why are good features important for neural networks?
- What is a classifier "head" vs "body"?
- How does ReLU create useful features?

{{% /details %}}
{{% details summary="Objectives" %}}
- Explain the importance of good features for neural network models
- Understand how a nonlinearity (like ReLU) can be useful for feature extraction
- Trace the data flow through an MLP, especially the shapes
- Write PyTorch expressions for each of the MLP components
- Explain the role of nonlinearities in a neural network (e.g., why they are used between linear layers)

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-02-16" %}}
- Feature extractors intro
- ReLU features intro
- Classifier head and body intro

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-02-18" %}}
- Notebook: {{% notebook name="ReLU Regression Interactive" nbname="u05n00-relu.ipynb" %}}
- Notebook: {{% notebook name="Logistic Regression and MLP" nbname="u05n2-logreg-mlp.ipynb" %}}
- MLP shapes practice

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-02-20" %}}
- Preview of learning by gradient descent
- Review day: gradient game
- Tech presentation

{{% /calendar-day %}}


</div>


<div class="calendar-week">

## Week 6: Gradient Descent & Generalization

{{% calendar-week-header %}}
Learning by gradient descent. Understanding why generalization matters and how to measure/improve it.

{{% details summary="Key Questions" %}}
- How does gradient descent work?
- What is overfitting vs underfitting?
- How can data augmentation help generalization?

{{% /details %}}
{{% details summary="Objectives" %}}
- Train an MLP classifier by gradient descent and know what everything does
- Describe the overall approach of Stochastic Gradient Descent: how it uses information from a batch of data to improve performance
- Describe a few ways that an ML model might do well on its training data but fail to generalize
- Describe ways to make a model generalize better (more data, data augmentation, regularization)
- Explain the importance of evaluating models on unseen data

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-02-23" %}}
- Gradient game activity
- Notebook: {{% notebook name="MNIST with PyTorch" nbname="u06n1-mnist-torch.ipynb" %}}

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-02-25" %}}
- Notebook: {{% notebook name="Compute gradients using PyTorch" nbname="u06n2-compute-grad-pytorch.ipynb" %}}
- Review training loops, SGD, MLP model

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-02-27" %}}
- Will It Generalize? slides
- Data augmentation notebook
- Tech presentation

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
- Explain what embeddings are (the data structures used in ML) and how they represent similarity
- Interpret vectors as points in a space and use dot product to measure similarity between data items
- Explain how a pretrained model can be repurposed for a new task by separating it into a feature extractor (body) and task-specific classifier (head)
- Describe the key differences between supervised learning and reinforcement learning
- Understand delayed rewards and exploration in RL
- Explain the difference between learning to mimic vs learning by exploring

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


