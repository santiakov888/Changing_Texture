---
layout: page
title: Changing Texture: : Integrating Long-range Correlation into Dynamic Texture Synthesis
permalink: /about/
---

Team members: Kaitai Zhang, Bin Wang, Santiago Carvajal, Jiajun Xu, Jingbo Sun**

### Introduction:

Dynamic texture synthesis aims to synthesize dynamic texture video given a short video of target dynamic texture. It has been a problem of interest in human perception, computer vision, and pattern recognition for the past several years. Several models [1][2] have been published recently which employ deep learning techniques targeting on the dynamic texture problem.

Here we point out one major drawback of current model [1], which is that the model will collapse on texture examples with long-range structure. The root cause of this issue is that the Gram loss, used in this model, fails to capture and describe structure information effectively. To solve this problem and extend the model’s capability, we adapted the deep Gram correlation loss into the current model inspired by [3].

### Problem Formulation and Our Approach

We will first briefly introduce the model from [1] which we modified in this project. As illustrated in Figure 1, this model is constructed from two convolutional networks (CNNs), an appearance stream and a dynamics stream, which have been pre-trained for object recognition and optical flow prediction respectively. Similar to previous work on spatial textures synthesis, it summarizes an input dynamic texture in terms of a set of spatio-temporal statistics of filter outputs (Gram matrices) from each stream, and then build a dictionary for every texture of interest as the training process.



### Contact me

[email@domain.com](mailto:email@domain.com)
