---
title: "Lab 6: The Remix"
weight: 4
revised: 2024
---

We've done various labs, but you've probably been more focused on "getting through it" than on really reflecting and learning from what you're doing. Today, rather than doing a lot of new work, we'll reflect on and extend some of the work we've done so far.

## Reflect

For this part, work in a text editor / word processor. (You can use a notebook if you want, but it's not necessary.) You are encouraged to discuss this with your classmates, but write your own answers.

For each lab (focusing on Labs 2 through 5), write a succinct (one or two sentences) but specific answer to following questions:

1. What was the main goal of the lab? That is, what specific facts or concepts did it demonstrate?
2. What did you learn from the lab?

Submit your reflections on Moodle in the text box provided. Go ahead and submit; when you complete the notebook in the second part, you can revise your submission to include it also.

## Extend

Pick one of the labs and extend it in some way. Here are some ideas:

- Lab 3 (backprop by hand): Extend it to fit a ReLU regression, even with the "pretend first layer activations" code already given there.
- Lab 4 (Keras):
  - Try removing the `activation = 'relu'` part of the hidden layer (i.e., the layer is still there but doesn't have an activation function). What happens? (The classifier's performance should become nearly equivalent to one of the other models that you trained; which one? Why?)
  - Try different learning rates and optimizers and see how they affect the training process.
  - Add Dropout after the hidden layer in the deeper model and see how it affects the training process and generalization.
- Lab 5 (image embedding):
  - Try different backbone models; do they have different embedding spaces?
  - Try the same approach on your Homework 1 data; what does the embedding space look like?
- Try something new:
  - I had tried doing a lab based on the Keras [Collaborative Filtering example](https://keras.io/examples/structured_data/collaborative_filtering_movielens/), but the example is *very* buggy. (It runs, but doesn't train correctly.) Try running the model code slowly by hand, check shapes, and try to fix it. (One fix: compute `(movie_embedding * user_embedding).sum(axis=1, keepdim=True)` instead of the "tensordot" line. But there are other issues too.)

If you're doing the sklearn classification notebook, you can just submit that notebook. Otherwise, you should submit a notebook that has:

1. The succinct code and results needed for your extensions (clean up any code and reflections that were only relevant to the original lab)
2. A brief summary of what code changes were needed, if applicable.
3. A brief reflection on what you learned.
