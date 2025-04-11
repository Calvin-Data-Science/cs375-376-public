---
title: "Project Scratch"
---


Simplified transformer
Everything in the same vector space (dropout projections, layers)
Simplified attention (randomly replace with fixed pattern)

Modeling a learner
* What if, within each document, only a part of the network’s knowledge is active? Maybe we get to skim the document to identify who, then run it
    * Simpler idea: for each document, we randomly drop out entire chunks of the network in a mostly ordered-dropout way (core skills rarely turn off, others often turn off). Layers, attention heads/queries, context distance, vocabulary (tokenizer)
    * 


How does the LM implement the following tasks? (Do they work? When do they break?)

- "spell the word ___"
- "capitalize ___" (a, b, c, any word, phrase?)
- (same, but give examples instead of commands.)


-   create an interactive application - using a model to do something interesting (e.g., [GANPaint](https://ganpaint.io/)), or allowing interesting exploration / interaction with the model itself (e.g., [LSTMVis](http://lstm.seas.harvard.edu/) or [Seq2Seq-Vis](https://seq2seq-vis.io/)). Links to lots of examples [here](https://distill.pub/2020/communicating-with-interactive-articles/).

-   try out a different deep learning toolkit (e.g., TensorFlow, tensorflow.js or [Flux.jl](https://fluxml.ai/)) on several tasks from class


### Face Generation GAN

Teachers have a hard time getting to know students by face, especially when students are wearing masks. Flashcard apps help, but the teacher can easily "overfit" to quirks of the student photo (background, clothing, etc.).

-   **Input**: students' profile photos
-   **Output**: a dozen different images for each student, with variation in background, lighting, clothing, etc. so that these factors are informative

Terms to search for:

- GAN inversion
- GAN editing
- GAN latent space


### Learned Multimedia Decoder

Many existing images/videos/audio are locked in poor quality low-efficiency codecs (old personal pictures, audio Bible recordings, video, music, graphics, etc.). If we could invert the poor-quality encoder, we could both recover a more faithful representation of the original and also re-encode the result in a high-efficiency codec.

-   **Input**: a JPEG (or other legacy codec) bitstream, unpacked (e.g., the JPEG data could be arranged spatially, so the data for each macroblock would align with where it is in the image).
-   **Output**: the correct image (or audio, video, etc.)


### Miscellaneous ideas

-   Language

    -   sequence-to-sequence-to-sequence (the latent code is a sequence). Ask me for details.

