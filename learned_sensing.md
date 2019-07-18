---
layout: page
title: Learned Sensing
permalink: /learned_sensing/
---
We have used microscopes to help us discover microscopic phenomena for hundreds of years. Thanks to the digital image sensor and computer, much of this discovery work has now started to become automated. A variety of machine learning algorithms now automatically process digital microscope images to find, classify and interpret relevant phenomena. Examples include searching for defects within electronic devices, checking for the presence of certain cells in an assay, or examining biological samples to search for indications of disease.

Despite their automation, microscopes have still changed relatively little - they are, for the most part, still optimized for a human viewer to peer through to examine a sample in detail. With infectious disease diagnosis, for example, human-based analysis of light microscope images is still the diagnostic gold standard. While human-based analysis of standard microscope images has many benefits - low-cost, simplicity, and directly interpretable results, to name a few, it also has many drawbacks – a large amount of required training, and a slow and error-prone diagnosis pipeline.

Here, we suggest an approach that can significantly improve the speed and accuracy of disease diagnosis via light microscopy. Our approach is based upon two key modifications to the standard microscope: 1) the addition of a micro-LED unit that is optimized to illuminate each sample (e.g., blood or sputum smears) to highlight important features of interest, and 2) the adoption of a deep convolutional neural network that is jointly optimized to automatically detect the presence of infection within the uniquely illuminated images.
