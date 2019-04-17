# Changing Texture: : Integrating Long-range Correlation into Dynamic Texture Synthesis

## Team members: Kaitai Zhang, Bin Wang, Santiago Carvajal, Jiajun Xu, Jingbo Sun**

## Introduction:

Dynamic texture synthesis aims to synthesize dynamic texture video given a short video of target dynamic texture. It has been a problem of interest in human perception, computer vision, and pattern recognition for the past several years. Several models [1][2] have been published recently which employ deep learning techniques targeting on the dynamic texture problem.

Here we point out one major drawback of current model [1], which is that the model will collapse on texture examples with long-range structure. The root cause of this issue is that the Gram loss, used in this model, fails to capture and describe structure information effectively. To solve this problem and extend the model’s capability, we adapted the deep Gram correlation loss into the current model inspired by [3].

## Problem Formulation and Approach:

The problem of how to maintain non-local and non-stationary textural structure has been studied before in the static texture synthesis domain [3][4]. Generally speaking, there are some modifications to the original Gram loss to capture long-range correlation.
Let I denote the target texture. Extracting the Gram matrix involves running an image I forward through a neural network, which yields the deep features. We denote the nth feature channel of the lth layer by fl,n . Using the Gram matrix, between n and the n’ feature channel

<p align="center">
  <img src="https://user-images.githubusercontent.com/35282488/56315962-fbe3f300-610d-11e9-974a-aeae6bb0755a.png">
 </p>

where q and m are the indices running across the Q × M feature map.

Motivated by the fact that the Gram matrix only makes use of inter-feature correlations whereas image structures are represented by the intra-feature correlations. The deep correlation is defined by the following equation:

<p align="center">
  <img src="https://user-images.githubusercontent.com/35282488/56317466-af9ab200-6111-11e9-84b4-7883ac388e53.png">
 </p>
 
 which shift pixel i vertically and pixel j pixel horizontally, then applying a pointwise multiplication across the overlapping regions. Also, for each image patch, they are weighted by the inverse of the total size of overlapping regions. More details of the deep correlation loss and some demonstrations could be found in the original paper, and this method have been validated to be effective in static texture synthesis domain. This loss manipulates the image by rotating it, flipping it, etc, to obtain better spatial results.

Our approach is to modify Tesfaldet et. al. model [1] by substituting R_(i,j)^(l,n) into the loss function instead of the original Gram loss used in their model. This will allow us to better capture spatio-temporal features of the synthesized dynamic texture, allowing a better rendering of textures such as those shown in Figure 2. 
