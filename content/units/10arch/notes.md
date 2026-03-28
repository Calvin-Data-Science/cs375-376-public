---
title: "Notes: Neural Architectures"
weight: 2
revised: 2026
---

These notes are reference material for Unit 3 (Architectures). The primary focus of class is self-attention and Transformers; these notes cover other architectures for comparison.

## Deep Neural Net = Stack of Layers

Neural networks are built from modular components, often connected sequentially:

- Linear transformation ("Dense", "fully connected")
- Multiple linear layers: MLP / "Feed-forward"
- Convolution and Pooling
- Self-Attention
- Recurrent (RNN, LSTM)
- Normalization (BatchNorm, LayerNorm)
- Dropout

The key difference between architectures is their **connectivity structure**:

- **Fully Connected**: Perceptron, MLP --- every input connects to every output within a layer
- **Fixed Local Connections**: Convolutional networks (CNN) --- local spatial connections
- **Fixed Temporal Connections**: Recurrent networks (RNN) --- information flows forward through time
- **Dynamic Connections**: [Transformer](https://nlp.seas.harvard.edu/annotated-transformer/) --- connections are computed on the fly via attention

## Feed-Forward / MLP

A feed-forward network (or multi-layer perceptron) is a stack of linear transformations with nonlinearities between them:

$$f(x) = f_2(\text{ReLU}(f_1(x)))$$

where $f_1$ and $f_2$ are both linear transformations ($f_i(x) = x W_i + b$) and $\text{ReLU}(x) = \max(0, x)$ applied elementwise. Other nonlinearities (GELU, SiLU, etc.) are sometimes used instead of ReLU.

**Key properties:**

- **Universal function approximator** --- can represent any function in principle, but not necessarily *efficiently*
- Fixed information flow within each layer

### Applying an MLP to a Sequence

There are two options for processing a sequence with an MLP:

| | Option 1: Concatenate | Option 2: Per-element |
|---|---|---|
| **Approach** | Concatenate the sequence into one giant vector | Apply the MLP to each element independently |
| **Interactions** | Can capture interactions between elements | Cannot capture interactions between elements |
| **Variable length** | Cannot handle variable-length sequences | Can handle variable-length sequences |
| **Parameters** | Huge number of parameters | Fewer parameters (reuse the same weights for each element) |

In Transformers, the MLP layers use Option 2 (applied independently to each position). Information sharing between positions happens in the attention layers instead.

## Convolutional Networks (CNN)

A convolutional layer is essentially a feed-forward network applied to a small *patch* (or "window") of the input, slid across the entire input to produce many outputs.

**Key properties:**

- Information flow is fixed but **local** --- each output depends only on a small neighborhood of the input
- **Parallel** --- all patches can be computed at the same time
- Summarize regions of the input via **pooling** (e.g., take the max or average over a region)
- Efficient at inference time
- Excellent for data with spatial structure (images, audio spectrograms)

**How they work:** A small set of learnable weights (the "kernel" or "filter") slides across the input. At each position, the kernel computes a weighted sum of the local patch. Different kernels detect different features --- edges, textures, patterns. Stacking multiple convolutional layers lets the network build up from simple local features to complex high-level concepts.

### Resources

- [Image Kernels explained visually](https://setosa.io/ev/image-kernels/) --- interactive demo of what convolution does to an image
- [CS231n: Convolutional Neural Networks for Visual Recognition](https://cs231n.github.io/convolutional-networks/) --- how to use convolutions in a neural network
- [Feature Visualization](https://distill.pub/2017/feature-visualization/) --- what convolutional networks learn at each layer

## Recurrent Networks (RNN, LSTM)

A recurrent network processes a sequence **one step at a time**, maintaining a "hidden state" that summarizes everything seen so far. At each time step, the network takes the current input and the previous hidden state, and produces an updated hidden state and an output.

**Key properties:**

- **Sequential** processing --- one step at a time
- Maintains and updates a **hidden state** that acts as a compressed memory of the sequence so far
- Can handle **variable-length sequences** naturally
- Efficient at inference time (constant memory per step)
- **Difficult to learn long-range dependencies** --- information from early in the sequence tends to get "washed out" as the hidden state is updated many times

**LSTM (Long Short-Term Memory)** is a variant of RNN designed to mitigate the long-range dependency problem. It uses a gating mechanism to selectively remember or forget information, which helps gradients flow over longer sequences. LSTMs were the dominant architecture for sequence tasks (translation, speech recognition, text generation) before Transformers.

## Compare and Contrast

| | MLP | CNN | RNN/LSTM | Transformer |
|---|---|---|---|---|
| **Connectivity** | Fully connected | Local (spatial neighbors) | Temporal (previous step) | Dynamic (learned attention) |
| **Sequence handling** | Fixed length (concatenate) or no interaction (per-element) | Local context via sliding window | Naturally sequential, variable length | Full context, variable length |
| **Parallelism** | Fully parallel | Fully parallel | Sequential (hard to parallelize) | Fully parallel |
| **Long-range dependencies** | Only if concatenated (expensive) | Requires many stacked layers | Difficult (vanishing gradients) | Direct (any token attends to any other) |
| **Parameter sharing** | None across positions | Same kernel at all positions | Same weights at all time steps | Same attention weights at all positions |
| **Primary strength** | Simple, general | Spatial/local patterns | Sequential data with short-range dependencies | Flexible, scalable, long-range |
| **Classic applications** | Tabular data, small models | Image recognition, object detection | Early machine translation, speech | Modern LLMs, vision (ViT), multimodal |

### When to Use Each

- **MLP**: When inputs are fixed-size and there is no meaningful spatial or sequential structure (e.g., tabular data). Also used as a component *within* other architectures (the "FFN" layers in a Transformer).
- **CNN**: When the data has local spatial structure and translation invariance matters (e.g., detecting an object regardless of where it appears in an image). Still widely used in computer vision, sometimes combined with Transformers.
- **RNN/LSTM**: Largely superseded by Transformers for most tasks, but still relevant for streaming/real-time applications where you process one element at a time and need constant memory. Recent "state space models" (like Mamba) revive some RNN ideas with better parallelism.
- **Transformer**: The default choice for most modern deep learning tasks, especially in NLP. Scales well with data and compute. The key advantage is that attention lets the model learn *which* parts of the input to focus on, rather than relying on fixed connectivity patterns.
