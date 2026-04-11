---
title: "Syllabus"
revised: 2026
---

This is a pair of hands-on courses on AI systems using machine learning, with a particular emphasis on deep neural networks.

- **Instructor**: [Ken Arnold](https://kenarnold.org), Calvin University, North Hall NH298
- **Meeting Times**: MWF 11:00am-12:05pm, SB **343**
- **Review/Office Hours**: **Thursdays** 1:30-3pm in NH 298 (or sometimes the Syslab, SB 337). Other times to be arranged on request. Or message me directly; time permitting, I'd love to chat.

The pair is composed of two half-semester courses: CS 375 and CS 376. It is designed so that students who can only take 2 credit hours can take only CS 375 and finish at Spring Break, while students who are able to go in more depth can continue to CS 376. (Taking only CS 376 is highly discouraged. Taking CS376 in a different year from CS375 is mildly discouraged.)

## Course Descriptions

Note that these descriptions were revised in Fall 2025 and may not have made it into the official catalog yet.

### CS 375 - Machine Learning

An introduction to artificial intelligence through machine learning, with an emphasis on deep neural networks. Students learn how neural networks compute and are trained, how to implement and apply them to tasks such as image classification, and how different learning approaches (supervised learning and reinforcement learning) address different types of problems. The course emphasizes hands-on implementation, evaluation of system performance, and discernment of philosophical, psychological, historical, and religious aspects of AI systems. Prerequisites: DATA 202, MATH 255, and either STAT 243 or STAT 343 (or permission of the instructor). Lab fee.

### CS 376 - Advanced Machine Learning

Building on CS 375, an in-depth study of modern generative AI systems, with an emphasis on large language models (LLMs) and transformer architectures. Students examine how these systems are built, trained, and deployed; implement core architectures from fundamental components; learn practical techniques for building and evaluating ML-powered applications; and discern the philosophical, psychological, historical, and religious contexts and implications of generative AI. Students learn to view diverse data types (text, images, audio) as sequences of tokens processed by neural architectures. The course emphasizes hands-on experience with contemporary tools and APIs. Prerequisite: CS 375. Lab fee.


## Objectives

### CS 375 – Machine Learning

Upon successful completion of this course, students will be able to:

1. **Frame machine learning problems** by identifying appropriate learning paradigms (supervised, self-supervised, reinforcement learning), task specifications, loss functions, and evaluation approaches
    - OG-ProblemFraming-Supervised
    - OG-ProblemFraming-Paradigms
    - OG-LossFunctions
    - OG-DataDistribution
2. **Explain the computational mechanisms** of neural network training and inference, including forward propagation, loss computation, and gradient-based optimization
    - TM-MLPParts
    - TM-LinearLayers
    - TM-ActivationFunctions
    - TM-Softmax
    - TM-DataFlow
    - TM-TensorOps
    - TM-RepresentationLearning
    - TM-Embeddings
3. **Implement and train neural networks** for classification and regression tasks
    - TM-Autograd
    - TM-Implement-TrainingLoop
    - OG-Theory-SGD
4. **Evaluate and improve ML systems** by applying validation strategies, diagnosing generalization problems (overfitting, underfitting), and reasoning about data distributions
    - OG-Eval-Experiment
    - OG-Implement-Validate
    - OG-Generalization
5. **Work with diverse ML approaches** including supervised learning models, pretrained models via APIs (e.g., large language models), and reinforcement learning concepts
    - OG-Pretrained
    - OG-LLM-APIs
6. **Analyze and articulate** philosophical, historical, and religious aspects of AI systems, including appropriate use cases, limitations, and potential societal impacts
    - Overall-Explain
    - Overall-Faith
    - Overall-PhilNarrative
    - Overall-Impact
    - Overall-Dispositions
    - Overall-History (optional)

Here are the [specific objectives used for course grading](/objectives-375).

### CS 376 – Advanced Machine Learning

Upon successful completion of this course, students will be able to:

1. **Explain and implement** the architecture and computational mechanisms of contemporary machine learning architectures
    - TM-LLM-Embeddings
    - TM-SelfAttention
    - TM-TransformerDataFlow
    - TM-LLM-Generation
    - TM-Architectures (bonus)
2. **Describe the approach and computational requirements** of training and using modern generative AI systems, including pre-training, tuning, and learning from feedback
    - OG-LLM-Train
    - OG-SelfSupervised
    - OG-Theory-Feedback
    - TM-LLM-Compute
3. **Work with pretrained models** using both low-level and high-level APIs to build AI-powered applications
    - OG-LLM-Tokenization
    - OG-LLM-ConversationAsDocument
    - OG-LLM-Prompting
    - OG-LLM-ContextAndTools
4. **Evaluate generative AI systems** and identify common types of failures
    - OG-LLM-Eval
    - Overall-LLM-Failures
5. **Analyze and articulate** philosophical, psychological, historical, and religious aspects of AI systems
    - Overall-Impact
    - Overall-PhilNarrative
    - Overall-Faith
    - Overall-Dispositions

Here are the [specific objectives used for course grading](/objectives-376).

## Topics

1. **Problem framing for machine learning**: Agent framework (environment, state, action, reward); supervised learning and reinforcement learning as different learning paradigms; task specification; evaluation metrics; considerations of data and appropriate use cases

2. **Neural computational architecture**: Computational building blocks (linear layers, activation functions, loss functions); the multi-layer perceptron (MLP) architecture; vector/matrix/tensor data and operations; embeddings and representation learning; gradient descent algorithms; backpropagation / automatic differentiation

3. **Implementation and training**: Implementing neural network primitives; training loops; stochastic gradient descent; validation strategies; diagnosing and addressing common training problems; low-level implementation in computational notebooks using PyTorch

4. **Applications of machine learning**: Design decisions in applied contexts; transfer learning; evaluation in practice; at least one substantial application (e.g., image classification with exploration of architecture choices, data augmentation, and hyperparameter tuning); also, use of LLM APIs for simple tasks.

5. **Perspectives on Artificial Intelligence**: Historical developments (from Turing to contemporary AI); philosophical questions (consciousness, intelligence, Chinese Room); religious and theological themes (imago Dei, technology and human relationships); societal impacts (bias, privacy, appropriate use); the nature of measurement and reductionism in AI systems


## Pillars

CS 375 focuses on fundamentals; CS 376 dives into generative AI. But both courses are organized around the two key pillars of modern AI: a **tuneable machine** playing an **optimization game**. Both courses also discuss the broader **context and implications** of AI systems.

Our objectives are organized around two main pillars:

- **Tuneable Machines (TM)**: The number-crunching machines that implement neural networks in ways that can be tuned to improve quantitative evaluations of their outputs. *How do these machines work?*
    - The architecture: layers, activations, data flow
    - The mechanics: forward pass, backward pass, training loops
- **Optimization Games (OG)**: How we set up problems in ways that we can solve using tuneable machines? What implications does that have on the real world?
    - Problem setup: supervised vs RL, loss functions, evaluation
    - Training strategy: SGD, generalization, validation

Each objective covers multiple skills:

- Conceptual understanding (explain, describe)
- Implementation (write code, compute)
- Analysis (diagnose, select, compare)

For example, [OG-LossFunctions](objective) asks you to:

- Compute MSE loss (implementation)
- Explain why we use cross-entropy (conceptual)
- Identify which loss fits a task (analysis)


## Prerequisites

A background at the level of DATA 202 (for basic supervised learning), MATH 255 (for working with vectors and matrices), and either STAT 243 or STAT 343 (for thinking about *distributions*) will be be generally expected. Beyond that, students should come to this course with some (perhaps rusty) ability to:

- Read and write Python code (or be willing to invest significant energy the first few weeks picking it up)
- Think systematically, generate and test hypotheses to explain observations, and communicate that thinking in precise language
- Manage time, individually and in small groups
- Collaborate to solve problems

## Materials

- 375:
  - Textbook: [Deep Learning with Python, Third Edition](https://deeplearningwithpython.io/) by [François Chollet](https://fchollet.com/)
   - It's free to read online, and we'll be loading chapters into Perusall for shared commenting.
   - If you'd like a physical copy, you can [buy it from Manning](https://www.manning.com/books/deep-learning-with-python-third-edition) or other retailers.
  - Other materials (optional):
    - [The Thinking Game](https://www.youtube.com/watch?v=d95J8yzvjbQ) documentary (2025)
    - [Artificial Intelligence: A Guide for Thinking Humans](https://www.amazon.com/dp/1250404851) by Melanie Mitchell - recommended inexpensive but good purchase
    - [Speech and Language Processing](https://web.stanford.edu/~jurafsky/slp3/) by Jurafsky and Martin (3rd edition draft, online only)
    - [AI by Hand](https://www.byhand.ai/t/foundation) by Tom Yeh
- 376: We will not be using a formal textbook, but we will draw from resources such as:
  - [Understanding Deep Learning](https://udlbook.github.io/udlbook/) by Simon J.D. Prince
  - [Build a Large Language Model (From Scratch)](https://www.manning.com/books/build-a-large-language-model-from-scratch) by Sebastian Raschka
  - [Hands-On Large Language Models](https://www.llm-book.com/) by Jay Alammar and Maarten Grootendorst, and other references from [Jay Alammar's blog](https://jalammar.github.io/)
- Moodle contains links to all of the resources used in this course. It will also be where you engage in discussion forums and submit assignments.
- We'll generally run code on either Kaggle or [Google Colab](https://colab.research.google.com/). If you use Colab, you can choose to log in with your Calvin credentials or use a personal Google account.

## Policies

### How will the course be graded?

This course will be graded using a hybrid proficiency-based system that is designed to encourage you to bring your whole self to this course. We are not computers, so we shouldn't assess ourselves like computers! But at the end of the day there are some things that we need to be able to *do* to demonstrate our learning.

We first agree to trust each other:

- I trust you to be honest adults who care about your own learning and growth.
- You trust me to design a course that helps you learn and grow, and to provide activities and feedback that helps you do that.
- You trust yourself that *you can learn this material* if you put in the effort. You should not take shortcuts that shortchange your own learning.

The following elements, detailed in the sections below, go into the course grade:

1. **Skills**: You will demonstrate that you can meet specific [objectives](/objectives-375) related to the course material.
2. **Effort**: Each week, you self-report what you spend time on related to this course.
3. **Community**: You will choose a small number of activities to contribute to our learning community.

In a [final "Journal" assignment](/final-journal/), students will propose a final grade based on these three components. The proposed grade should generally follow the guidelines below, but students may argue for exceptions.

#### Skills: Proficiency-Based Grading

The core of the grading system is based on the specific learning objectives for the course. Each objective will be assessed multiple times throughout the course, and students will have multiple opportunities to meet each objective.

- Students can meet objectives at three levels: "progressing" (P), "met" (M), and "excellent" (E).
  - The Progressing (P) level can be met by assignments (such as lab notebooks and discussion forums).
  - The Met (M) level requires either an *in-class quiz* or a self-directed *project*.
  - The E level is given at instructor discretion to work that demonstrates understanding, strategy, or disposition that is likely to generalize robustly beyond this scope of course. As a concrete example, a successful interview for a ML-centered job would demonstrate E-level completion of an objective.
  - The instructor may limit the number of objectives that can become Met in a given week. So students are strongly encouraged to Meet objectives promptly.
- We will aggregate these objective levels in a way that encourages students to aim for M-level completion of most objectives, with some room for P-level completion and some room for E-level completion. Last year we computed this as the mean of all objectives scores, where 0 = not addressed, 1 = P achieved one time, 2 = P achieved 2 times, 3 = M achieved, 4 = E achieved. This average (0-4) will then be rescaled to the 0-100 scale such that 1 = 68% (D+), 2 = 78% (C+), 3 = 88% (B+), 4 = 100% (A+).

![EMP rubric](https://kurmasgvsu.github.io/Teaching/Courses/F24/CIS500/EMPNrubric_notYet.png) by Zach Kurmas at GVSU

The proposed weight for this component is 70% of the course grade.

### Effort Hours

> In-person, 2-credit courses will typically have a ... 195 (3 x 65) minutes of class time and 8 hours of out-of-class student work per week over an 8-week half-semester. Source: [Definition of a Credit Hour](https://calvin.edu/sites/default/files/2025-01/Definition%20of%20a%20credit%20hour%2C%20including%20specific%20considerations%20for%20distance%20learning.pdf), based on [34 CFR 600.2](https://www.ecfr.gov/current/title-34/subtitle-B/chapter-VI/part-600/subpart-A/section-600.2)

Each week, your weekly reflection should account for how you spent each of the 8 hours of out-of-class time. The reflection assignments will give details. This will be on the honor system.

To allow for flexibility between lighter and heavier weeks (since things come up) while still encouraging consistent effort, we will allow a **maximum of 12 hours** reported each week.

Effort grades are computed as total hours divided by total possible hours (7 weeks * 8 hours per week = 56 hours). The proposed weight for this component is 20% of the course grade.

### Community

Every student should be able to identify at least 3 substantial contributions to the course community, with at most 2 credits of any one of the following types:

- Thoughtful contributions to discussions, either in class or outside of class (e.g., Moodle discussion forums). The contribution should be significant enough that another student would credit you specifically for shaping their thinking (it's ok if no one actually does, but that's the level to aim for)
- Substantial contributions to the class's making sense of readings. Same standard as for discussions.
- Presenting a tech update in class
- Organizing a perspectival discussion in class
- Leading an opening devotion.
- Providing substantial feedback on others' work.

The community grade component is computed as `min(1, x/3)`, where `x` is the number of contributions (subject to the limit of 2 per type). The proposed weight for this component is 10% of the final course grade. (Since the course staff did not support the logistics of this component in Spring 2026, students may choose to opt out of this component, in which case the weight will be redistributed to the other two components.)

### Are Incomplete grades offered?

An incomplete grade (I) will only be given in unusual circumstances, and only if those circumstances have been confirmed by the Student Life office.

### Do I have to come to class?

Students are expected to be present at class, both physically and mentally. Why?

- We have turned away students that wanted to enroll because there are not enough seats in the room. If you're not going to come to class, please drop the course so that someone else can take your seat.
- We will do many activities in class that are difficult to make up later.
- Many of the assessments of your learning will happen in class, through quizzes, discussions, and other activities.

Come to class:

- to ask the questions that you think everyone else already knows the answer to (but in fact they nod in agreement because they were wondering that too).
- to help your fellow students figure out that thing that just clicked for you yesterday.
- or just because you want to discuss AI!

That said, things happen: sickness, family emergencies, job interviews, etc. If you must miss class, please notify me in advance if possible, and plan to stop by my office hours as soon as possible to catch up on what you missed.

### I have some special needs; will you accommodate them?

**Disabilities**: Calvin University is committed to providing access to all students. If you are as student with a documented disability, please notify a disability coordinator in the Center for Student Success (located in Spoelhof University Center 360). If you have an accommodation memo, please come talk to me in the first two weeks of class. **If something comes up mid-semester, like an injury, please reach out to the disability coordinator and me.**

### How do I demonstrate academic integrity in this class?

The primary purpose of exercises in this class is to help you *learn* the material. The primary purpose of assessments are to help you *retain* the material. Academic integrity entails using course materials for the purposes that they were designed, not bypassing those purposes in an attempt to obtain answers without effort or demonstrate performance without learning.

Moreover, your work in this class should demonstrate *gratitude* and *respect* to those whose work enables yours. It should demonstrate the *integrity* necessary to produce work that your future employer can legally use. And it should demonstrate an active embrace of the often-necessary struggle of figuring things out yourself. So I expect you to *credit the people who help you*, be they classmates or StackOverflow strangers, and *heed the license terms* under which they offer their code.

Solutions to exercises are easy to find. You are expected *not* to refer to them until after you have submitted your work. If you do refer to them, you are *required* to clearly indicate that you have done so within the assignment.

If you realize that your actions have violated academic integrity principles, please let the instructor know as soon as possible.

**Etiquette**: We expect you to treat students and instructors for this with respect by adopting courteous communication practices throughout the course. No personal attacks, trolling, bad language will be tolerated.

## How should we use AI in this course?

Thoughtful use of all types of AI is encouraged in this class. However, you should be capable of fulfilling most of the class objectives without AI assistance.

### Freedom *not* to use AI

In this class **you always have the freedom to choose not to use AI tools**. In particular, that means that we will grade such that **choosing not to use AI will never lower your grade**.

Practically, this means: if you're ever tempted to take a shortcut by using AI, instead describe what you'd ask for help with. For example, rather than using an AI to polish a discussion post, post the pre-AI version and describe what you would have asked the AI to help with.

Another option to consider is **only using local LLMs** that you can run on your own computer.

### Encouraged Uses

You are encouraged to use AI tools to support your learning process by:

- Requesting explanations and analogies for complex concepts
- Generating practice problems and study questions to check your understanding
- Getting help with coding and debugging
- Breaking down problems
- Discussing how concepts relate

Use a variety of technologies for different purposes: LLMs (ChatGPT, Claude, Gemini, ...), search, speech interactions, image/video/diagram generation.

You are encouraged to use these tools collaboratively with other students and to discuss and share your strategies.

### Cautions and Guardrails for AI Use

It is crucial that you practice evaluating AI outputs criticaly, since they will sometimes be incorrect, distracting, misguided. Dialogue LLMs like ChatGPT are trained to give you answers that **feel** correct and **feel like** they help your understanding.

Avoid using AI to bypass your own thinking and learning. For example, **don't use AI to generate first drafts** for short-answer questions or discussions. Instead, write your thoughts first and ask for AI feedback. Prompts might include "what is unclear or incorrect about my answer?" or "please list phrases in my writing that might be extraneous". **Honor your readers' time and attention**.

If you do at any point include any AI-generated content in something you submit, please make a reasonable attempt to mark what sections are AI-generated and to include what prompts you used. (Your prompts are often more interesting than the outputs!)

## Diversity and Inclusion

I came to Calvin because I wanted to explore what our Christian calling to “act justly” means in the context of AI, data, and the technologies that we use with it. Engaging that question wholeheartedly requires that each of us, me included, engage respectfully with perspectives very different from our own. For example, we must question those who abuse data for selfish gain, but we also must question the perspectives of those who challenge those abuses on purely secular grounds.

I intend for this class to be an environment where we equally respect people of every ethnicity, gender, socioeconomic background, political learning, religious background, etc. I will try to create that community by having us read diverse voices, engage with issues of importance to people unlike ourselves, and structure discussions that require students to engage respectfully with perspectives different from their own. I invite your help.

We will not always do this well. If you or someone else in this class is hurt by something I say or do in class, I would like to work to remedy it. I will welcome this feedback in whatever way is comfortable for you: in public, in private, via another person (such as our TA or my department chair, Keith VanderLinden), or via a report to [Safer Spaces](https://calvin.edu/offices-services/safer-spaces/) or the [provost's office](http://www.calvin.edu/go/comments-on-faculty/).
