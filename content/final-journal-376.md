---
title: "Final Journal"
revised: 2026
---

## Overview

This final journal is an opportunity for you to reflect on your learning and contributions in this course, and to propose a final grade based on the three components of our grading system: Skills, Project, and Community. (See details on these components in the [syllabus](/syllabus/).)

## Instructions

Please structure your Journal as follows:

### Skills

In the Moodle Gradebook you'll find the list of [CS 376 objectives](/objectives-376) and your quiz-based scores for each. For each objective:

- If it's already at the Excellent level, simply note that.
- If it's at "Meets Expectations" but you think it could be at "Excellent" (e.g., because you have evidence for all criteria, not just what showed up on the quizzes), make a brief case for that. For example, "showed at M level on two quizzes, also showed criterion 2 ("explain why networks need nonlinearities") in notebook u06nXX-NAME".
- If it's at "Progressing", refer to the quiz(zes) where it was assessed to get a sense of what was missing. Then:
  - Write an explanation of what was incomplete or incorrect about your work. 
  - Point to some evidence that shows you can now meet the objective (perhaps a notebook or discussion post).
  - If you are able to, run this by the instructor, who might ask a follow-up question or ask you to do a small additional task to demonstrate your understanding.

For notebooks, write a sentence like "In notebook u06nXX-NAME, I did XYZ, which shows that I can do ABC." You don't need to quote the notebook or explain the details of what you did in it — just point to the relevant part and give a brief explanation of how it connects to the objective.

Then summarize:

- Compute a proposed Skills score. As a reminder, score each objective: **0 = not addressed, 1 = P achieved once, 2 = P achieved twice, 3 = M achieved, 4 = E achieved**. Average these scores (0–4 scale), then rescale: 1→68, 2→78, 3→88, 4→100. Show your work.
- Reflect overall on what you learned in this course. What difficulties did you encounter, and how did you overcome them? What are you most proud of? What still feels confusing or incomplete?

### Project

Briefly reflect on your project (see the [project description](/project/) for the criteria):

- What did you set out to do, and what did you actually build/learn?
- Which course objectives did your project help you demonstrate (and at what level)? Point to specific parts of your project as evidence.
- What would you do differently with more time?

Then propose a Project score on a 0–100 scale, and briefly justify it.

### Community

List up to 3 contributions (max 2 of any one type):

- Thoughtful contributions to discussions (in class or on Moodle forums)
- Substantial contributions to making sense of readings (e.g., Perusall)
- Presenting a tech update in class
- Organizing a perspectival discussion in class
- Leading an opening devotion
- Providing substantial feedback on others' work

For each contribution, briefly describe what you did and why you think it was substantial. 


### Tentative Course Grade

Compute your proposed course grade using the weights from the syllabus, or propose your own weights if you think that would be more fair. Show your work:

1. Construct a vector of your scores for each of the three components (Skills, Project, Community), scaled to 0-100. For example, if you had 88% for Skills, 90% for Project, and 100% for Community, your vector would be `[88, 90, 100]`.
2. Compute your final grade as a weighted average of these scores. For example, if you use the syllabus weights (70% Skills, 20% Project, 10% Community), you would compute it as follows:

```
scores = [88, 90, 100]
weights = [0.70, 0.20, 0.10]
grade = np.dot(weights, scores)
print(grade.round(2))
```

Finally: **what grade does this correspond to, and do you think it's a fair reflection of what you have learned in this class?** If you want to argue for a different grade than the formula gives, make your case.

## Submission

Submit your Final Journal on Moodle by Wednesday May 6.

