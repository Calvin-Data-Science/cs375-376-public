---
title: "Syllabus"
revised: 2025
---

This is a pair of hands-on courses on AI systems using machine learning, with a particular emphasis on deep neural networks.

- **Instructor**: [Ken Arnold](https://kenarnold.org), Calvin University, North Hall NH298
- **Studio Meeting Times**: MWF 11:00am-12:05pm, SB 343
- **Review/Coding Hours**: Tuesdays 2-3pm in Syslab (SB 337). Other times to be arranged on request. Or message me directly; time permitting, I'd love to chat.

The pair is composed of two half-semester courses: CS 375 and CS 376. It is designed so that students who can only take 2 credit hours can take only CS 375 and finish at Spring Break, while students who are able to go in more depth can continue to CS 376. (Although not recommended, it is technically possible to take only CS 376. But we highly recommend taking the two courses in sequence.)

## Objectives

CS 375 focuses on fundamentals; CS 376 dives into generative AI. But both courses are organized around the same 4 key pillars of modern AI: neural computation, ML systems, learning, and context/implications.

(Note that most interesting concepts live at the intersection of pillars, so the descriptions below should feel like they overlap somewhat.)

The key questions in each pillar motivate why we should care about studying that topic. The key objectives are specific things we can show that we can do as a result of studying that topic.

<!-- OBJECTIVES -->
### Neural Computation

Today's ML systems are a mashup of two kinds of computational objects: the traditional sequential programming that we're used to is still usually the "outer loop" of an ML system, but that code is the caretaker for a very different kind of animal: a highly parallel vector computer controlled by billions of parameters. This pillar is about understanding how that parallel vector computer works and how we can control it.

#### Key questions

- 375:
  - How do neural nets compute? (How does that differ from traditional programming?)
  - What are the "data structures" of neural computing and efficient operations we can do with them?
  - How can we update parameters to optimize an objective function?
- 376:
  - How can we represent text, images, and other data as sequences?
  - How can we process and generate sequences using neural nets?
  - How can models capture and use nuanced long-range relationships?

#### Key objectives

After this course, I will be able to:

- 375 (5 objectives, 3.75 required for B, 2.5 for C):
  {{< objectives "Neural Computation" 375 >}}
- 376:
  {{< objectives "Neural Computation" 376 >}}

Not core objectives, but useful for understanding the field:

- State-space models
- Quantization and pruning
- Key-value caching

### ML Systems

#### Key questions

- 375:
  - What are the inputs to and outputs of AI systems?
  - What abstractions do systems provide, and how can they compose? (ML APIs)
  - How do we evaluate ML solutions?
- 376:
  - How do we evaluate language models?
  - Can I run an LLM on my laptop? Can I train one?
  - How do I get good-quality results from an LLM?
  - How can I use an LLM to make a (semi-)autonomous agent?

#### Key objectives

After this course, I will be able to:

- 375 (7 objectives, 5.25 required for B, 3.5 for C):
  {{< objectives "ML Systems" 375 >}}
- 376:
  {{< objectives "ML Systems" 376 >}}

### Learning Machines

#### Key questions

- 375:
  - How can systems improve from experience?
  - What can be learned from data vs interaction?
  - How can we evaluate learning: does it generalize?
- 376:
  - How can we learn without labeled data? (self-supervised learning)
  - How do *foundation models* learn generalizable patterns from massive datasets?
  - How can generative agents learn to improve their behavior from feedback?
  - Some current models can learn at *test time* (e.g., in-context learning); how does this work?

#### Key objectives

After this course, I will be able to:

- 375 (6 objectives, 4.5 required for B, 3 for C):
  {{< objectives "Learning Machines" 375 >}}
- 376:
  {{< objectives "Learning Machines" 376 >}}

### Context and Implications

CS 375 and 376 will investigate broader contexts and implications of AI from many lenses.

#### Key questions

- What problems can we use AI to solve?
- What *should* we use AI for?
- What are the limits of AI systems? Is superhuman AI imminent?
- What might happen socially when AI systems are deployed broadly? (effects on work, education, creativity, ...)
- How might we design AI systems to align with human values? to honor each other and our neighbors? What are the risks if we don't?
- How do privacy and copyright relate with AI? Is generative AI all theft?
- What is creativity? Agency? Truth?

#### Key objectives

The implications of AI are vast, so we will not attempt to cover everything in this course. Here are the basic objectives that we will aim for:

- 375:
  - Recognize when an AI system might have negative impacts on people and flag the need for careful analysis before deploying such a system. [CI-Basic-Impact]
  - Explain basic AI concepts to a non-technical audience without major errors. [CI-Basic-Explain]
  - Identify, in general sense, some ways in which reformed Christian concepts apply to AI development and deployment. Specific examples might include: shalom, humanity in the image of God, and the creation-fall-redemption-restoration narrative. [CI-Basic-Faith]
- 376:
  - I can identify common types of failures in LLMs, such as hallucination and bias. [CI-LLM-Failures]

Beyond the basic objectives, students will have opportunities to explore a variety of types of broader contexts and implications of AI. Students will generally choose two specific areas of depth (for 25SP, we're only requiring one of these). Areas include:

- **Philosophical and Theological**: I can identify and discuss relevant theological narratives and philosophical questions. (Overall: what does it mean to be human?) [CI-Topic-PhilNarrative]
-	**Social, Organizational, and Legal**: I can identify societal implications of AI technologies and recall relevant facts. I can deeply analyze real-world problems to identify how AI could be used or misused in those situations. [CI-Topic-SocAnalyze]. I can evaluate specific design and evaluation choices in AI systems' based on how they relate to human contexts (organizations, societies, etc.) in which those systems might operate. [CI-Topic-SocEvaluate]
- **Dispositional and Visionary**: I can identify and demonstrate strategies that support my practice of dispositions such as integrity, humility, meticulousness, creativity, responsibility, perseverance / continuous technical learning / growth mindset. I can envision value-aligned technological futures involving AI. Practically, I can use generative AI in ways that honor others, help me think better, and help me serve others better. [CI-Topic-DispIntegrity, CI-Topic-DispVision]
- **Historical**: I can trace current AI technologies and ways of thinking back to origins and developments of at least a decade ago. [CI-Topic-History]

> Specific topics may include:
> 
> - sustainability (energy usage of data center construction and operation, ...)
> - impacts on relationships and social interactions
> - privacy and surveillance; data collection and aggregation
> - Human-AI interaction (over-reliance, resilience to errors, paradoxes of automation)
> - recommendation systems and the economies of attention and intention
> - impacts on education
> - perception, categorization, and algorithmic decision-making
> - intellectual property and legal considerations around Generative AI

### Optional Topics

I encourage students to research and share material on these and other AI-related topics:

- Robotics and human-robot interaction
- Computer architecture considerations for neural networks (e.g., memory bandwidth)
- Hardware architectures optimized for neural networks (e.g., TPUs, CUDA), energy efficiency analysis
- Quantization, pruning, and other techniques for practical implementation under constraints
- Stochastic optimization algorithms beyond those covered in class
- Distributed training/inference abstractions and tooling

## Prerequisites

A background at the level of either CS 212 or DATA 202 will be be generally expected. Beyond that, students should come to this course with some (perhaps rusty) ability to:

- Read and write Python code (or be willing to invest significant energy the first few weeks picking it up)
- Think systematically, generate and test hypotheses to explain observations, and communicate that thinking in precise language
- Manage time, individually and in small groups
- Collaborate to solve problems

Although CS 375 is not a formal prerequisite for CS 376, students who do not have a solid understanding of the objectives of CS 375 should be prepared to proactively identify and fill in those gaps as they arise.

## Materials

- 375 Textbook: [Deep Learning with Python, Second Edition](https://www.manning.com/books/deep-learning-with-python-second-edition?a_aid=keras&a_bid=76564dff) by [François Chollet](https://fchollet.com/)
  - Suggestion: get the print version, it's only slightly more than the e-book and includes the e-book.
  - There is a 3rd edition in progress; the chapters we're using are already released in the e-book but you won't get the print version until the full book is released, expected March 2025.
- 376: We will not be using a formal textbook, but we will draw from resources such as:
  - [Understanding Deep Learning](https://udlbook.github.io/udlbook/) by Simon J.D. Prince
  - [Build a Large Language Model (From Scratch)](https://www.manning.com/books/build-a-large-language-model-from-scratch) by Sebastian Raschka
  - [Hands-On Large Language Models](https://www.llm-book.com/) by Jay Alammar and Maarten Grootendorst, and other references from [Jay Alammar's blog](https://jalammar.github.io/)
- Moodle contains links to all of the resources used in this course. It will also be where you engage in discussion forums and submit assignments.
- We'll generally run code on either Kaggle or [Google Colab](https://colab.research.google.com/). If you use Colab, you can choose to log in with your Calvin credentials or use a personal Google account.

## Policies

### How will the course be graded?

I designed the grading scheme of this class to:

- Be simple and clear.
- Balance flexibility with structure.
- Generally trust you to be honest adults.

{{% details summary="CS 375 Grading Scheme" %}}

The course grade is determined by the number and breadth of objectives that are fulfilled. The list below gives a tentative mapping of objectives to letter grades; the final mapping will be determined collaboratively at the conclusion of the class and may require exceptions in special cases.

- A: at most one missing objective in any of the 4 pillars AND at least 2/3 of PPP points
- B: no fewer than 3/4 of the objectives satisfied in each of the 4 pillars AND at least 1/2 of PPP points
- C: no fewer than half of the objectives satisfied in each of the 4 pillars AND at least 1/3 of PPP points
- D: at least one objective satisfied in each of the 4 pillars AND at least 10% of PPP points.

Note: For the Context and Implications pillar, only one "Topics" pillar is required. For example, if you cover none of the Topics objectives but all of the Basic objectives, you can still earn an A. Likewise, if you cover a Topics objective, you can miss a Basic objective and still earn an A.

> Note: There was some inconsistency about how we'd verbally discussed the A-level grade in class. If your understanding was different from the above, please discuss that in the self-assessment (described below).

Other requirements ("should" means "strongly encouraged", but not strictly required):

- At least one objective in each pillar should be met by a project. (You can meet multiple objectives across several pillars in a single project, so you probably only need one bigger project or a few mini-projects.)
- At least two project objectives should be met *before the final week of class*. (i.e., avoid last-minute work).
- At least one objective in each pillar should be met through a discussion with the instructor.

If most but not all criteria of one grade level are met, a `-` should be assigned to that grade. If some but not all of the criteria of the next grade level are met, a `+` should be assigned to the original grade.

At the end of the course you will submit a **self-assessment** document where you will reflect on your understanding of AI according to the objectives listed above. We will attempt to track completion in the Moodle gradebook, but since Moodle was designed for traditional bucket-of-points grading, it will not track perfectly. So **keep track of your progress on your own** and include the grade that you have demonstrated in your self-assessment, along with references to items in your portfolio that demonstrate that competency.

For a rough illustrative example (not meant to be prescriptive or override the criteria above), the following might characterize the sort of student who would earn a C in this course:

- Can use an AI API in contexts very similar to those explored in class (but doesn't think deeply about whether it's appropriate)
- Can discuss superficially how an AI system can learn from training data (but doesn't draw implications beyond that)
- Can give a general example of what the input and output of an AI system is and what processing the system generally does (but the descriptions are vague, can't actually perform the computations by hand or in code)
- Can match a clearly specified ML task with an appropriate performance metric; doesn't confuse regression with classification even if the classes happen to be encoded numerically (but doesn't deeply consider real-world implications of this metric, i.e., what it means practically for a model to perform well by that metric)
- Applies data splitting techniques (at least train-test) without being explicitly instructed to do so; doesn't train on the test set.
- Can list several categories of social and contextual questions (such as bias, privacy, interpretability, etc.), but describes them generically; can't draw implications in specific situations. Can mention some generic principles from the reformed Christian tradition that might apply to those categories, but doesn't make specific connections.

{{% /details %}}

{{% details summary="CS 376 Grading Scheme" %}}

- The list of objectives is given in the Objectives section above, under headings marked 376.
- Students can meet objectives at three levels: "progressing" (P), "met" (M), and "excellent" (E).
  - The Progressing (P) level can be met by assignments (such as lab notebooks and discussion forums). The instructor will track these and ensure that there is an assignment corresponding to each assessed objective.
  - The Met (M) level requires either an *in-class quiz*, an *interaction* (with the instructor, or perhaps with a chatbot or a peer), or a self-directed *project*.
  - The E level is given at instructor discretion to work that demonstrates understanding, strategy, or disposition that is likely to generalize robustly beyond this scope of course. As a concrete example, a successful interview for a ML-centered job would demonstrate E-level completion of an objective.
  - The instructor may limit the number of objectives that can become Met in a given week. So students are strongly encouraged to Meet objectives promptly.
- The course grade will be determined by 3 factors:
  - The number of objectives met at each level: 
  - The quality of the course project.
  - PPP (completion) credits

Specifically, we propose to compute the final grade as a weighted mean:

- 10%: PPP points (instructor may adjust the denominator depending on how this category is affecting the course grade)
- 20%: course project (see rubric for detailed specs, but rubric will be set so that C = checks all the minimum boxes, B = also connects substantively to course objectives, A = sufficient quality to publish as an academic paper or blog post)
- 70%: course objectives, computed as the mean of all objectives scores, where 0 = not addressed, 1 = P achieved one time, 2 = P achieved 2 times, 3 = M achieved, 4 = E achieved. This average (0-4) will then be rescaled to the 0-100 scale such that 1 = D+, 2 = C+, 3 = B+, 4 = 100%.

For example:

An M in all course objectives, a B-level project, and full participation = (.1 * 1.0) + (.2 * .85) + (.7 * .89) = 89.3%, a B+, so any effort to achieve an E will push the grade up to A-.

This grading scheme addresses the following problems with the CS 375 grading scheme:

1. It was not sufficiently clear what it meant to meet an objective.
2. Demonstrations of objectives piled up at the end of the course.
3. No distinction was made between meeting an objective superficially and meeting it deeply.
4. The Context and Implications section was not well-integrated with the rest of the course.
5. The breadth requirement (across pillars) added unnecessary complexity.

{{% /details %}}

### How do I demonstrate that I've met objectives?

You can demonstrate that you've met an objective through a *reflection in a project*, a *meeting with the instructor*, or a screen recording of a *chatbot conversation*. See ["How to Demonstrate Objectives"](../demo_objectives.md) for details.

**Graduate students** taking this course will be graded on the same overall criteria, but with more rigorous expectations for what it means to meet an objective. For example, graduate students should curate a portfolio at a level of completeness and refinement that they could present to a potential employer. Their work should also demonstrate engagement with primary sources and more rigorous evaluation, both quantitative and qualitative, of their own and others' work.

### Preparation, Practice, and Participation (PPP)

As a community, we will undertake many activities that don't directly demonstrate proficiency but are important for shaping our community and retaining what you've learned.

PPP activities are graded by completion, not content. Any legitimate effort by the due date will be awarded a completion credit. Late completion is okay (but frowned on) for solo activities but not for community activities. In some cases the same activity will have multiple occasions of engagement (e.g., posting a comment and responding to others' comments); in that case, each occasion will receive a PPP activity point.

### Are Incomplete grades offered?

An incomplete grade (I) will only be given in unusual circumstances, and only if those circumstances have been confirmed by the Student Life office.

### Do I have to come to class?

Attendance is not mandatory, but highly encouraged, both for your own learning and as one of the main ways to contribute to other students' learning. Come to class:

- to ask the questions that you think everyone else already knows the answer to (but in fact they nod in agreement because they were wondering that too).
- to help your fellow students figure out that thing that just clicked for you yesterday.
- or just because you want to discuss AI!

Also note that many in-class activities will earn PPP points, so if you miss many class meetings you may have difficulty earning a high grade.

### I have some special needs; will you accommodate them?

**Disabilities**: Calvin University is committed to providing access to all students. If you are as student with a documented disability, please notify a disability coordinator in the Center for Student Success (located in Spoelhof University Center 360). If you have an accommodation memo, please come talk to me in the first two weeks of class. **If something comes up mid-semester, like an injury, please reach out to the disability coordinator and me.**

### How do I demonstrate academic integrity in this class?

The primary purpose of exercises in this class is to help you *learn* the material. The primary purpose of assessments are to help you *retain* the material. Academic integrity entails using course materials for the purposes that they were designed, not bypassing those purposes in an attempt to obtain answers without effort or demonstrate performance without learning.

Moreover, your work in this class should demonstrate *gratitude* and *respect* to those whose work enables yours. It should demonstrate the *integrity* necessary to produce work that your future employer can legally use. And it should demonstrate an active embrace of the often-necessary struggle of figuring things out yourself. So I expect you to *credit the people who help you*, be they classmates or StackOverflow strangers, and *heed the license terms* under which they offer their code.

Solutions to exercises are easy to find. You are expected *not* to refer to them until after you have submitted your work. If you do refer to them, you are *required* to clearly indicate that you have done so within the assignment.

If you realize that your actions have violated academic integrity principles, please let the instructor know as soon as possible.

**Etiquette**: We expect you to treat students and instructors for this with respect by adopting courteous communication practices throughout the course. No personal attacks, trolling, bad language will be tolerated.

## How should we use AI in this course?

Thoughtful use of all types of AI is highly encouraged in this class. However, you should be capable of fulfilling most of the class objectives without AI assistance.

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
