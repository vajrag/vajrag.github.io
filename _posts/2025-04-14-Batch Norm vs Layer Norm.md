---
title: "Understanding Activation Normalization in Deep Learning"
date: 2025-04-14
layout: single
classes: wide
author_profile: true
read_time: true
tags: [Deep Learning, Notes]
---

Deep neural networks are difficult to train. As they grow deeper, they become increasingly prone to issues like `exploding gradients`, `internal covariant shift`, and `vanishing gradients`. One powerful family of techniques that helps tame this complexity is **Activation Normalization**.

In this post, we will break down:
- What is normalization of activation functions?
- Why do we normalize them?
- Common normalization techniques - including BatchNorm, LayerNorm and others -- with an in-depth comparison.

---

## What is Normalization of Activations?

Activation normalization refers to the process of scaling and shifting the outputs (activations) of neurons during training so that they follow a specific distribution — usually with zero mean and unit variance.

Formally, given an input x, we normalize it using:

$$
\hat x = \frac{x - \mu}{\sigma + \epsilon}
$$

where:
- $\mu$ is the mean
- $\sigma$ is the standard deviation
- $\epsilon$  is a small constant for numerical stability

This is usually followed by learnable affine parameters $\gamma$ (scale) and $\beta$ (shift):

$$
\text{Normalized Output} = \gamma \cdot \hat x + \beta
$$

---

## Why do we Normalize Activations?

Training deep networks can suffer from *internal covariate shift* — a phenomenon where the distribution of inputs to each layer keeps changing as parameters update. 

Let's break down *Internal Covariate Shift* with a simple example. 

#### Internal Covariate Shift

Refers to the change in the distribution of activations (inputs to each hidden layer in the neural network) as the model trains. This forces each layer to constantly adapt to new distributions, making optimization slower and harder. 

Let's say we have a 3-layer feedforward neural network:

> Layer1: Input -> Hidden 1 -> Activation function 1 <br>

> Layer2: Activation function 1 -> Hidden layer 2 -> Activation function 2 <br>

> Layer3: Activation function 2 -> Output <br>


Now assume we initialize weights randomly and start training. Here is what can happen:

1. <ins>Early Training</ins>
    - Input data has a nice distribution (e.g., say Mnist Digits has pixel values scaled between 0 an 1)
    - Layer 1 processes it -> produces some activation values (let's say with a mean ~0.5 and std ~0.2)
    - Layer 2 receives these activations and learns accordingly. 


2. <ins>A Few Epochs Later</ins>
    - Layer 1's weights have now updated - it now outputs activations with mean ~2.0 and std ~1.5
    - Layer 2 suddenly receives a very different distribution than what it originally trained on
    - Its weights are no longer optimal for this new input - it must now adjust again

![Internal Covariate Shift](/assets/images/posts/internal_covariate_shift.png)

This shift in activation distribution from Layer 1 -> Layer 2 is the Internal Covariance Shift. If this is happening it can lead to 
- Graidents exploding or vanishing
- Learning becomes slower 
- Models become sensitive to initialization 

---
## Popular Activation Normalization Techniques 

In this section, we will explore some of the main techniques for normalizing activations. 

### Batch Normalization (BatchNorm)

Batch Normalization was proposed in 2015. It works by normalizing across the batch dimension. I.e, for each feature/channel across all samples in the batch. 

Let's visualize 🔍






