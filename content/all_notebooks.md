---
title: "Notebooks Index"
revised: 2025
---

## Goal

These notebooks will demonstrate proficiency in basic machine learning concepts and skills.

To complete a notebook, follow instructions and fill in blanks. Most blanks will be labeled `# your code here`, an ellipsis (`...`), or `*your answer here*` (for narrative answers written in Markdown). You should remove placeholder comments.

Successful solutions will:

- Include code that successfully accomplishes the task.
  - It should generate the results when run fresh ("Restart and Run All")
  - It should have no extraneous code.
  - Format code clearly (consistent spacing, one idea per line, no overly long lines, etc.)
- Document each major step succinctly but clearly.
  - Use Markdown cells (with appropriate formatting and links) to describe the overall steps taken.
    - See the Setup section of various notebooks for an example of code explanations.
    - Note that you are not required to understand the code in the "Setup" section.
  - Use clear variable names, keyword arguments, and code comments to make the code easy to follow.
- Include responses to each of the analysis questions.
  - Add a Markdown cell for each question.
  - Add code cells as necessary to run computations that some questions may need.
  - Any activities marked "Extension" are optional but encouraged.

We aim that each notebook will:

- Demonstrate a single concept
- Take less than 15 minutes to complete, if that concept is understood (if it's taking longer than 15 minutes, please let the instructor know so it can be simplified in the future)
- Take less than 5 minutes to run to completion
- Be a useful reference for how to perform that operation in the future

We also strive for the sequence to make sense.

## The Notebooks

**Note**: Notebooks beyond the current week may not be updated for the current year.



### Week 1

- {{% notebook name="Jupyter Notebook Warmup" nbname="u01n0-notebook-warmup.ipynb" %}}
  - Jupyter Notebooks
- {{% notebook name="Train a simple image classifier" nbname="u01n1-train-clf.ipynb" %}}
    - Course Objectives Addressed
  - Setup
  - Configure our experiments
    - Load the data
    - Example Images
    - Train a model
    - Make some predictions
  - Experimentation
  - All validation set predictions
  - Try out your own image

### Week 2

- {{% notebook name="PyTorch Warmup" nbname="u02n1-pytorch.ipynb" %}}
    - Course Objectives Addressed
  - Dot Products
    - `for` loop approach
      - Torch Elementwise Operations
    - Torch Reduction Ops
    - Building a dot product out of Torch ops
  - Linear Layer
    - Linear layer, Module-style
  - Mean Squared Error
  - Multidimensional arrays
  - Appendix
- {{% notebook name="Regression in `scikit-learn`" nbname="u02n2-sklearn-regression.ipynb" %}}
    - Course Objectives Addressed
  - Setup
  - Task
    - Part A: Linear regression
    - Part B: Decision tree regression
    - Part C: Random Forest regression
  - Analysis
  - Extension

### Week 3

- {{% notebook name="Linear Regression the Hard Way" nbname="u03n1-linreg-manual.ipynb" %}}
  - Objectives
    - Course Objectives Addressed
  - Setup
  - Task
    - Step 0: Initialize the model
    - Step 1: Single prediction
    - Step 2: Prediction for all inputs
      - Visualizing the predictions
    - Step 3: Compute loss
    - Step 4: Compute loss given parameters
    - Check in
  - Guided Extension
- {{% notebook name="Classification in `scikit-learn`" nbname="u03n2-sklearn-classification.ipynb" %}}
    - Course Objectives Addressed
  - Setup
  - Task
    - Part A: Logistic Regression
    - Part B: Decision tree classifier
    - Part C: Random Forest
  - Analysis
  - Extension

### Week 4

- {{% notebook name="Multiple Linear Regression, the Hard Way (PyTorch version)" nbname="u04n1-multi-linreg-manual-torch.ipynb" %}}
    - Course Objectives Addressed
  - Setup
  - Task
    - Part A: Linear regression
  - Analysis
- {{% notebook name="Multiple Linear Regression, the Hard Way" nbname="u04n1-multi-linreg-manual.ipynb" %}}
    - Course Objectives Addressed
  - Setup
  - Task
    - Part A: Linear regression
  - Analysis
- {{% notebook name="Softmax, part 1" nbname="u04n2-softmax.ipynb" %}}
    - Course Objectives Addressed
  - Setup
  - Task
  - Analysis
  - Optional Extension: Numerical Issues
    - Task for Numerical Issues
    - Analysis of Numerical Issues
  - Extension *optional*
- {{% notebook name="From Linear Regression in NumPy to Logistic Regression in PyTorch" nbname="u04n3-logreg-pytorch.ipynb" %}}
    - Course Objectives Addressed
  - Setup
    - Basic EDA
  - Part 1: Classification the wrong way (using linear regression)
    - 1.A Using NumPy
    - 1.B: Using PyTorch
  - Part 2: Converting to Classification
    - 2.A Using NumPy (we'll do this together)
    - 2.B Using PyTorch
      - Setting up the linear layer
      - Softmax
      - Cross-entropy loss
      - Full PyTorch Implementation
    - Looking ahead: a multi-layer network
  - Analysis

### Week 5

- {{% notebook name="ReLU Regression Interactive" nbname="u05n00-relu.ipynb" %}}
  - Task
- {{% notebook name="Image Classification: Losses and Feature Extraction" nbname="u05n1-img-classifier-feature-extractor.ipynb" %}}
  - Setup
  - Configure our experiments
    - Load the data
    - Train a model
  - Top Losses
  - Model as Feature Extractor
    - Importance of Feature Extractors
  - Check-In
- {{% notebook name="Logistic Regression and MLP" nbname="u05n2-logreg-mlp.ipynb" %}}
  - Setup
  - Data Loading
  - Train and Evaluate Model
  - Analysis
- {{% notebook name="Train Simple Image Classifier" nbname="u05n3-mnist-clf.ipynb" %}}
  - Setup
  - Task
  - Analysis
  - Extension
- Supplemental
  - {{% notebook name="Softmax and Sigmoid" nbname="u05s2-softmax-2.ipynb" %}}
    - Setup
    - Task
    - Analysis
  - {{% notebook name="Diagnose and Probe an Image Classifier" nbname="u05s3-clf-prototypes.ipynb" %}}
    - Setup
    - Configure our experiments
      - Load the data
      - Train a model
    - Top Losses
    - Manual Last Layer
    - Softmax and Cross-Entropy

### Week 6

- {{% notebook name="MNIST with PyTorch" nbname="u06n1-mnist-torch.ipynb" %}}
    - Course Objectives
  - Load and Understand the Data
    - Understanding Flattening
    - Setting Up Data Loaders
  - Train an MLP to Classify MNIST
    - Shape checkpoint
  - Analyzing the Trained Model
    - Confusion Matrix
    - Most Confident Mistakes
    - Visualizing Learned Weights
  - Reflection Questions
  - Next Steps
- {{% notebook name="Trace Simple Image Classifier" nbname="u06n1-trace-mnist.ipynb" %}}
  - Setup
  - Task
  - Analysis
- {{% notebook name="Compute gradients using PyTorch" nbname="u06n2-compute-grad-pytorch.ipynb" %}}
  - Setup
  - Task 1
  - Task 2
  - Analysis
- {{% notebook name="Linear Regression using the Fast.ai Learner" nbname="u06n2-linreg-learner.ipynb" %}}
  - Setup
  - Task
  - Solution
  - Analysis
- {{% notebook name="Linear Regression the Hard Way" nbname="u06n3-linreg-manual.ipynb" %}}
  - Setup
  - Task
- {{% notebook name="Nonlinear Regression" nbname="u06n3-nn-regression.ipynb" %}}
  - Setup
  - Task
  - Solution
    - Step 1: Fit a Line
    - Step 2: Add a Layer
    - Step 3: **Add a nonlinearity**
  - Analysis
  - Extension (optional)
- Supplemental
  - {{% notebook name="Bias-Variance Decomposition" nbname="u06s01-bias-variance.ipynb" %}}
  - {{% notebook name="MNIST with PyTorch" nbname="u06s2-mnist-torch-augmentation.ipynb" %}}
    - Load and Understand the Data
      - Understanding Flattening
      - Setting up data loaders
    - Train an MLP to classify MNIST
    - Data Augmentation

### Week 7

- {{% notebook name="Probe an Image Classifier" nbname="u07n1-image-embeddings.ipynb" %}}
  - Setup
  - Configure our experiments
    - Load the data
    - Train a model
  - Top Losses
  - Manual Last Layer
  - Softmax and Cross-Entropy
- {{% notebook name="Image Operations" nbname="u07n1-image-ops.ipynb" %}}
  - Setup
    - Configure
    - Load the data
  - Task
  - Convolution layers
  - A real conv layer
- {{% notebook name="A Reinforcement Learning Example" nbname="u07n2-rl.ipynb" %}}

### Week 8

- {{% notebook name="Tokenization" nbname="u08n1-tokenization.ipynb" %}}
  - Setup
    - Download and load the model
  - Demo
  - Task
    - Getting familiar with tokens
    - Applying what you learned
  - Analysis
- Supplemental
  - {{% notebook name="Sentence Embeddings" nbname="u08s1-sentence-embeddings.ipynb" %}}
    - Install and Import
    - Load Model and Data
    - Compute Sentence Vectors
    - Visualize Sentence Vectors
    - Find Clusters
    - How does it work?
    - Looking for Similar Vectors

### Week 9

- {{% notebook name="Demo of Logits and Embeddings from a Language Model" nbname="u09n0-logits-demo.ipynb" %}}
  - Tokenization
  - Embeddings
  - Example of mapping
  - Vector Analogies
  - What the model does
- {{% notebook name="Logits in Causal Language Models" nbname="u09n1-lm-logits.ipynb" %}}
  - Setup
  - Task
  - Analysis
- {{% notebook name="An exercise on bias in word embeddings." nbname="u09n1-word-embeddings.ipynb" %}}
  - Directions are meaningful
- {{% notebook name="Translation as Language Modeling" nbname="u09n2-decoding.ipynb" %}}
  - Setup
  - Warm-up
  - Scoring a candidate translation
  - Dig In!
    - The guts of the model
  - Visualize attentions
  - Similarity

### Week 10

- {{% notebook name="Implementing self-attention" nbname="u10n1-implement-transformer.ipynb" %}}
  - Setup
  - Dataset
  - Tokenization
  - Multi-Layer Perceptron
  - A language model with a single MLP
  - Trace the Simple Model
    - Step 1: Embeddings
    - Step 2: MLP
    - Step 3: LM Head
  - Generating text
  - Self-Attention
    - Train the Transformer
    - Tracing the Transformer
    - Finish the trace
  - Other things you could try

### Week 11

- {{% notebook name="Prompt Engineering" nbname="u11n1-prompt-engineering.ipynb" %}}
  - Warm-Up
  - Chat Templating
  - Retrieval-Augmented Generation

### Week 12

- {{% notebook name="Stable Diffusion Deep Dive" nbname="u12n1-stable-diffusion.ipynb" %}}
  - Setup & Imports
  - Loading the models
  - A diffusion loop
  - The Autoencoder (AE)
  - The Scheduler
  - Loop starting from noised version of input (AKA image2image)
  - Exploring the text -> embedding pipeline
    - Token embeddings
    - Positional Embeddings
    - Combining token and position embeddings
    - Feeding these through the transformer model
    - Textual Inversion
  - Messing with Embeddings
  - The UNET and CFG
    - Classifier Free Guidance
  - Sampling
  - Guidance
  - Conclusions
- {{% notebook name="Calvin Course Advisor Bot" nbname="u12n2-agent-rag.ipynb" %}}
    - Option 1: Run locally:
  - Warm-Up: Structured Outputs
  - Step 2: Make a simple retrieval system
  - A Complete Bot

### Week 13

- {{% notebook name="Why so big? Counting parameters in sequence models" nbname="u13n1-count-params.ipynb" %}}
  - Setup
  - Embeddings
  - Complete but vacuous model
  - Multi-Layer Perceptron
    - Complete Language Model with MLP
  - Transformer
  - Analysis
- {{% notebook name="Models for Sequence Data" nbname="u13n2-seq-models.ipynb" %}}
  - Setup
  - Getting started
  - Feed-Forward Network
    - Create the model
    - Check its output shape
    - Check its speed
    - Check how gradients flow
  - GRU
    - Your turn
  - Convolution
  - Transformer
  - Analysis
- {{% notebook name="Programming with Self-Attention" nbname="u13n3-self-attention.ipynb" %}}
  - Where We're Going
  - Section 1: Feed-Forward Network
    - Exercise
  - Section 2: Keys and Queries
  - Exercise
  - Exercise
    - Exercise: **histogram**.
  - Section 3: Values (other than 1)
  - Exercise: pattern detect
