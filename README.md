# Changing Texture: : Integrating Long-range Correlation into Dynamic Texture Synthesis

**Team members: Kaitai Zhang, Bin Wang, Santiago Carvajal, Jiajun Xu, Jingbo Sun**

**Purpose**
Dynamic texture synthesis aims to synthesize dynamic texture video given a short video of target dynamic texture. It has been a problem of interest in human perception, computer vision, and pattern recognition for the past several years. Several models [1][2] have been published recently which employ deep learning techniques targeting on the dynamic texture problem.
Here we point out one major drawback of current model [1], which is that the model will collapse on texture examples with long-range structure. We believe the root cause of this issue is that the Gram loss, used in this model, fails to capture and describe structure information effectively. To solve this problem and extend the model’s capability, we propose to adapt the deep correlation loss into the current model inspired by [3].
