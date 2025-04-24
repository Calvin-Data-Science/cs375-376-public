---
title: "Lab 5: Stable Diffusion"
revised: 2024
---

Open this notebook. You can run it on Kaggle or Colab, or run it on a lab machine (but there's some configuration issues to resolve if you do that.)

On a lab machine, start by opening a terminal and running the following command to set up the environment:

```bash
/home/cs/376/setup-cs376.sh
```

Then, log out and log back in. Then open a terminal and run the following command to start Jupyter Lab:

```bash
activate_376
jupyter lab
```


- {{% notebook name="Stable Diffusion Deep Dive" nbname="u12n1-stable-diffusion.ipynb" %}}

Your goal today is to *be creative* and see what you can make! The notebook includes a variety of things to try, but you can also try your own ideas.

For your write-up, you should include:

1. What does the "random seed" do in first diffusion main loop? What happens when you change it or remove it?
2. What happens when you set the guidance scale to 0 (again in the first diffusion loop)? Follow the flow of data through the code to see what's happening.
3. What happens when you stop the diffusion early (e.g., `if i == 10: break`)? What do you notice about the output?
4. Now going to the image2image model: what is the role of adding noise to the latent image? What happens when you change the amount of noise? (change `start_step`; refer to `num_inferenece_steps` for its max value)
5. Something creative that you did with the Stable Diffusion model: what did you try, what results did you get, and what did you learn?

Some ideas of things to try:

- Change the prompt. Try more or less descriptive prompts. This is especially interesting for the image-to-image models.
- Under "messing with embeddings", try changing the two prompts to different texts. Or change the mix factor. What happens?
- Try different ways of mixing things together:
  - Try different text chimeras
  - Try starting with an image latent composed of half of one image and half of another (horizontal or vertical split, or perhaps grab the middle from one and the edges from another)
- Try outpainting: scale the latents to half the size, replace the middle part of a random latent with those (each iteration), and diffuse.
