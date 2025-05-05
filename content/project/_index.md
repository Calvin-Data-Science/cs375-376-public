---
title: "Project (CS 376)"
toc: true
revised: 2025
---

Instead of a final exam, our course will culminate in a final project.

## Objectives

Successful projects will demonstrate that you can:

- **Apply fundamental machine learning concepts and principles** to the task of designing, implementing, and/or analyzing intelligent systems. Your work should demonstrate a deep understanding of the underlying concepts, rather than simply copy-pasting existing solutions. Consider the suggestions provided below.
- **Implement and/or experiment** with a system that uses ML. 
- **Communicate your work** using text and visuals that are precise, concise, and appropriate for the audience.

Successful projects will also demonstrate competency in various other skills, but the specific skills will vary between people and projects. Some options include:

- systematic experimentation
- detailed understanding of model architecture and functionality
- structuring (or wrangling) data
- detailed assessment of model performance
- systematic exploration of variations (parameter choices, architecture choices, data choices, etc.)
- Clean coding
- Efficient coding
- ...many others are possible.

You are encouraged to try to demonstrate competency in several of these topics even before the final project submission. Please either write a note or arrange a brief meeting.

## Choosing a Project

The [choosing-a-project](/project/proj-choice) page has some suggestions for project types.

### Rubric

{{% details summary="Rubric" %}}

This rubric is a rough guide; adjustments may be made based on the specifics of your project. The [choosing-a-project](/project/proj-choice) page has some details about evaluation of different types of projects.

Since different projects will have different emphases, projects wil lbe graded holistically based on their contribution to your portfolio:

- A = I could write you a recommendation letter based on this work
- B = you should definitely include this in your portfolio
- C = you could include this in your portfolio, but not if you have better work
- D = you should probably not include this in your portfolio

Here are some ways that projects can demonstrate these levels of quality. The strongest projects will demonstrate several of these.

- **Connecting to fundamental ML concepts**. You can dig below the surface in some way. For example, your report might include a *substantive* discussion of:

    - why a model (or hyperparameter of some model) was chosen by discussing how the model aligns with the task
    - analyzing what kinds of errors the model makes and why that might or might not make sense in light of the architecture
    - how a choice of loss function, training data, evaluation approach, etc. impacts the outcome
    - how a model type that was not covered in detail in class actually works (ideally with some specific examples)

- **Evaluation**, both quantitative and qualitative. Don't just say it works, measure it. For example, you might:

    - compare the performance of two or three different approaches to a task (e.g., simple baseline method you implemented, state-of-the-art method that someone else implemented, and simple tweak to the baseline method that improves it a little)
    - quantitative (numbers that measure performance) and qualitative (specific examples of what the model does well or poorly)
    - robustness analyses

- **Real-World Connections**:

  - Why is this project interesting? What is the real-world problem that it addresses?
  - What choices are you making *because of the real-world problem*?
  - Connect your results about system performance to the real-world problem.
  - Are there any decisions that you might make differently because of ethical considerations? Be specific!

- **Communication: Decisions and Rationale**

    Explains what decisions were made during the project why they were made, and possible alternatives.

    This is usually done *throughout the report*, i.e., "We chose to use model [name of model] because [characteristic of the task]; reasonable alternatives might have been [other model name] or, if we thought of the problem as a zero-shot classification task, we could even have used [very different kind of model]"

    The strongest reports will discuss the results in terms of how they relate to these choices, e.g., what choices probably mattered a lot to the results; what other choices might have worked out better (thus future work).

    You might have several sections of code or experimentation. A general structure for each one might be:

    - Say what you're trying to do
    - do it (describing important decisions and milestones along the way),
    - then discuss what you did and what you observe from it.

    On a high level, you might structure your report like:

    - we want to do X
    - so we adjusted Y
    - and we observed difference Z
    - which tells us ______ about the relationship between X and Y
    - so, were we successful at X? (and why or why not?)

- **Clear communication of results**:

  - Good visualizations, tables, textual summaries, examples, etc.
  - Connect the results to the real-world problem.

- **Clear discussion of limitations and future directions**

  - Not just "I ran out of time to do X", but "these results assume that Y is true, but in the real world, some cases where Y might not be true are [examples]."
  - What are the implications of this? What would you do next if you had more time?
  - Specific limitations of the chosen approach are discussed (e.g., "our dataset only had examples of X, so we couldn't test how well the model generalizes to Y")
  - Ethical considerations are specific, e.g., rather than generic concerns about bias, the report gives specific examples of biases that might be present and what the consequences might be.
  - Future directions are plausible and described in enough detail that someone else could pick up the project and run with it.


Minimum expectations:

- **Report**: 
  - [ ] The report is well organized (has a clear logical flow, uses headings to indicate sections, etc.)
  - [ ] It has no major writing issues.
  - [ ] The report is concise (any unnecessary information or outputs are moved to an appendix or removed)
  - [ ] The report is understandable without reading the code.
  - [ ] All resources that were used (except for provided course materials) are clearly cited.

An excellent project could become a submission to an academic conference or a blog post. At the very least it should be a good portfolio piece.

{{% /details %}}

## Teams

- Ideally 2 or 3 people
- ... who can commit to work synchronously at least once a week
- Each member should be able to clearly document their role (see "Deliverables" below)
- Post in the Moodle discussion forum for help finding teammates


## Milestones

To show progress:

1. Submit your project report early, nearly blank but with a clear vision statement, and submit updates to it as you progress.
2. Include an update on your project progress in your weekly reflection.

## Final Deliverables

### Presentation

The final course meeting (during the designated final exam period) will be devoted to final project presentations. Feedback on others' projects is expected, so attendance is mandatory.

Presentations should communicate the key points (not every detail) of your project, such as:

{{% details summary="Example Presentation Outline" %}}

- What **problem** are you trying to solve?
- **How you approached** that problem:
  - How did you frame the problem in a way that you could apply a model to answer?
  - what model did you use, what did you train/fine-tune on, etc.?
  - How did you turn model's outputs into something useful?
- What **results** did you get?
  - Include both specific examples and summary numbers, if applicable.
  - This would be a good place to give a demo -- but maybe record a video in case it doesn't work.
- What did you **learn**? you could take this in various ways:
  - about your problem?
  - about the model or data you're using?
  - about AI/ML more generally?
  - about your problem-solving process?
  - etc.
- What should others take away?
  - If someone in the audience gets asked "what was that presentation about?", how would you want them to answer?
  - What are some limitations of your project?
  - What broader questions might your project raise? How might you contribute to the discussion?
  - What might you do next?

{{% /details %}}

Slides are not strictly required (you could talk as you scroll through a notebook) but are probably helpful. Aim for 5 minutes of content. All team members should participate.

{{% details summary="Example Presentation" %}}

Here is an [example presentation](https://docs.google.com/presentation/d/1WVWa32uvPxat12nuemBX2Pjo19EAKnUKbwjaGpkOR_M/edit#slide=id.p) that I threw together. Self-critique:

- The Goal slide is ok, but it's not clear what the example is showing.
- Approach slide diagram could be clearer, with more intentional use of color.
- Details slide may be too dense; the code screenshot might not be helpful.
- Evaluation is quick and dirty and not finished. (But it's a good idea to show some results, even if they're not great.)

{{% /details %}}

By the **end of the day of final presentations**, submit the following:

-   A technical report on the project. This can be your Jupyter notebook file, or you may use a different technology if you want to include results that don't fit in a notebook easily.
-   A **short explanation of the technology you build on** for a nontechnical audience.
-   Supporting materials, including code/notebooks, as appropriate

The following sections provide additional detail about each component.

### Technical Report

The report should be at the level of polish and formality of a blog post (more than a class homework assignment, less than an academic paper). Precise technical language should be used in descriptions of methods.

- Audience:
  - The introduction and conclusion should be written for a general audience (friends and family, for example).
  - The rest of the report should be written for someone who is familiar with AI / machine learning in general but none of the specific software used (e.g., `keras` or Hugging Face `transformers`).
- Explain your overall approach and the choices you make along the way.
  - The report should still make sense if all of the source code is hidden. (i.e., don't use code comments to explain what you're doing or why)
  - Use Markdown (text) cells appropriately, e.g., to format headers (`## Header`) and links.
-   Submit your work as a Jupyter Notebook (`.ipynb`) file if possible.

{{% details summary="Example Report Structure" %}}

Reports should be organized in a way that makes sense for your project. The following is a general outline of what a report might look like. You can use this as a starting point, but feel free to adjust it to fit your project.

- A succinct but descriptive **title**
- A **real-world question or goal** and *why* it's interesting.
- A description of the **dataset**: what sort of data does it contain? Where did it come from? Why did you choose it? What are its strengths and limitations?
- A specific technical goal or question
- Your technical **approach** for achieving that goal or answering that question
- What you noticed from **exploring the data** (e.g., counts by category, distributions of continuous variables, things you notice from inspecting individual samples at random)
- Your **modeling setup**: what are your features? Targets? Metrics? Loss function?
- Your **validation approach**: train-val-test split? cross-validation?
- Your **baseline results**: applying the simplest model you can think of; how good were the results (quantitatively and perhaps qualitatively)?
- Your **attempts at improved results**: what did you adjust, and why? How did the results change?
- An **analysis of errors** (quantitatively and perhaps qualitatively)
- **An analysis of the effects of alternative choices.** You can consider differences in model architecture, specific task, hyperparameter choices, inclusion/exclusion criteria, etc. Remember to think about the choice of **metrics** and the **uncertainty** involved in any estimate of them.
- A **summary of your findings**. Did you achieve your goal or answer your question?
- **Limitations and future directions**

Artistic or exploratory projects may need other elements.

Checklist:

- [ ] Describes **why** you made various decisions
- [ ] Backs up claims with **evidence** (e.g., numbers, examples)
- [ ] Cites **sources** for any ideas that are not your own (and describes what you took from each source)

{{% /details %}}

### Reflection

Write an individual reflection (about a page or should suffice) discussing:

1. Which *course objectives* do you think this project demonstrates? For each one, write a sentence or two about how you think it demonstrates that objective. (You can find the course objectives in the [syllabus](/syllabus/).)
2. How does this project fit into your portfolio? What **technical skills** do you want it to demonstrate? **What makes it high-quality**?
3. Imagine discussing this project in a technical job interview. What question does the interviewer ask? What's your response? (Ask an LLM for feedback on this one.)
4. What was your role or contribution to the project (if it was a team project)? Look at some examples of Author contributions statements, such as [this one](https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html#author-contributions).

A few other things you could optionally include in the reflection:

- A summary of the main things you learned from the process of doing the project.
- Superlatives (pick a few): most fun part? most proud of part? frustrating? surprising? interesting? challenging? rewarding? most useful part of the course for your project? 
- Wishes: what would you do differently next time? advice for someone else doing a similar project? material you wish you had learned in the course?


### Supporting Material

Submit code needed to replicate the visual and quantitative results in your report.

- Share any github repos with `kcarnold` or make them public.
- Include the notebooks you used.
  - If you used Colab, download the `ipynb` file.
  - "Restart and Run All" before submitting, if possible.
  - The technical report may include all of the needed code; if so, nothing more is required.
- Include clear instructions for how to acquire any data you used. (Don't upload the dataset itself, unless it happens to be very small.)

## General Advice

- **Repeat trials** with different random seeds. Consider the variability of results.
- **Notice decisions** you make during data prep and modeling.
  - What data did you omit?
  - How did you set up the modeling problem?
  - What’s missing?
- **Analyze errors**
  - What systematic mistakes did the model make?
  - What effect did decisions have on those mistakes?

Technically: **keep it simple**. A thoughtful analysis of a technically simple thing is much better than a hasty analysis of a technically fancy thing.

See the Resources page here, especially [Tools](/resources/#tools).


<!--

Feedback:

Have you found existing work that you\'d replicate?

I agree that a Kaggle competition would be good for you. Maybe warm up on a closed competition to get used to how it works, then jump to a live one when you feel ready?

For tabular data, get a random forest running first, then try xgboost, and only after that go for anything more complicated.

All three look pretty good. The house prices competition is going to be the most straightforward but hardest to make interesting, because there\'s been so much done on that competition already, and the data isn\'t super-rich.

Prompt engineering is pretty cool overall. See https://arxiv.org/abs/2106.13884 for a simple approach to that idea.

I think the landscape generation one seems promising because the approaches are similar to what we've been working with already in class, and the results can look cool, and you have opportunity to control the inputs and intermediate results in interesting ways too.

Note that there have been lots of other papers since the Taming Transformers paper (which I added to the replication ideas list last year); you could do a little Google Scholar citation tracking (or browsing on paperswithcode) to find a good starting point to work from. 

I wrote up some general comments about replication projects that might help you here: https://cs.calvin.edu/courses/cs/344/22sp/project/#choosing-a-replication-project


General notes to everyone:

- this is rough feedback on project proposals. I probably haven\'t clicked on any of your links or thought deeply about what issues you might encounter.
- A positive reaction to one of your project ideas isn\'t necessarily a negative reaction to the others, but I am going to try to pick the project that I think will work out best.

-->