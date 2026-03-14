---
title: "Exploring Language Models"
weight: 5
revised: 2026
---

Objectives:

- Describe how a conversation is represented as a document for a language model.
- Describe what a next-token conditional distribution is.
- Describe the implications of how language models generate text sequentially.
- Compute the log-probability that a language model assigns to a sequence of tokens, and connect this to cross-entropy loss.

Open the [**Language Model Internals** page](/lm-internals.html).

# Part 1: A Conversation is a Document

Type a message like: `Tell me a story about a dragon.` (Replace "dragon" with your own topic.) Click "Send" to finish your message.

Before generating anything, look at how the tool displays the conversation. You should see your message displayed as a sequence of tokens, with special markers indicating the role (e.g., `<start_of_turn>user` and `<start_of_turn>model`).

1. Where in the token sequence does the user's turn end and the assistant's turn begin? What markers separate them?

2. Think about this: all the model does is predict the next token in a document. Why would it generate a story rather than, say, continuing your sentence with more questions? What about the document structure makes "a story" the likely continuation?


# Part 2: Building a Response Token by Token

Now we'll construct the assistant's response ourselves, one token at a time.

The tool should show you the model's predicted **next-token distribution**: a list of candidate tokens and their probabilities. For example, you might see something like:

| Token   | Probability |
|---------|-------------|
| In      | 0.25        |
| Once    | 0.18        |
| A       | 0.12        |
| There   | 0.09        |
| Deep    | 0.07        |
| ...     | ...         |

3. Pick the **most likely** token. It gets added to the sequence, and the tool shows a new distribution for the *next* token. Repeat this about 10 times, always picking the top prediction. Write down the sequence of tokens you get. Does it produce a coherent story opening?

4. Compare your sequence with a neighboring team. Did you get the same thing? Why or why not?

5. Now **reset** the response and start over. This time, pick an **unlikely token** for the very first assistant token---say, the 5th or 10th most likely option. Then continue picking the top prediction for the next ~10 tokens. Write down what happens.

6. Try step 5 again with a different unlikely starting token. What do you notice? Reflect on this question: *The model doesn't plan ahead---it only sees the tokens that have already been written. How does it still produce something coherent after a weird start?*

7. *(Bonus)* Try forcing an unlikely token in the *middle* of a response that was going well. Does the model recover?


# Part 3: Predictable vs. Surprising Tokens

Generate a full story (maybe 2-3 sentences) by letting the model pick all the tokens itself.

8. Click on different tokens in the generated story to see the distribution the model predicted at that position. Find a token where the model was **very confident**---one option dominates with high probability (e.g., > 0.8). What token is it, and why is it so predictable?

9. Find a token where the model was **uncertain**---several options have similar probability. What token is it? Why is this position harder to predict?

10. The probability the model assigned to the token that actually came next tells us how "surprised" the model was. Where in the story was the model *most* surprised? Where was it *least* surprised? Does this match your intuition about which words are predictable and which aren't?


# Part 4: Measuring Surprise

When training a language model, we need a number that says how well the model predicted the actual next token. We can measure this in **bits**: $-\log_2(p)$, where $p$ is the probability the model assigned to the correct token. This tells us how many bits of information were needed to identify that token, given the context. Some reference points:

- A fair coin flip ($p = 0.5$): 1 bit
- Rolling a specific number on a die ($p = 1/6$): ~2.6 bits
- A token the model is very sure about ($p = 0.95$): ~0.07 bits
- A token the model finds surprising ($p = 0.01$): ~6.6 bits

11. Pick a token where the model was confident and one where it was uncertain. Compute $-\log_2(p)$ for each. Which takes more bits? Does that match your intuition?

12. Select a span of about 5 consecutive tokens in the story. The tool should show you the **total bits** needed to encode that span. Try to verify this: write down the probability for each token, compute $-\log_2(p)$ for each, and add them up. Does it match?

13. Now select two different spans of similar length: one that feels very predictable (e.g., the middle of a common phrase) and one that feels more surprising. Which takes more bits? The model was trained to minimize this total---this is the **cross-entropy loss**.

14. *(Stretch)* Divide the total bits by the number of tokens to get **bits per token**. Compare your value to the reference points above. On average, is the model more like flipping a coin or more like a near-certain prediction?
