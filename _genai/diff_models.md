---
title: "Diffusion Models"
layout: single
classes: wide
permalink: /genai/diff_models/
author_profile: true
read_time: true
---

In recent years, diffusion models have quietly become the backbone of some of the most breathtaking AI-generated images — from hyper-realistic portraits to surreal dreamscapes. You’ve likely seen their magic behind tools like DALL·E 2, Stable Diffusion, and MidJourney.

But how do these models actually work? What makes them different from GANs and VAEs? And why are they so good at controlled, high-fidelity generation?

Let’s break it down.

---

## Intuition Behind Diffusion Models 

At their core, diffusion models learn to reverse a slow, stochastic destruction of data.

- Imagine taking an image and adding tiny bits of Gaussian noise to it over and over again - until it becomes pure noise 
- Now imagine trying to learn how to undo that process - step-by-step - untilwe regenerate the original image. 

Diffusion models to exactly that. 

## Forward and Reverse Processes

There are two stages in diffusion:
- **Forward Process(Diffusion)**: Adds noise to data step-by-step. This is a fixed, non-learned process. After enough steps, the data becomes nearly Gaussian noise.
- **Reverse Process(Denoising)**: This is where learning happens. A neural network is trained to predict the original image from the noisy version, gradually removing noise over several steps.

This sequential denoising is what allows diffusion models to generate crisp, detailed outputs.


