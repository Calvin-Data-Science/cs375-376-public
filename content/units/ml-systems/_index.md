---
title: "ML Systems"
revised: 2025
weight: 11
---


## Key questions

- 375:
  - What are the inputs to and outputs of AI systems?
  - What abstractions do systems provide, and how can they compose? (ML APIs)
  - How do we evaluate ML solutions?
- 376:
  - How do we evaluate language models?
  - Can I run an LLM on my laptop? Can I train one?

## Key objectives

After this course, I will be able to:

- 375:
  - APIs and systems
    - I can create a computational notebook that includes code, execution results, section headings, and formatted textual explanations.
    - I can write code that loads data, preprocesses it, and feeds it to a supervised ML model using a sklearn-style fit-predict API.
    - I can select appropriate loss functions and metrics for a given task (and thus choose an appropriate model type/structure). Specifically, I can distinguish between regression and classification problems, even if classification targets happen to be encoded as numbers.
    - I can integrate an ML model into a larger application.
  - Experimentation and Evaluation
    - I can design, run, and analyze empirical experiments to quantify the impact of hyperparameter changes on model performance.
    - I can make and interpret plots of relevant evaluation metrics.
    - I can identify hyperparameters that can be adjusted to improve the performance of a model.
- 376:
  - I can solve basic language and reasoning tasks using commercially deployed LLM APIs.
  - I can apply and critically analyze evaluation strategies for generative models.
  - I can describe the overall process of training a state-of-the-art dialogue LLM such as Llama or OLMo.
  - I can analyze the computational requirements of training and inference of generative AI systems.

## Learning Sequence

-   I've trained a classifier (using code already provided)
    -   basic image clf notebook
-   I've called a LLM API
    -   `llm` library
-   I've designed a prompt for an LLM
-   I've used a high-level API to run a neural network model
-   I've generated:
    -   An array of class probabilities
    -   A chatbot response
    -   A next-token prediction
    -   An image
-   I've computed the similarity between two embeddings and compared that with another pairwise similarity.
-   I've used the sklearn (fit-predict) API
-   I've evaluated the performance of a regression model and a classification model using appropriate metrics.

## Materials

- [Slides](/slides/ml-systems.html)
