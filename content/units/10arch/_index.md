---
title: "376 Unit 3: Architectures"
weight: 10
revised: 2024
---


{{% details summary="Q&A" %}}

- What's a hidden state?
  - It's the output of a layer of a neural network.
  - It's an *embedding* of the part of the input needed to continue the current calculation (e.g., predict the next token).
- Why is just the start token's hidden state typically used for classification?
  - Any individual token would otherwise contain some information from that single token as well as information from the entire sequence.
  - Note: It can attend to the entire sequence (in a bidirectional model like BERT).
  - Its hidden state representation doesn't need to be used for anything else (unlike other tokens, which need to be able to decode to a token.)
  - There may be better ways to do this, but this is a common approach.
- Why do we need padding?
  - Everything needs to be a tensor.
  - Tensors generally need to be rectangular, not ragged.
  - But when we put multiple sentences into a batch, they might have different lengths.
  - So we pad them to the same length.
  - (We could use ragged tensors instead, but hardware support for them isn't as good.)
  - This is mainly a concern when *training*. At inference time we often only have one sequence at a time. (unless we're doing beam search, which we'll talk about later.)
- Why is GPT-3 encoder-only?
  - See the Outline.

{{% /details %}}
