---
title: "Homework 3: Open-Ended AI Project"
revised: 2025
---

**Important**: Read this whole document before you start.

## Goal

In this assignment, you will choose one of three project options and build something real with AI/ML tools. Each option targets different course objectives and lets you explore an area that interests you.

You may work individually or in pairs. If you work in a pair, **each person must write their own reflection section** (see below), and both partners should be able to explain every part of the project. A good test: if someone asked either of you "why did you do X?", both of you should be able to answer confidently.

## Choose Your Project

Pick **one** of the following options.

### Option A: Build an LLM-Powered Application

Build an application that uses an LLM API (e.g., OpenAI, Anthropic, Google Gemini) to do something useful. Examples:

- A study tool that quizzes you on material and explains what you got wrong
- A writing assistant that gives feedback on drafts
- A data analyzer that takes a CSV and answers questions about it
- A tool that helps debug code by explaining error messages

**What you need to demonstrate** (OG-LLM-APIs):

- Construct appropriate API calls with system and user messages
- Process and use the model's response meaningfully (not just print it)
- Show that you thought about what the LLM is and isn't good at for your task

**Suggested models**: Claude 3.5 Sonnet or Claude 4 Haiku (via the Anthropic API), GPT-4o-mini (via OpenAI), or Gemini 2.0 Flash (via Google AI Studio). All have free tiers or student credits available.

### Option B: Pretrained Embeddings Project

Use a pretrained model's embeddings to solve a problem involving similarity or search. Examples:

- An image search engine: given a text query, find the most similar images in a collection
- A "find similar" tool: given one image (or text), find the most similar items
- A simple recommendation system based on content similarity
- Clustering a dataset and visualizing what the model "sees"

**What you need to demonstrate** (OG-Pretrained, TM-Embeddings):

- Explain what embeddings are and why similar items end up near each other
- Use the "body + head" pattern: a pretrained feature extractor with your own task-specific logic on top
- Show a visualization of the embedding space (e.g., a 2D plot using UMAP or t-SNE) and explain what you see
- Discuss at least one risk of using a pretrained model (bias, domain mismatch, etc.)

**Suggested models**: OpenAI `text-embedding-3-small`, Sentence Transformers (`all-MiniLM-L6-v2`), or CLIP (`openai/clip-vit-base-patch32`) for cross-modal image+text embeddings. For images, `torchvision` models like EfficientNet_V2 or ConvNeXt work well as feature extractors.

### Option C: Adversarial Examples or Data Augmentation Experiment

Design and run an experiment about how training data affects model behavior. Examples:

- Generate adversarial examples that fool a classifier and analyze *why* they work
- Compare model performance with and without data augmentation strategies
- Test how a model trained on one distribution performs on a shifted distribution (e.g., trained on photos, tested on sketches)
- Investigate how the amount or diversity of training data affects generalization

**What you need to demonstrate** (OG-DataDistribution):

- Identify a specific way the training distribution could differ from deployment
- Design an experiment with a clear hypothesis and measurable outcome
- Show quantitative results (accuracy, confusion matrices, example predictions)
- Explain what your results tell us about when we should or shouldn't trust this model

**Suggested tools**: PyTorch with `torchvision.transforms` for augmentation, the [Adversarial Robustness Toolbox](https://github.com/Trusted-AI/adversarial-robustness-toolbox), or FGSM attacks implemented from scratch (a few lines of code). Datasets like CIFAR-10, MNIST, or your HW1 letter dataset work well.

## Report Expectations

Your report should be a professionally crafted Jupyter Notebook, suitable to use in a portfolio. Your notebook should be:

- **Well-formatted**: use appropriate `## Headings`; proofread text and code.
- **Literate**: explain what you are doing and why, in your own words. Walk the reader through your thinking.
- **Reproducible**: running it from a clean slate should reproduce the results shown.
- **Focused**: don't include extraneous code or leftover cells. Everything in the notebook should serve your narrative.

We recommend this structure:

1. **Introduction**: What are you building and why? What problem does it solve or question does it answer?
2. **Setup**: What tools, models, and data are you using? Why did you choose them?
3. **Implementation**: Your working code with explanations. Show your work clearly.
4. **Results**: What happened? Show concrete outputs, examples, and (where relevant) quantitative evaluation.
5. **Reflection** (individual, even if working in a pair): see below.

### Reflection Section

Each person must write their own reflection addressing:

- What did you learn from this project that you didn't know before?
- What was the hardest part, and how did you work through it?
- What would you do differently if you had more time?
- How does this project connect to the course objectives listed for your option?

If working in a pair, clearly label each person's reflection (e.g., "## Reflection (Alice)" and "## Reflection (Bob)").

## Using AI Tools

You are welcome and encouraged to use AI assistants (Claude, ChatGPT, Copilot, etc.) as you work on this project. They are powerful learning tools.

However, **the goal is for you to learn**, not to produce a polished artifact you don't understand. Here is what we expect:

- **Do** use AI to help you understand error messages, debug code, or learn about a new API.
- **Do** use AI to brainstorm ideas or get unstuck.
- **Don't** paste the assignment prompt into an AI and submit what comes back.
- **Do** make sure you can explain every line of code in your notebook. If you can't explain it, you haven't learned it yet — ask the AI to *teach* you rather than just giving you the answer.

If you used AI assistance, briefly mention how in your reflection (e.g., "I used Claude to help me understand how to format the API request, then wrote the rest myself").

## How Your Work Will Be Evaluated

Your notebook will be evaluated based on how well it demonstrates the course objectives for your chosen option. Specifically:

| | Does not yet meet | Meets | Exceeds |
|---|---|---|---|
| **Objective understanding** | Objectives are not clearly addressed | Work demonstrates each listed objective with concrete evidence | Work demonstrates deep understanding, e.g., explaining tradeoffs or limitations |
| **Technical execution** | Code doesn't run, or results are not shown | Code runs, produces correct results, and is clearly explained | Code is clean, well-organized, and handles edge cases thoughtfully |
| **Communication** | Report is hard to follow or missing key sections | Report is clear, well-structured, and walks the reader through the work | Report is polished, insightful, and portfolio-ready |
| **Reflection** | Reflection is superficial or missing | Reflection shows genuine engagement with what was learned | Reflection connects the work to broader ideas or identifies meaningful next steps |

## Submit

- Submit your Jupyter Notebook to Moodle by **Friday, March 6**.
- Make sure you Restart your notebook and Run All before submitting.
- If your project requires data files or API keys, include instructions for how to set them up (but **do not commit API keys** to your notebook — use environment variables or a separate config file).
- If working in a pair, **both partners submit**, and note your partner's name at the top of the notebook.
