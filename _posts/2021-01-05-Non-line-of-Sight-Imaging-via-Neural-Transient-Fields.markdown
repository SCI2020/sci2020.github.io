---
layout: post
title:  "Non-line-of-Sight Imaging via Neural Transient Fields"
date:   2021-01-05
categories: paper
---
We present a neural modeling framework for Non-Line-of-Sight (NLOS) imaging. Previous solutions have sought to explicitly recover the 3D geometry (e.g., as point clouds) or voxel density (e.g., within a pre-defined volume) of the hidden scene. In contrast, inspired by the recent Neural Radiance Field (NeRF) approach, we use a multi-layer perceptron (MLP) to represent the neural transient field or NeTF. However, NeTF measures the transient over spherical wavefronts rather than the radiance along lines. We therefore formulate a spherical volume NeTF reconstruction pipeline, applicable to both confocal and non-confocal setups. Compared with NeRF, NeTF samples a much sparser set of viewpoints (scanning spots) and the sampling is highly uneven. We thus introduce a Monte Carlo technique to improve the robustness in the reconstruction. Comprehensive experiments on synthetic and real datasets demonstrate NeTF provides higher quality reconstruction and preserves fine details largely missing in the state-of-the-art.

test

<!-- ![setting](/_posts/image16_setting.png "Magic Gardens") -->
![a](/assets/screenshot.jpg)
<!-- ![b](_posts/image16_setting.png "RUNOOBb")
![c](/image16_setting.png "RUNOOBc")
![d](image16_setting.png "RUNOOBd") -->

Check out the [arXiv Page][arXiv] for more information.

[arXiv]: https://arxiv.org/abs/2101.00373
