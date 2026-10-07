---
layout: page
title: C++ Transformer w/ Inference Endpoint
description: AI Infra and C++
img: assets/img/attention.png
importance: 1
category: work
related_publications: true
---

This was a project I did in order to futher solidify my C++ skills and gain greater intuition into the theory behind LLMs.

I started it after reading _Attention Is All You Need_, because I wanted to know what **PyTorch** and **TensorFlow** abstract away.

End to end, it takes raw Shakespeare sonnets, learns to predict the next token, and serves generated text over a REST endpoint. In this project, I:

- Implemented a Transformer language model from scratch in **C++**, including single-head attention, cross-entropy loss, and layer normalization, using **Eigen** matrix operations
- Built a custom word-level tokenizer that constructs vocabularies of **5,000+** tokens from **10,000** lines of raw text using `std::vector` and `std::unordered_map`
- Designed a binary model serialization pipeline and engineered a REST inference endpoint with **Crow**, enabling real-time text generation from saved model weights

### The model

Every piece of the architecture is there for a reason, and writing each one by hand made those reasons obvious:

- **Token embeddings** turn each token ID into a dense vector, which is what the Transformer actually operates on
- **Sinusoidal positional encodings** give the model a sense of where a token sits in the sequence, since attention on its own has no notion of order
- **Single-head self-attention** learns a query, key, and value vector per token, then uses scaled dot-product scores to weight the values into a contextual representation. A causal mask keeps the model from peeking at future tokens
- **Feedforward layers** transform each token independently after attention, letting the model learn richer per-token representations
- **Residual connections** preserve information across blocks, so the model learns refinements rather than relearning everything
- **Layer normalization** standardizes each representation to zero mean and unit variance, which made training converge much faster

### Training and inference

Training examples came from sliding windows over the token ID sequence, where the target is the input shifted forward by one token — plain autoregressive language modeling. Each step clears gradients, runs a forward pass, applies softmax, computes cross-entropy loss against the target, backpropagates, and updates parameters with **SGD**. Every operation I wrote needed a differentiable counterpart, which was the hardest and most instructive part.

Serialization saves the model configuration, the Eigen weight matrices, and the tokenizer vocabulary, so inference sees the exact same token-to-ID mapping as training. The **Crow** server loads all three on startup and exposes a POST endpoint that takes a prompt and a token limit, greedily samples the highest-probability token, appends it to the context, and repeats until it hits the limit or an end token.

The repo can be found [here](https://github.com/Dodesimo/CPPTransformer).
