# Changing Texture: : Integrating Long-range Correlation into Dynamic Texture Synthesis

## Team members: Kaitai Zhang, Bin Wang, Santiago Carvajal, Jiajun Xu, Jingbo Sun**

## Introduction:

Dynamic texture synthesis aims to synthesize dynamic texture video given a short video of target dynamic texture. It has been a problem of interest in human perception, computer vision, and pattern recognition for the past several years. Several models [1][2] have been published recently which employ deep learning techniques targeting on the dynamic texture problem.

Here we point out one major drawback of current model [1], which is that the model will collapse on texture examples with long-range structure. The root cause of this issue is that the Gram loss, used in this model, fails to capture and describe structure information effectively. To solve this problem and extend the model’s capability, we adapted the deep Gram correlation loss into the current model inspired by [3].

## Problem Formulation and Approach:

The problem of how to maintain non-local and non-stationary textural structure has been studied before in the static texture synthesis domain [3][4]. Generally speaking, there are some modifications to the original Gram loss to capture long-range correlation.
Let I denote the target texture. Extracting the Gram matrix involves running an image I forward through a neural network, which yields the deep features. We denote the nth feature channel of the lth layer by fl,n . Using the Gram matrix, between n and the n’ feature channel

<div style="text-align: center;">
![image](https://user-images.githubusercontent.com/35282488/56315962-fbe3f300-610d-11e9-974a-aeae6bb0755a.png)
</div>
