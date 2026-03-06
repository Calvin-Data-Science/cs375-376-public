---
title: "Final Journal"
revised: 2026
---

## Overview

This final journal is an opportunity for you to reflect on your learning and contributions in this course, and to propose a final grade based on the three components of our grading system: Skills, Effort, and Community. (See details on these components in the [syllabus](/syllabus/).

To help with the bookkeeping, here's a [spreadsheet template](/cs375-final-journal.xlsx) with all the objectives, formulas, and weights pre-filled. You can fill it in and use it as the basis for your journal, but your submission should include the reflection and narrative parts too — not just the numbers.

## Instructions

Please structure your Journal as follows:

### Skills

In the Moodle Gradebook you'll find the list of objectives and your quiz-based scores for each. For each objective:

- If it's already at the Excellent level, simply note that.
- If it's at "Meets Expectations" but you think it could be at "Excellent", make a brief case for that. For example, "showed at M level on two quizzes, also showed criterion 2 ("explain why networks need nonlinearities") in notebook u06nXX-NAME".
- If it's at "Progressing", refer to the quiz(zes) where it was assessed to get a sense of what was missing. Then:
  - Write an explanation of what was incomplete or incorrect about your work. 
  - Point to some evidence that shows you can now meet the objective (perhaps a notebook or discussion post).
  - If you are able to, run this by the instructor, who might ask a follow-up question or ask you to do a small additional task to demonstrate your understanding. Another option is go on Codehelp on Moodle and have a Tutor Chat (with an AI tutor) about the objective. You may start with the two Focused Tutors that are already configured if you like. These are automatically logged, so just mention here that you did that.
- If you are not able to make a case for meeting the objective, that's okay. Just be honest about that and move on to the next one.

For notebooks, write a sentence like "In notebook u06nXX-NAME, I did XYZ, which shows that I can do ABC." You don't need to quote the notebook or explain the details of what you did in it — just point to the relevant part and give a brief explanation of how it connects to the objective.

The **"Overall"** objectives were not well organized this semester. The discussion forums addressed [Overall-Impact](objective) and discussed some of the others, but we didn't provide enough opportunities for you to demonstrate them. So *only the Overall-Impact objective will be assessed for the Skills score this semester*. The one exception is [Overall-Faith](objective): it's officially marked Optional, but if you write a brief reflection and submit it as part of this Journal, we can include it in your Skills score.

Then summarize:

- Compute a proposed Skills score. As a reminder, score each objective: **0 = not addressed, 1 = P achieved once, 2 = P achieved twice, 3 = M achieved, 4 = E achieved**. Average these scores (0–4 scale), then rescale: 1→68, 2→78, 3→88, 4→100. Show your work.
- Reflect overall on what you learned in this course. What difficulties did you encounter, and how did you overcome them? What are you most proud of? What still feels confusing or incomplete?

### Effort

Gather your total hours from your weekly self-reports. Summarize, overall:

- Total outside-of-class hours by week:
  - Week 1: X hours
  - Week 2: Y hours
  - ...
- Total hours across the course: Z hours
- Approximate percentage of time spent on each type of activity:
  - Notebooks: A%
  - Assignments: B%
  - Reading: C%
  - Discussion forums: D%
  - ...

Then reflect on the kinds of things you engaged with. Which notebook was most helpful or interesting? Which reading? Which discussion forum? etc.

Compute a proposed Effort score based on the guidelines in the syllabus.

### Community

Since the course staff did not fully support the logistics of this component this semester, you may choose to **opt out** of this component. If you opt out, its 10% weight will be redistributed proportionally to Skills and Effort (roughly 78% Skills, 22% Effort).

If you'd like to include Community, list up to 3 contributions (max 2 of any one type):

- Thoughtful contributions to discussions (in class or on Moodle forums)
- Substantial contributions to making sense of readings (e.g., Perusall)
- Presenting a tech update in class
- Organizing a perspectival discussion in class
- Leading an opening devotion
- Providing substantial feedback on others' work

For each contribution, briefly describe what you did and why you think it was substantial. 

> Old comuptation: Compute your Community score as `min(1, x/3)` where `x` is the number of qualifying contributions.
>
> But of course that doesn't make sense: if you choose to claim one or two Community contributions instead of opting out, that formula would penalize you compared to opting out. So instead, just list your Community score at 100% and weight your overall grade accordingly (see below).



### Tentative Course Grade

Compute your proposed course grade using the weights from the syllabus (*correction: using the following softmax-style computation*).

1. Construct a vector of your scores for each of the three components (Skills, Effort, Community), scaled to 0-100. For example, if you had 88% for Skills, 95% for Effort, and 100% for Community, your vector would be `[88, 95, 100]`.
2. Construct a vector of logits for each of the three components (Skills, Effort, Community) as, roughly, `logits_base = [0, -1.25, -1.95]`. (Note that `np.exp(logits_base)` gives the weights 70%, 20%, 10%.). Then adjust as needed, e.g., set the logit for Community to something like `-10` if you opted out, `-3` if you had one contribution, `-2.5` if you had two contributions, and `-1.95` (no adjustment) if you had three contributions.

Then compute your weights as `weights = np.exp(logits) / np.exp(logits).sum()`, and your overall grade as `grade = (weights * scores).sum()`. Show the calculation. For example:

```
scores = [88, 95, 100]
logits = np.array([0, -1.25, -1.95])
logits[2] = -3 # (one Community contribution)
weights = np.exp(logits) / np.exp(logits).sum()
print(weights.round(2))
[0.75, 0.21, 0.04]
grade = np.dot(weights, scores)
print(grade.round(2))
89.95
```

Finally: **what grade does this correspond to, and do you think it's a fair reflection of what you have learned in this class?** If you want to argue for a different grade than the formula gives, make your case.

## Submission

Submit your Final Journal on Moodle by the last day of class (Friday, March 6).

**Note about the last quiz**: Your Final Journal may reference your quiz scores as of the time you write it. If the last quiz changes any of your objective levels, you may submit a brief addendum after that quiz is returned.

