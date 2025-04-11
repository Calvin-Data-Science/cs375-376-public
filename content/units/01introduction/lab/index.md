---
title: 'Lab 1: Warmup'
weight: 3
revised: 2025
---

## Objectives

- Use a Jupyter notebook to run Python code
- Start to uncover how an image classifier works.

## Step 0: Get a Kaggle account

You'll need an account on [Kaggle](https://www.kaggle.com/).

You'll also need to verify your phone number in order to get access to GPUs, but we'll do that in the "Image Classifier" section below.

**Note**: You can also do this on Google Colab; you'll see links at the notebook sections for that. If you're using Kaggle, though, ignore the Colab links. **I don't recommend trying to run this on your own computer at this point**; even if you have a compatible GPU, getting Python to work with it can be a project.

## Step 1: Jupyter Notebooks

In this section, we'll practice working with Jupyter notebooks. You may find these references helpful:

- The Help menu in Kaggle
- Kaggle documentation

{{% task %}}
Get the following notebook.

1. Right-click the "Jupyter Notebook Warmup" link below and select "copy URL" (or "copy link location")
2. On Kaggle, create a new Notebook (in the [Code](https://www.kaggle.com/code) section).
3. On the File menu, select Import Notebook.
4. Paste the URL you just copied and click Import.
5. **Rename the notebook** to the suggested name (click the "notebookXXXXX" text at the top of the screen.)

{{% notebook name="Jupyter Notebook Warmup" nbname="u01n0-notebook-warmup.ipynb" %}}
{{% /task %}}

A number will appear next to each of the code cells when they have run successfully.

{{% task %}}
Add a code cell that computes 1+1. Check the output.
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

> **Note**: The first time you log into Kaggle, you'll need to **Verify your phone number** to get Internet and GPU access. So:
>
> 1. On the right sidebar, find "Session Options".
> 2. At the bottom of the notebook options, check for a message that reads like "Want more power? Get phone verified". Click that link and follow the instructions.
> 3. Turn on Internet access.
> 4. Switch Accelerator to GPU (either GPU option works; you might try to benchmark the difference sometime, *not now*).
> 
> If you have any trouble with this, 

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
