---
title: "Generalization and a Kaggle Competition"
weight: 4
revised: 2026
---

## Outcomes

The process of completing this assignment will improve your ability to:

- Explain the importance of evaluating image classifiers on unseen data.
- Describe characteristics of a dataset that are relevant to downstream performance.
- Use data augmentation to improve model generalization.
- Describe how the concept of *distributions* applies to image data.

Along the way, we'll participate in a Kaggle competition, so you'll get to practice with that.

## Task

Load up the classifier you trained in Homework 1. **Use it to make predictions on a set of images collected by others** in the class. You'll do this by participating in a Kaggle competition.

Click the link provided in Moodle to join the Kaggle competition. Then **make a copy of your Homework 1 notebook** (in Google Colab, File → Save a copy) to use as your starting point for this assignment.

### Getting the competition data

Download the competition dataset into your Colab notebook:

```python
import urllib.request, zipfile
from pathlib import Path

competition_url = "https://students.cs.calvin.edu/~ka37/letter-images-26sp.zip"
competition_dir = Path("./data/competition")
competition_dir.mkdir(parents=True, exist_ok=True)
archive_path = competition_dir / "letter-images-26sp.zip"

if not archive_path.exists():
    print(f"Downloading {competition_url}...")
    urllib.request.urlretrieve(competition_url, archive_path)
    with zipfile.ZipFile(archive_path, "r") as z:
        z.extractall(competition_dir)
    print("Done.")
```

Then check what's inside:

```python
!ls {competition_dir}
```

You should see folders and CSV files similar to:

```
sample_submission.csv  test/  test.csv  train/  train.csv
```

### Loading the competition images

The competition images are in a flat folder with a CSV file mapping filenames to labels (not sorted into class subfolders like your Homework 1 data). Here's how to load them:

```python
import pandas as pd
from torch.utils.data import Dataset
from PIL import Image

valid_df = pd.read_csv(competition_dir / 'train.csv').sort_values('filename')
test_df = pd.read_csv(competition_dir / 'test.csv').sort_values('filename')

class CSVImageDataset(Dataset):
    """Load images from a flat folder using a CSV for labels."""
    def __init__(self, df, image_dir, transform, class_names):
        self.df = df.reset_index(drop=True)
        self.image_dir = Path(image_dir)
        self.transform = transform
        self.class_names = class_names

    def __len__(self):
        return len(self.df)

    def __getitem__(self, idx):
        row = self.df.iloc[idx]
        image = Image.open(self.image_dir / row['filename']).convert('RGB')
        image = self.transform(image)
        if 'label' in row and pd.notna(row['label']):
            label = self.class_names.index(row['label'])
            return image, label
        return image, -1  # test set has no labels

valid_dataset = CSVImageDataset(valid_df, competition_dir / 'train', data_transforms, class_names)
valid_dataloader = DataLoader(valid_dataset, batch_size=config.batch_size, shuffle=False)
```

Here `data_transforms` and `class_names` should be the same ones from your HW1 notebook (`class_names` should be `['a', 'b', 'c']`).

### Steps

1. Run your Homework 1 model-training code in the new notebook (or load saved weights). **Note that although the competition has a "training" set, you should (mostly) use your Homework 1 model, including its dataset.**
2. Use the code below to make predictions on the **test** images and generate a `submission.csv`. Upload it to the Kaggle competition. Name your submission "Homework 1 baseline" or the like. Write down in your analysis how well your baseline does on the leaderboard.
3. The competition's "training" dataset is actually a **validation set** of images from other students. Use it to evaluate your confusion matrix, like you did in Homework 1. **Report the most frequent mistakes** your classifier makes. **Quantify the mistakes** (using the confusion matrix) and make an educated guess as to *why* these might be the most common mistakes.
4. Make some changes to the training process you used in Homework 1. For example, you might want to add data augmentation or change the foundation model. Experiment as much as you want, but **make two more submissions** to evaluate on the test set and see what effect your changes had on the leaderboard. Be thoughtful about your changes and **explain them in your analysis**.
5. Optionally, try to improve your model's performance further to try to get a higher score on the leaderboard. You may, for example, train on the training set given in the competition.

### Generating submission.csv

```python
test_dataset = CSVImageDataset(test_df, competition_dir / 'test', data_transforms, class_names)
test_dataloader = DataLoader(test_dataset, batch_size=config.batch_size, shuffle=False)

# Get predictions
test_predictions = []
model.eval()
with torch.no_grad():
    for inputs, _ in test_dataloader:
        inputs = inputs.to(device)
        outputs = model(inputs)
        preds = outputs.argmax(dim=1).cpu().numpy()
        test_predictions.extend(preds)

# Map predictions to class names and save
test_df['label'] = [class_names[p] for p in test_predictions]
test_df[['id', 'label']].to_csv('submission.csv', index=False)
```

Upload `submission.csv` to the Kaggle competition page.

## Analysis and Submission

Submit your Homework 3 notebook to Moodle. You don't need to submit a revised Homework 1 notebook, but make sure that your Homework 3 notebook includes details of what you changed in that notebook.

Your notebook should include:

- An introduction that summarizes what you did and what you found.
- A clear explanation of the source and nature of the data you used for training your initial (homework 1) classifier.
  - Include any relevant information you reported in the README in Homework 1.
  - Also, read the introduction to Microsoft's [Dataset Documentation (Datasheets for Datasets) template](https://www.microsoft.com/en-us/research/uploads/prod/2022/07/aether-datadoc-082522.pdf). Then, skim through the questions that follow. **Choose two or three questions** that are most relevant to *how well the model that you trained on that data worked on new data*. Include both the **question texts** and your answers. Good answers are those that would most help someone who is training on your dataset predict how it will work on new data.
- An organized summary of your results for the baseline model and the two modified models.
  - Recall that in Homework 1 you estimated the accuracy that your classifier would obtain on other people's images. **Compare the accuracy you observed from the baseline model to the accuracy that you thought you'd get.**
  - Discuss what you noticed from analyzing the mistakes of your baseline model.
  - Discuss what changes you tried in order to improve performance, and most importantly, *why you tried them*.
  - Discuss what you learned from the changes you tried.
- A clear conclusion that summarizes what you found and interprets what the results mean.


## Details


Possible things to adjust:

- How big your Homework 1 classifier's validation set is
- Which foundation model to use (see hw1 for a list of options)
- What data augmentation (if any) to apply
- How many epochs to train
- What learning rate to use

Think about what other sources of variation might come up, and how you might be systematic about them.

## Augmentation

We didn't do code for image augmentation in the lab, but it's straightforward with `torchvision.transforms`. In your Homework 1 notebook, create an augmentation pipeline that applies random transformations *before* the standard preprocessing:

```python
from torchvision import transforms

augmentation_transforms = transforms.Compose([
    transforms.RandomHorizontalFlip(),
    transforms.RandomRotation(15),
    transforms.ColorJitter(brightness=0.2, contrast=0.2),
    transforms.Resize((config.image_size, config.image_size)),
    # then apply the same normalization as your pretrained model expects:
    config.pretrained_weights.transforms(crop_size=config.image_size),
])
```

Then create a new version of your training dataset that uses these augmented transforms:

```python
train_dataset_aug = datasets.ImageFolder(
    root=your_data_path,
    transform=augmentation_transforms
)
```

> Because the random transforms are applied each time an image is loaded, each epoch will see different augmented versions of your training images.

I suggest visualizing some example batches from the augmented dataset to make sure the augmentation is working as you expect. When you train the model, use the augmented dataset instead of the original.

**Think carefully** about which augmentations make sense for handwritten letters. For example, would a horizontal flip be appropriate for distinguishing 'b' from 'd'?

## Errata

None yet this year.
