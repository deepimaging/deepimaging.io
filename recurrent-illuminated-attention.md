---
layout: page
title: "Towards an Intelligent Microscope: Adaptively Learned Illumination for Optimal Sample Classification"
permalink: /recurrent-illuminated-attention

---
#### Amey Chaware<sup>1,+</sup>, Colin L. Cooke<sup>1,+</sup>, Kanghyun Kim<sup>1</sup>, Roarke Horstmeyer<sup>1,2</sup>
*1: Department of Electrical and Computer Engineering, Duke University, Durham NC, USA.*
*2: Department of Biomedical Engineering, Duke University, Durham NC, USA.*
*+ denotes equally contributing authors*

#### Abstract
Recent machine learning techniques have dramatically changed how we process digital images. However, the way in which we capture images is still largely driven by human intuition and experience. This restriction is in part due to the many available degrees of freedom that alter the image acquisition process (lens focus, exposure, filtering, etc). Here we focus on one such degree of freedom - illumination within a microscope - which can drastically alter information captured by the image sensor. We present a reinforcement learning system that adaptively explores optimal patterns to illuminate specimens for immediate classification. The agent uses a recurrent latent space to encode a large set of variably-illuminated samples and illumination patterns. We train our agent using a reward that balances classification confidence with image acquisition cost. By synthesizing knowledge over multiple snapshots, the agent can classify on the basis of all previous images with higher accuracy than from naively illuminated images, thus demonstrating a smarter way to physically capture task-specific information.

![Our setup](/projects/rl-illumination/agent_env_small.png)


#### Code and Data
[Github](https://github.com/clvcooke/recurrent-illuminated-attention)

[Fourier MNIST Dataset](https://www.kaggle.com/clvcooke/fourier-mnist-hard)

[Malaria Dataset](https://www.kaggle.com/clvcooke/fourier-malaria)
