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


### Rubric (To Be Updated)

{{% details summary="Rubric" %}}
*This rubric was from last year, we may adjust it for this year.*

This rubric is a rough guide; adjustments may be made based on the specifics of your project. The [choosing-a-project](/project/proj-choice) page has some details about evaluation of different types of projects.

- 20pt: **Concepts: Used fundamental ML concepts**

    The project dug below the surface in some way to connect to fundamental ML concepts. (This is about conceptual understanding, not implementation, although those are related.)

    The report might demonstrate this by a *substantive* discussion of:

    - why a model (or hyperparameter of some model) was chosen by discussing how the model aligns with the task
    - analyzing what kinds of errors the model makes and why that might or might not make sense in light of the architecture
    - how a choice of loss function, training data, evaluation approach, etc. impacts the outcome
    - how a model type that was not covered in detail in class actually works (ideally with some specific examples)

- 20pt: **Implementation and/or Experimentation**

    The project implemented a method not discussed in class, experimented systematically with some existing method, or otherwise did good applied work.

    In many projects, this will be addressed by a thorough *evaluation* of the proposed approach. Evaluations should be both quantitative (numbers) and qualitative (discussing specific examples). A *comparison* between two or three interestingly different approaches is probably good.

- 5pt: **Communication: project goal clear?**

    The report and presentation clearly state the project goal and *connect* it with the technical details of the approach and metrics. Then, the discussion of the results should *connect back* to the goal. (e.g., suppose you got some loss number; does that mean your model succeeded at its goal?)

- 10pt: **Communication: Decisions and Rationale**

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

- 5pt: **Communication: Results**

    It summarizes results clearly, using visuals if possible, and relates those results to overall success at the goal.

- 5pt: **Communication: Limitations and Future Directions**

    It summarizes limitations/caveats, social/ethical considerations, and future directions that could be pursued.

    - [ ] Specific limitations of the chosen approach are discussed (e.g., "our dataset only had examples of X, so we couldn't test how well the model generalizes to Y")
    - [ ] Ethical considerations are specific, e.g., rather than generic concerns about bias, the report gives specific examples of biases that might be present and what the consequences might be.
    - [ ] Future directions are plausible and described in enough detail that someone else could pick up the project and run with it.

- 5pt: **Report and Presentation Craft**

    The report is clear, concise, and well organized, and has no major writing issues.

    In general the reports will be Jupyter notebooks (ipynb) with code included. The results should be understandable *without reading the code*, though.

    - [ ] Overall, the report displays a high degree of *integrity*: claims are backed up with evidence, strengths and limitations are acknowledged.
    - [ ] The report is well-organized, with clear headings and a logical flow.
    - [ ] The report is concise, with no unnecessary information. (e.g., outputs are selected to be informative, rather than large dumps of data)

- 5pt: **References**

    All resources that were used (except for provided course materials) are clearly cited.

An excellent project could become a submission to a conference or a blog post (see [upcoming AI deadlines](https://aideadlin.es/?sub=ML,AI)). At the very least it should be a good portfolio piece.

{{% /details %}}

## Teams

- Ideally 2 or 3 people
- ... who can commit to work synchronously at least once a week
- Each member should be able to clearly document their role (see "Deliverables" below)
- Post in the Moodle discussion forum for help finding teammates


## Milestones and Deliverables

To show progress:

1. Submit your project report early, nearly blank but with a clear vision statement, and submit updates to it as you progress.
2. Include an update on your project progress in your weekly reflection.

{{% details summary="Presentations" %}}

The final course meeting (during the designated final exam period) will be devoted to final project presentations. Feedback on others' projects is expected, so attendance is mandatory.

Presentations should communicate the key points (not every detail) of your project, such as:

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

Slides are not strictly required (you could talk as you scroll through a notebook) but are probably helpful. Aim for 5 minutes of content. All team members should participate.

Here is an [example presentation](https://docs.google.com/presentation/d/1WVWa32uvPxat12nuemBX2Pjo19EAKnUKbwjaGpkOR_M/edit#slide=id.p) that I threw together. Self-critique:

- The Goal slide is ok, but it's not clear what the example is showing.
- Approach slide diagram could be clearer, with more intentional use of color.
- Details slide may be too dense; the code screenshot might not be helpful.
- Evaluation is quick and dirty and not finished. (But it's a good idea to show some results, even if they're not great.)

{{% /details %}}

{{% details summary="Final Deliverables" %}}

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

Here are some elements that would generally be expected in a report. Not all reports need to have all elements, and reports may include other elements. Reports should *generally* include:

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

### Reflection

Write, individually, about a page on:

1. What was your role or contribution to the project (if it was a team project)? Look at some examples of Author contributions statements, such as [this one](https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html#author-contributions).
2. How you would describe the project in a technical job interview.
3. A summary of the main things you learned from the process of doing the project.
4. Superlatives: most fun part? most proud of part? frustrating? surprising? interesting? challenging? rewarding? most useful part of the course for your project? 
5. Wishes: what would you do differently next time? advice for someone else doing a similar project? material you wish you had learned in the course?

At the end of your report, include a brief summary of how the project demonstrates competency of various skills.

### Supporting Material

Submit code needed to replicate the visual and quantitative results in your report.

- Share any github repos with `kcarnold` or make them public.
- Include the notebooks you used.
  - If you used Colab, download the `ipynb` file.
  - "Restart and Run All" before submitting, if possible.
  - The technical report may include all of the needed code; if so, nothing more is required.
- Include clear instructions for how to acquire any data you used. (Don't upload the dataset itself, unless it happens to be very small.)

{{% /details %}}

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

I wrote up some general comments here: https://cs.calvin.edu/courses/cs/344/22sp/project/#choosing-a-replication-project


Kaggle will be most straightforward, the others more interesting.

If you can get access to the dataset, the replication project could also be cool, especially if it connects with some of your personal interests.

Have you found existing work that you\'d replicate?

I agree that a Kaggle competition would be good for you. Maybe warm up on a closed competition to get used to how it works, then jump to a live one when you feel ready?

For tabular data, get a random forest running first, then try xgboost, and only after that go for anything more complicated.

All three look pretty good. The house prices competition is going to be the most straightforward but hardest to make interesting, because there\'s been so much done on that competition already, and the data isn\'t super-rich.

Prompt engineering is pretty cool overall. See https://arxiv.org/abs/2106.13884 for a simple approach to that idea.

I think the landscape generation one seems promising because the approaches are similar to what we've been working with already in class, and the results can look cool, and you have opportunity to control the inputs and intermediate results in interesting ways too.

Note that there have been lots of other papers since the Taming Transformers paper (which I added to the replication ideas list last year); you could do a little Google Scholar citation tracking (or browsing on paperswithcode) to find a good starting point to work from. 

I wrote up some general comments about replication projects that might help you here: https://cs.calvin.edu/courses/cs/344/22sp/project/#choosing-a-replication-project



If you want to try the research project, that would be cool. If so, let\'s find a time to meet. Easiest would be to try to book an "advising" meeting with me: https://outlook.office365.com/owa/calendar/Arnoldmeetings@calvincollege.onmicrosoft.com/bookings/s/HPLJtsUd4EWK0_CV-nIgEg2

I wrote up some general comments about replication projects that might help you here: https://cs.calvin.edu/courses/cs/344/22sp/project/#choosing-a-replication-project

General notes to everyone:

- this is rough feedback on project proposals. I probably haven\'t clicked on any of your links or thought deeply about what issues you might encounter.
- A positive reaction to one of your project ideas isn\'t necessarily a negative reaction to the others, but I am going to try to pick the project that I think will work out best.

-->