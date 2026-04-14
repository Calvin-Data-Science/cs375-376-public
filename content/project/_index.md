---
title: "Project (CS 376)"
toc: true
---

Instead of a final exam, our course culminates in a project. Unlike quizzes, which test specific objectives, the project is your chance to go deeper on something you care about and demonstrate what you can do.

## What will you demonstrate?

The most important question for your project is: **what course objectives will this demonstrate, and how?**

You'll answer this in your proposal. For each objective you claim, write a sentence about how your project will address it. This becomes your personal rubric — the instructor will give feedback on it, and you'll revisit it in your reflection.

At minimum, a strong project should demonstrate something from each pillar:
- **Tuneable Machines**: understanding how the model works (architecture, data flow, what it's actually doing)
- **Optimization Games**: framing the problem, evaluating results, and reasoning about what the numbers mean

You're also encouraged to write *additional* objectives beyond the course list — skills you want to develop or demonstrate that aren't already in the syllabus.

## Teams

- Ideally 2–3 people who can work synchronously at least once a week
- Each member should be able to clearly describe their role
- Use the Moodle discussion forum to find teammates

## Milestones

1. **Proposal** (due early): Submit a short document with: (a) what you're doing, (b) which course objectives it will demonstrate and how, (c) how you'll know if it's going well. Keep it short — a paragraph and a list is fine.
2. **Weekly updates**: Include a brief project update in your weekly reflection.
3. **Final deliverables**: See below.

## Final Deliverables

### Presentation

The final course meeting (during the designated final exam period) will be devoted to presentations. **Attendance is mandatory.**

Aim for 5 minutes. Slides are helpful but not required (you could scroll through a notebook). All team members should participate.

{{% details summary="Suggested outline" %}}

- **What problem** are you trying to solve, and why does it matter?
- **How you approached it**: how you framed it as an ML problem, what model/data you used
- **What results** you got — both numbers and specific examples
- **What you learned**: about the problem, the model, or AI/ML more generally
- **Limitations and what you'd do next**

{{% /details %}}

### Technical Report

The report should be at the level of polish of a good blog post: more than a homework assignment, less than an academic paper.

- **Audience**: Intro/conclusion for a general audience; the rest for someone who knows ML in general but not the specific tools you used.
- **Format**: A Jupyter notebook (`.ipynb`) is preferred. The report should make sense even if all code is hidden.
- **Structure**: Explain what you did, why you made the choices you made, and what you observed. For each major section: say what you're trying to do, do it, then discuss what you learned.

{{% details summary="Example report structure" %}}

This is a starting point — adjust for your project.

- **Title** and real-world question/goal (and why it's interesting)
- **Dataset**: what it contains, where it came from, strengths/limitations
- **Approach**: your technical method, including key choices and why you made them
- **Evaluation**: quantitative results AND qualitative analysis. For any number you report, also ask: *what does this number actually mean for the real problem, and what doesn't it capture?*
- **Analysis of errors** or failure cases
- **Comparison of alternatives** (different approaches, hyperparameters, data choices)
- **Summary**: did you achieve your goal? Why or why not?
- **Limitations and future work**: be specific. Not "I ran out of time to do X" but "these results assume Y, which might not hold when..."

Checklist:
- [ ] Explains *why* you made various decisions
- [ ] Backs up claims with evidence (numbers, examples)
- [ ] Cites sources for any ideas not your own

{{% /details %}}

### Reflection

Write an individual reflection (about a page):

1. **Objectives**: Which course objectives does this project demonstrate? For each one, write a sentence or two about how. Compare to what you claimed in your proposal — did you end up demonstrating what you planned? More? Less?
2. **Portfolio quality**: How would you rate this project (A/B/C/D)? What makes it strong, and what would have made it stronger?
3. **Interview question**: Imagine discussing this in a technical job interview. What question does the interviewer ask, and what's your answer? (Ask an LLM for feedback on this one.)
4. **Contribution** (for team projects): What was your specific role? See examples of [author contribution statements](https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html#author-contributions).

### Supporting Material

Submit code needed to replicate your results.

- Share GitHub repos with `kcarnold` or make them public
- Include notebooks. Run "Restart and Run All" before submitting if possible.
- Include instructions for acquiring any data used (don't upload large datasets)

## Grading

### Minimum bar

Every project must meet these to count as submitted:

- [ ] Report is organized, well-written, and cites sources
- [ ] Code is submitted and documented
- [ ] You presented
- [ ] Reflection is complete

### Objectives

Your proposal specifies which objectives the project demonstrates. Your reflection self-assesses whether it does. The instructor will confirm or adjust.

Demonstrating an objective in the project counts as meeting it at **M (Met)** level.

### Holistic quality

In your reflection, you'll propose a holistic grade (A/B/C/D) based on the portfolio framing:

- **A** — strong enough that I could write you a recommendation letter based on this
- **B** — definitely worth including in your portfolio
- **C** — could include it, but not if you have stronger work
- **D** — probably not portfolio-worthy

The main ways to get to A or B:
- Go **below the surface** on something: analyze what the model is actually doing, not just what it outputs
- **Evaluate meaningfully**: qualitative + quantitative, and connect numbers back to the real problem
- **Make and justify decisions**: explain why you made the choices you did, and what the alternatives were
- **Specific limitations**: not generic concerns, but concrete examples tied to your project
