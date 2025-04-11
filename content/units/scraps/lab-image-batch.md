---
title: "Image batch lab"
---

Objectives:

- Describe the structure of image batches
- Write code to access and modify image data

## Image Batch Structure

Now, let's see what's going *into* the classifier. The images are given in *batches* of, say, 16 images at a time. They all get packed into a single array. That's possible because arrays can have multiple axes. Let's see how those work:

{{% notebook name="Image Operations" nbname="u02n2-image-ops.ipynb" %}}
