---
title: "Homework 1: Train and evaluate a classifier on your own images"
revised: 2026
---

<!-- next year:

- Give students a clear outline of the code, and the structure of the responses (maybe even templates).
-->

**Important**: Read this whole document before you start.

## Goal

In this assignment, you will train and evaluate your own image classifier to distinguish the handwritten letters A, B, and C.

Completing this homework will give you practice

- Working with image datasets
- Training image classifiers
- Evaluating image classifiers
- Explaining your decisions and their possible consequences.

A famous image classification example is handwritten digits (called MNIST). For fun, we'll remix that idea and classify handwritten *letters*.
To keep it manageable, we'll just work with the first 3 *letters* (`a` through `c`).

Try to make the best model you can, under the following constraints:

1. *No more than* 100 training images. (**Note**: This is a *maximum*, not a minimum.)
2. No more than 5 minutes compute time (on a Kaggle, Colab, or lab machine GPU) to train a model.
3. Only use models that are already built into `torchvision`.

## Instructions

Let's make this a **friendly competition**: which *team* (of up to 5) can make the best classifier?

1. Collect your own set of images of handwritten letters, one letter per image. (Do this yourself, don't get it from the Internet.)
    - Please do share images amongst your team. You might use a OneDrive shared folder or similar.
2. Organize your dataset into a folder structure like `images/c/c01.png`.
    - Make an `images/README.txt` describing your dataset (see below for details)
3. Train a classifier to indicate which letter is contained in the image.
4. Evaluate the accuracy of the classifier on the validation set. (See below for details).
5. Submit your Jupyter Notebook and dataset ZIP file to Moodle.
  - Make sure you Restart your notebook and Run All.
  - Check that your code outputs match what you write about. There *will* be some variability in your classifier's performance. Think statistically: remember that a number like accuracy is an *estimate* of a proportion and your sample size is probably small.

## Report Expectations

Your report should be a professionally crafted Jupyter Notebook, suitable to use in a portfolio. So your notebook should be:

- *Well-formatted*: use appropriate `## Headings`; proofread text and code
- *Literate*: explain what you are doing and why.
- *Reproducible*: running it from a clean slate should reproduce the results shown, including training the main model described. (*you don't need to include code to train other models that you may have also tried*, unless substantial modifications were necessary.)

We highly recommend the following structure:

1. A compelling opening *vision statement*, with appropriate citations of any code or notebooks on which you are basing this work (e.g., for this assignment that would be the Lab 1 notebook);
2. A clear explanation of the source and nature of the *data*, including links that would allow others to access the same data (e.g., how you built your dataset and where it can be found);
3. A complete discussion/demonstration of the *analysis*, with explanations and code required to build and evaluate the models;
4. Strong *conclusions*.

The notebook shouldn't include anything that doesn't apply to these goals (e.g., no in-applicable text retained from an original notebook)

For this assignment:

- The dataset description in the notebook should include at minimum (1) how many images you have of each class and (2) how you collected the images (e.g., whether you used a mouse/finger/pen or took pictures of paper/whiteboard/chalkboard/documents you found in the Meeter Center/...). Also include this information in your dataset's `README.txt`.
- Your analysis should include at least:
  1. How many images you have in your classifier's training and validation sets.
  2. Evaluations of the model on your validation set.
      - How accurate is the classifier overall?
      - Which letter is it most successful at classifying? Give an example of a correctly classified image (show a specific image file and its classification).
      - What mistakes does it make most frequently? Give an example of a mistake (show a specific image file and its classification).
      - For the previous 3 questions, any ideas about *why*?
      - **Generalization**: Suppose someone else gave you one of their images. How likely do you think your classifier would be to get it right, and **why**? *report your answer in terms of a percentage, either overall or broken down by which letter*.
- Your conclusion should include at least: what choices did you have to make in the process of collecting data, processing it, and analyzing the results?
    - What are one or two choices that you could have made differently?
    - What do you expect would be different if you made that different choice?

### Notes

- Include all the code needed to get *one* good accuracy number.
- *Don't* try to show the results of every model you trained, but *do* make a single cell to change numbers for any aspects you varied (e.g., the seed, how many images you used)
- *Don't* include extraneous code
- Use *Markdown* cells, not code comments, to report results.

### Tips

- Collecting data
    - I've hacked together [this little webapp](https://codepen.io/kcarnold/full/poZpdqX) to let you sketch and share/save. It's clunky; improvements welcome! Think about whether it makes sense to have a lot of images like these.)
    - You can also take pictures of sketches on paper, whiteboards, etc.
    - You should have at least 10 images per letter.
    - To get started, you can use [this dataset](https://students.cs.calvin.edu/~ka37/example_letter_images.zip) I hacked together very quickly. But it's bad in various ways, so please collect your own.
- Coding
  - Start with the Lab 1 classifier code and a small set of images.
    - I've made some updates to the starter notebook so that it runs on MPS (Apple Silicon) and includes some example code for getting validation set predictions.
  - One easy way to get your dataset into your notebook is to put it your `public_html` folder on the lab computers. Then you can access it at `https://students.cs.calvin.edu/~username/filename.zip` (make sure you include the tilde.) Then you can set `url` to that in the Lab 1 data loader code. (Be sure to change `archive_path` and `extract_path` as needed.)
    - If you have any trouble on the notebook, try accessing that URL on your own browser. If you get a permissions error, check the permissions on the ZIP file on the lab computers (right-click and Properties, or via the command line). For the web server to be able to read it, “Other” has to be able to “read”, i.e., `chmod o+r ~/public_html/letter_images.zip`.
  - You might need to set the batch size to be smaller than the default.
- Improving a model
  - Try changing config parameters.
    - The model preset might have a particularly big impact on speed and accuracy. Look up documentation, such as [`torchvision` models](https://docs.pytorch.org/vision/main/models.html)
    - One epoch is probably not enough.
  - Visualize things:
    - What does your data look like?
    - What do the predictions of your classifier look like?
    - What does the confusion matrix look like?

To get the confusion matrix, loop over the validation set, loop over the validation dataloader and accumulate all of the probabilities:

```python
val_predicted_probs = []
model.eval()
with torch.no_grad():
    for inputs, _ in tqdm(val_dataloader, desc="Predicting on validation set"):
        inputs = inputs.to(device)
        outputs = model(inputs)
        probs = outputs.softmax(dim=1).cpu().numpy()
        val_predicted_probs.append(probs)
val_predicted_probs = np.vstack(val_predicted_probs)  # Shape: (num_val_samples, num_classes)
```

Look at `val_predicted_probs.shape` and make sure you understand why its second dimension is 3.

Then get the model's top prediction for each image using `val_predictions = np.argmax(val_predicted_probs, axis=1)` 

To get the true labels out of the dataset, use

```python
val_labels = np.hstack([
    labels.numpy() for _, labels in val_dataloader
])
val_labels.shape
```

Then to show a confusion matrix, use:

```python
from sklearn.metrics import ConfusionMatrixDisplay
ConfusionMatrixDisplay.from_predictions(val_labels, val_predictions, display_labels=class_names)
```

(assuming that `class_names` is the same list you used when constructing the data loader).

<!--

Future: top losses would be useful. I've prototyped this in a Kaggle notebook, basic idea is:

https://github.com/tulasiram58827/plot_top_losses_keras/blob/master/Plot_Top_Losses_Keras_wandb.ipynb
https://github.com/tulasiram58827/plot_top_losses_keras

-->