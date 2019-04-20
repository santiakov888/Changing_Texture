# Changing Texture: Integrating Long-range Correlation into Dynamic Texture Synthesis

## Team members: Kaitai Zhang, Bin Wang, Santiago Carvajal, Jiajun Xu, Jingbo Sun

## Summary

Dynamic texture synthesis aims to synthesize dynamic texture video given a short video of target dynamic texture. It has been a problem of interest in human perception, computer vision, and pattern recognition for the past several years. Several models [1][2] have been published recently which employ deep learning techniques targeting on the dynamic texture problem. However, these models fail on textures that have spatial consistencies. We have identified that this shortcoming is due to the Gram Loss used in their models. Thus, we have attempted to solve this problem by incorporating horizontal, vertical, and rotational loss terms to the Gram Loss used in [1], forcing the neural network to account for spatial consistencies.

Our results are shown below in Figure 1. As seen in this figure it we are able to produce significantly better results with the addition of the extra terms to the Gram Loss., with the loss with all the terms performing the best, followed by the results with only horizontal and vertical terms being added. However, the price for achieving better results in this case are that the number of parameters that need to be inputed are greater, and each parameter needs to be finetuned to achieve optimal results. 

## Introduction:

Dynamic texture synthesis aims to synthesize dynamic texture video given a short video of target dynamic texture. It has been a problem of interest in human perception, computer vision, and pattern recognition for the past several years. Several models [1][2] have been published recently which employ deep learning techniques targeting on the dynamic texture problem.

Here we point out one major drawback of current model [1], which is that the model will collapse on texture examples with long-range structure. The root cause of this issue is that the Gram loss, used in this model, fails to capture and describe structure information effectively. To solve this problem and extend the model’s capability, we adapted the deep Gram correlation loss into the current model inspired by [3].

## Nerual Network Model

XXXXXXXXxMaybe add some specifics about the model itself here?XXXXXXXXXXXXXXX

We will first briefly introduce the model from [1] which we modified in this project. As illustrated in Figure 1, this model is constructed from two convolutional networks (CNNs), an appearance stream and a dynamics stream, which have been pre-trained for object recognition and optical flow prediction respectively. Similar to previous work on spatial textures synthesis, it summarizes an input dynamic texture in terms of a set of spatio-temporal statistics of filter outputs (Gram matrices) from each stream, and then build a dictionary for every texture of interest as the training process. This architecture is inspired by psychophysical studies which have suggested that humans process object recognition and motion independently (called the two-stream hypothesis [5]).

<p align="center">
  <img src="https://user-images.githubusercontent.com/35282488/56317720-45ced800-6112-11e9-85bc-1cfeea11d634.png">
</p>
<p align="center">
  Figure 1: Two-stream convolutional networks for dynamic texture synthesis
</p>

During the synthesis process, it optimizes a randomly initialized noise pattern such that its spatio-temporal statistics from each stream match those of the input texture. Unlike normal CNN, this model conducts Gradient Descent and Back-propagation during the synthesis process, and it optimizes each pixel in the input noise pattern to match the spatio-temporal statistics. Meanwhile, all the parameters from object recognition and optical flow prediction network are pre-trained and remain fixed during the synthesis process.

## Approach:

There two critical requirements to synthesize perceptually natural textures: spatial consistency and temporal consistency. This model fails to keep spatial consistency, thus cannot succesfully render texturesand when the target has long-range structure within each frame. The reason is that they use the Gram loss in the appearance stream only computes the inter-feature correlation and erases all spatial information.

The problem of how to maintain non-local and non-stationary textural structure has been studied before in the static texture synthesis domain [3][4]. Generally speaking, there are some modifications to the original Gram loss to capture long-range correlation.
Let I denote the target texture. Extracting the Gram matrix involves running an image I forward through a neural network, which yields the deep features. We denote the nth feature channel of the lth layer by fl,n . Using the Gram matrix, between n and the n’ feature channel

<p align="center">
  <img src="https://user-images.githubusercontent.com/35282488/56315962-fbe3f300-610d-11e9-974a-aeae6bb0755a.png">
 </p>

where q and m are the indices running across the Q × M feature map.

Motivated by the fact that the Gram matrix only makes use of inter-feature correlations whereas image structures are represented by the intra-feature correlations. The deep correlation is defined by the following equation:

<img src="https://latex.codecogs.com/svg.latex?\Large&space;x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" title="\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" />


<p align="center">
  <img src="https://user-images.githubusercontent.com/35282488/56317466-af9ab200-6111-11e9-84b4-7883ac388e53.png">
 </p>
 
which shift pixel i vertically and pixel j pixel horizontally, then applying a pointwise multiplication across the overlapping regions. Also, for each image patch, they are weighted by the inverse of the total size of overlapping regions. More details of the deep correlation loss and some demonstrations could be found in the original paper, and this method have been validated to be effective in static texture synthesis domain. This loss manipulates the image by rotating it, flipping it, etc, to obtain better spatial results.

Our approach was to modify Tesfaldet et. al. model [1] by substituting R_(i,j)^(l,n) into the loss function instead of the original Gram loss used in their model. This allowed us to better capture spatio-temporal features of the synthesized dynamic texture, allowing a better rendering of textures such as those shown in Figure 2. 

## Experimentation:

We experimented with two different loss functions to incorporate spatio-temporal features. The first loss function only incorporates horizontal and vertical spatial consintecies to the Gram Loss function. The second loss function adds rotational loss terms to the our first loss function. Figure 2 below shows the results from our experimentation. The leftmost video shows the original video, the next video is the rendered video by [1], next video shows result from first loss, and last video shows video from second loss.
