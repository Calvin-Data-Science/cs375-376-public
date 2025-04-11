---
title: "376 Unit 4: Generation and Prompt Engineering"
weight: 11
---


{{% next-year %}}

Quiz questions?

- Which sequence generation algorithm will give only a single output?
  - greedy
  - sampling, beam search
- Which sequence generation algorithm yields different results each time it is run? (sampling)
- Which sequence generation algorithm requires the most computation (i.e., forward passes through the model): beam search
- Why might beam search give higher quality translations than greedy sampling?
  - Beam search allows the generation algorithm to revisit prior decisions.
  - Greedy sampling is too noisy.
  - The network was trained using beam search.
- In a generative adversarial network (GAN), which of the following is a correct description of the *input* to a generator network (typically called `z`)?
  - A random vector
  - The generated image, expressed as a vector
  - A vector that has been optimized to represent a specific given image
- If z1 and z2 are both input vectors to a generator network, what can you say about a linear interpolation between z1 and z2 (i.e., alpha * z1 + (1 - alpha) * z2)?
  - The generated image will probably look reasonable.
  - When alpha is 1, the output image will correspond to z2
  - The output will be a cross-fade between the two images, like a double-exposure.
  - The operation is invalid because the dimensionality doesn't match up.
- The *input* to the discriminator network of a GAN is:
  - Images, either real images or outputs of the generator network. 
  - The same vectors that are given to the generator network (z1, z2, etc.)
  - Binary labels, representing *real* or *fake*
- A discriminator network is best described as
  - A binary classifier computing the probability of an image being real or fake.
  - A probability distribution that defines the manifold of generated images.
  - A function that gives the probability of the next pixel
- When training the discriminator, we want to take gradient steps that...
  - Reduce the cross-entropy loss of the real-fake classifier
  - Increase the cross-entropy loss of the real-fake classifier
- When training the generator, we want to take gradient steps that...
  - Increase the cross-entropy loss of the real-fake classifier
  - Reduce the cross-entropy loss of the real-fake classifier


{{% /next-year %}}


<!--
- [Slides](/slides/2022-03-30%20Generative%20Models.pdf)
- We briefly discussed [StyleGAN 3](https://nvlabs.github.io/stylegan3/) ([blog post](https://lambdalabs.com/blog/stylegan-3/)).
  - The demo was done in [this notebook](https://colab.research.google.com/drive/1eYlenR1GHPZXt-YuvXabzO9wfh9CWY36) which also includes text-guided refinements via a method called [CLIP: Connecting Text and Images](https://openai.com/blog/clip/) ([code](https://github.com/openai/CLIP))
  - Here is the [core code for StyleGAN 3](https://github.com/NVlabs/stylegan3/blob/main/training/networks_stylegan3.py)

-->

{{% next-year %}}

- Actually show a random image generation
- Show class-average images as an example of why we need to model relationships between pixels

{{% /next-year %}}


