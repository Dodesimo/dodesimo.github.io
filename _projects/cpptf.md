---
layout: page
title: C++ Transformer w/ Inference Endpoint
description: AI Infra and C++  
img: assets/img/attention.png
importance: 1
category: work
related_publications: true
---

This was a project I did in order to futher solidify my C++ skills and gain greater intuition into the theory behind LLMs. In this project, I: 

- Implemented a Transformer language model from scratch in **C++**, including single-head attention, cross-entropy loss, and layer normalization, using **Eigen** matrix operations
- Built a custom word-level tokenizer that constructs vocabularies of **5,000+** tokens from **10,000** lines of raw text using `std::vector` and `std::unordered_map`
- Designed a binary model serialization pipeline and engineered a REST inference endpoint with **Crow**, enabling real-time text generation from saved model weights

The repo can be found [here](https://github.com/Dodesimo/CPPTransformer).