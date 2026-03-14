# LM Internals Visualizer — Feature Spec

Spec for the "Show Internals" tool to support the Exploring Language Models activity.

## Input

- A text box where the user types a message (the "user turn").
- The tool wraps this in the chat template (e.g., `<start_of_turn>user\n...\n<end_of_turn>\n<start_of_turn>model\n`) and displays the full token sequence.

## Core Display

**Token sequence view**: The full document (system/user/assistant tokens) displayed as a horizontal or wrapped sequence of individual tokens. Special tokens (role markers, turn delimiters) should be visually distinct (e.g., dimmed, smaller, or a different color).

Each token in the assistant's response should have a **background color or bar** indicating how confident the model was at that position (e.g., green = high probability, red/orange = low probability).

## Interactions

### 1. Inspect a token's distribution

**Click any token** in the sequence to see the model's predicted next-token distribution *at that position*. Display:
- A ranked list of the top ~10 candidate tokens with their probabilities.
- The probability assigned to the token that actually came next (highlighted in the list if it's in the top 10, otherwise shown separately).
- The surprise in bits: $-\log_2(p)$ for the actual next token.

### 2. Build response token by token

When the assistant response area is active (after the user turn), the tool shows the next-token distribution and lets the user **click a candidate token to append it** to the response. This repeats: after each token is chosen, the tool runs the model again and shows the new distribution.

Required controls:
- **Pick token**: Click any token in the candidate list to append it.
- **Auto-complete**: A button to let the model pick the rest (always choosing the top token, or sampling — either is fine).
- **Reset response**: Clear the assistant's tokens and start over from the end of the user turn.
- **Undo**: Remove the last appended token and go back to the previous distribution.

### 3. Select a span and compute total bits

**Click and drag** (or shift-click) to select a contiguous span of tokens in the response. When a span is selected, display:
- Number of tokens selected.
- Total bits: $\sum -\log_2(p_i)$ across the selected tokens.
- Bits per token: total bits / number of tokens.

## Model

Use the same model already in the tool (Gemma 2B or similar). The model must return log-probabilities for the top-k tokens at each position. If the model is already running in the backend, this just needs the logprobs to be surfaced in the UI.

## Non-requirements (out of scope for now)

- Temperature control (we'll address this in a later activity).
- Editing the user message after generation has started (just reset).
- Multiple conversation turns (one user message → one assistant response is sufficient).
- Showing the full vocabulary distribution (top 10–20 is enough).
