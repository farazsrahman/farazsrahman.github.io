---
layout: post
title:  "Decision Making Diffusion Models"
date:   2024-10-19 10:00:00 -0700
categories: Project
---

<div style="display: flex; justify-content: center; margin: 15px 0;">
    <img src="/images/diffusion.png" alt="Diffusion image" width="600">
</div>

(Note: this blog  will temporarily serve as a summary of the main results, while I am still working on the write up)


Diffusion models (DMs) in their various forms have become extremely powerful tools to generatively sample from high-dimensional distributions. Originally DMs were designed to sample from the space of [images](https://arxiv.org/abs/2006.11239), but more recent work have brought applications in sampling [motion plans](https://diffusion-policy.cs.columbia.edu/), [biochemical structures](https://www.nature.com/articles/s41586-024-07487-w) and more. While there is rich theory going back to the (insert time) on the time-reversed Langevin process, most recent works abstract the away the diffusion trajectory and focus study on the quality of the generated sample leaving open questions about insight we might gain from studying diffusion trajectories.

This project aims to provide preliminary answers to two questions. The first naturally arises from the fact that diffusion is a time-variant process: given a set of features from a diffusion sample, which were generated earlier and which later? To answer this question we study the decline in variance over time of a DM output by conditioning on some prefix of a given diffusion trajectory.


<figure style="display: flex; flex-direction: column; align-items: center; margin: 20px 0; max-width: 100%;">
    <img src="/images/butterfly_variance.png" alt="Butterfly variance" style="max-width: 90%; height: auto;">
    <figcaption style="margin-top: 8px; text-align: center; font-family: 'Times New Roman', Times, serif; color: #000000; font-size: 12px; max-width: 90%; word-wrap: break-word;">
        In the example above the variance of the interior of the butterfly's wing (i.e. it's texture and color) shrink to zero far quicker than the shape of the wing.
    </figcaption>
</figure>


We find that the variance of certain features drop significantly earlier than others in a couple of data sets suggesting that those features were generated first and can be thought of as a prior when generating later features.

The second question follows from the first. Can we use this above ordering to break down our diffusion trajectory into smaller piece wise linear components using system identification? 
If so, can techniques from control theory and linear systems provide insight into how features influence each other through the diffusion process? Our results here are more rudimentary, but we hope that it may provide useful intuition to a practitioner or inspire future work.

<!-- <figure style="display: flex; flex-direction: column; align-items: center; margin: 20px 0; max-width: 100%;">
    <img src="/images/block_spectral_norm.png" alt="Butterfly variance" style="max-width: 90%; height: auto;">
    <figcaption style="margin-top: 8px; text-align: center; font-family: 'Times New Roman', Times, serif; color: #000000; font-size: 12px; max-width: 90%; word-wrap: break-word;">
        The plot above shows the spectral norms over time in the piece-wise linearization of a DM trajectory. Specifically these are the influences of each feature on the fourth feature of a generated dataset of block bisections (see below).  
    </figcaption>
</figure> -->


In asking these questions, we also generated a toy dataset of block bisections (see below) to test if diffusion trajectories could faithfully learn interdependencies encoded in how we generated the block data.

<figure style="display: flex; flex-direction: column; align-items: center; margin: 20px 0; max-width: 100%;">
    <img src="/images/generated_blocks.png" alt="Butterfly variance" style="max-width: 90%; height: auto;">
    <figcaption style="margin-top: 8px; text-align: center; font-family: 'Times New Roman', Times, serif; color: #000000; font-size: 12px; max-width: 90%; word-wrap: break-word;">
        Here are a couple sample generations of the 32x32 block - bisection toy dataset that we concstructed. Features in the spectral norm plot above correspond to different 4x32 layers in the above samples.
    </figcaption>
</figure>

The general theme of the results here suggest that DMs partake is some form of reasoning as the forward process occurs. Further exposition of this idea will be available in a formal write up soon.