---
title: 'Lab 1: Warmup'
weight: 3
revised: 2025
---

## Objectives

- Use a Jupyter notebook to run Python code
- Start to uncover how an image classifier works.

## Step 0: Log in to your Google account

You can use either your personal account (if you have one) or your Calvin account.

**Note**: **I don't recommend trying to run this on your own computer at this point**; even if you have a compatible GPU, getting Python to work with it can be a project.

## Step 1: Jupyter Notebooks

In this section, we'll practice working with Jupyter notebooks. You may find these references helpful:

- [Colab overview](https://colab.research.google.com/notebooks/basic_features_overview.ipynb)
- some parts of the [Jupyter Notebooks docs](https://jupyter-notebook.readthedocs.io/en/latest/examples/Notebook/Running%20Code.html)

{{% task %}}
Get the following notebook.

1. Click the "open in Colab" link in on the line below.
2. **IMPORTANT**: Click "Copy to Drive" on the toolbar. It will open in a new tab -- **close the old tab** so you don't get confused.
3. Rename the notebook to remove the "Copy of"...

{{% notebook name="Jupyter Notebook Warmup" nbname="u01n0-notebook-warmup.ipynb" %}}
{{% /task %}}

A number will appear next to each of the code cells when they have run successfully.

{{% task %}}
Add a code cell that computes `1+1`. Check the output.
{{% /task %}}

**Note carefully** the difference between **Command mode** and **Edit mode**.

{{% task %}}
Add a Markdown cell that looks like this (you may want to refer to a Markdown quick reference; [here's one](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet))  ([GitHub Docs](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github), [spec](https://github.github.com/gfm/))

> Here is some Markdown formatting:
> 
> - This is **bold**.
> - This *is* italic.
> - This is a [link to Calvin's website](https://calvin.edu).

"Run" the cell to ensure that it gets formatted correctly. Check that the website link opens correctly.
{{% /task %}}

I highly encourage you to get comfortable with keyboard shortcuts for the following operations:

- Switch between edit and command mode. (Enter/Return and Esc)
- Insert a cell above or below (`a` and `b`)
- Change a cell to code / Markdown (`m` or `y` in Command mode)
- Run the current cell (with or without selecting the cell below) (`Ctrl-Enter` or `Shift-Enter`)

For more keyboard shortcuts click the Command Palette button on the bottom toolbar on Kaggle (it may be hidden by a cookie consent bar!) or use a search engine.

{{% task %}}
Suppose a cell has multiple expressions in it, like this:

```python
x = 1.0
x * 2
print("Something")
x = x * 2
x * 2
```

Which one gets displayed? Can you figure out the general rule for what output gets displayed from a notebook cell?

**Add a Markdown cell with your answer to this question**.

{{% /task %}}

When you're done, save your notebook and submit it on Moodle.

## Step 2: Image Classifier

In the next section, you'll work with a basic image classifier.

In this section (and most future Labs), the tasks to do are inside the notebook itself. You'll find cells labeled **Task** and blank code chunks usually labeled `# your code here`. Follow the instructions top-to-bottom, then download and submit when done.

{{% task %}}
1. Make a new notebook (so you don't overwrite your work from the first part).
1. Get this notebook: {{% notebook name="Train a simple image classifier" nbname="u01n1-train-clf.ipynb" %}}
2. Work through the instructions **thoughtfully**. *Resist the urge to "just get through it".* Ask questions, help others, etc.
3. Download the notebook and submit the `ipynb` file to Moodle.
{{% /task %}}

Checklist:

- [ ] Did we fill in the table with the accuracy and loss numbers?
- [ ] Did we think about whether the predictions are a probability distribution?
- [ ] Did we try out using `argmax`? Can we get it to show the name of the predicted class, not just its number?
- [ ] Did we try changing something to see what effect it has on the accuracy?
