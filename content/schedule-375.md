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
Getting started with ML: running Python in notebooks, training an image classifier using off-the-shelf code.

{{% details summary="Key Questions" %}}
- What is a model architecture? What is training data? What is validation data?
- How do we measure if a model is learning (accuracy vs loss)?

{{% /details %}}
{{% details summary="Objectives" %}}
- Run Python code in computational notebooks
- Train an ML model using off-the-shelf code
- Understand the PPP grading system

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Wednesday" date="2026-01-21" %}}
- Welcome discussion: hopes and concerns
- Course logistics
- Intro slides

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-01-23" %}}
- Basic Image Classifier notebook
- PPP credit system
- Intro to Perusall

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
- Implement basic array operations (element-wise, reductions, dot products)
- Describe the basic ML workflow (instantiate, fit, predict, evaluate)
- Use the sklearn API for regression tasks

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-01-26" %}}
- Lab 1 review
- Translation workflow discussion
- Cognition required for imitation

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-01-28" %}}
- Intro to array programming
- PyTorch/NumPy warmup: dot products and MSE

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-01-30" %}}
- Landscape of AI/ML (supervised, unsupervised, RL)
- sklearn regression notebook

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
- Call an LLM API to build an AI-powered application
- Contrast regression and classification tasks
- Use sklearn for classification

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-02-02" %}}
- Lab recap: PyTorch and sklearn notebooks
- Calling LLM APIs: "use an AI to make an AI"

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-02-04" %}}
- Linear regression "the hard way"
- AI fairness/bias context

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-02-06" %}}
- sklearn classification notebook
- Intro to classification metrics

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
- Implement multiple linear regression "by hand"
- Explain the purpose and mathematical properties of softmax
- Connect cross-entropy loss to classifier evaluation

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-02-09" %}}
- Multiple linear regression: thinking in shapes
- Multilingual chat application

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-02-11" %}}
- Softmax notebook
- Interactive softmax demo

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-02-13" %}}
- From Linear Regression to Logistic Regression in PyTorch
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
- Trace data flow through an MLP, especially shapes
- Write PyTorch expressions for MLP components

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-02-16" %}}
- Feature extractors intro
- ReLU features
- Classifier head and body intro

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-02-18" %}}
- ReLU features notebook
- MLP shapes practice

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-02-20" %}}
- Preview of learning by gradient descent
- Review day

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
- Train an MLP classifier by gradient descent
- Describe ways a model might fail to generalize
- Describe ways to improve generalization (more data, augmentation, regularization)

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-02-23" %}}
- Learning by Gradient Descent
- Gradient game activity

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-02-25" %}}
- autograd API
- Review training loops, SGD, MLP model

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-02-27" %}}
- Will It Generalize?
- Data augmentation

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
- Explain what embeddings are and how they represent similarity
- Describe the key differences between supervised learning and RL
- Understand delayed rewards and exploration in RL

{{% /details %}}
{{% /calendar-week-header %}}
{{% calendar-day dow="Monday" date="2026-03-02" %}}
- Embeddings Day: words, sentences, images
- Image embedding notebook

{{% /calendar-day %}}


{{% calendar-day dow="Wednesday" date="2026-03-04" %}}
- Reinforcement Learning intro
- AlphaGo documentary discussion

{{% /calendar-day %}}


{{% calendar-day dow="Friday" date="2026-03-06" %}}
- Learning to Mimic vs Learning by Exploring
- Course wrap-up

{{% /calendar-day %}}


</div>


