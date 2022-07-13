---
layout: post
title:  "Non-line-of-Sight Imaging via Neural Transient Fields"
date:   2021-01-05
categories: paper
---

## Abstract:
We present a neural modeling framework for Non-Line-of-Sight (NLOS) imaging. Previous solutions have sought to explicitly recover the 3D geometry (e.g., as point clouds) or voxel density (e.g., within a pre-defined volume) of the hidden scene. In contrast, inspired by the recent Neural Radiance Field (NeRF) approach, we use a multi-layer perceptron (MLP) to represent the neural transient field or NeTF. However, NeTF measures the transient over spherical wavefronts rather than the radiance along lines. We therefore formulate a spherical volume NeTF reconstruction pipeline, applicable to both confocal and non-confocal setups. Compared with NeRF, NeTF samples a much sparser set of viewpoints (scanning spots) and the sampling is highly uneven. We thus introduce a Monte Carlo technique to improve the robustness in the reconstruction. Comprehensive experiments on synthetic and real datasets demonstrate NeTF provides higher quality reconstruction and preserves fine details largely missing in the state-of-the-art.

# Single Photon Imaging
Single-photon imaging is a new imaging technology different from traditional cameras. Single-photon imaging acquires a single photon reflected from an object and its flight time at the picosecond level to obtain a high-dimensional transient image. As shown in the figure below, a single pixel of this transient image is a histogram, which records the number of photons per unit time, rather than the brightness represented by the usual image. Single-photon imaging can collect information that is difficult for the human eye to perceive, such as faint light, distant objects, and non-visual scenes. It is of much importance in remote sensing imaging, robotic vision, biomedical imaging, autonomous driving and other application fields.

![a](/assets/NeTF_images/1.png "Single photon imaging and its application"){:height="100%" width="100%"}
<center style="font-size:14px;color:#B0B0B0;text-decoration:underline">Single photon imaging and its application</center> 

# Non-line-of-sight 3D Reconstruction
We obtain NLOS scene information through single-photon NLOS imaging. We have analyzed the relationship between the intensity of the laser light reflected by the surface of the object and returned to the wall and time after diffuse reflection on the intermediate wall in order to restore the 3D shape of the NLOS object and surface reflection characteristics. According to whether the laser and the single-photon detector scan the same position on the intermediate wall at the same time, single-photon NLOS imaging can be divided into confocal and non-confocal settings. Many existing methods use high-dimensional transient information obtained by single-photon NLOS imaging, and view NLOS 3D reconstruction as an inverse imaging problem, which is approximately solved by deconvolution. Some methods are based on the wave optics or diffraction characteristics of light and avoid solving this inverse imaging problem. These methods have achieved good reconstruction performance, but it is difficult to restore the structural details of NLOS scenes, and non-linear phenomena such as self-occlusion and non-uniform reflection in imaging are not taken into consideration.


<!-- <img src="/NeTF_images/2.png" height="100%" width="100%"/>
</div> -->
<div align=center>
<img src="/assets/NeTF_images/2.png" height="70%" width="70%"/>
</div>
<center style="font-size:14px;color:#B0B0B0;text-decoration:underline">Single-photon NLOS imaging confocal setting. The laser scanning point and the single photon detector detecting point are at the same position on the wall</center> 

# New NLOS Imaging Model with NeTF
We have proposed a new single-photon NLOS imaging forward model, with Neural Transient Field (NeTF) to solve the inverse problem. Inspired by the recent research Neural Radiation Field (NeRF, [Mildenhall 2020ECCV]), based on volume rendering theory, the NLOS scene is expressed as the weight of a fully connected neural network, and transient data is used as input for training and learning. The density distribution of the NLOS scene and the reflectivity with the characteristics of the viewing angle can realize 3D reconstruction of the NLOS scene. Different from existing methods, NeTF can continuously represent and perform differentiable calculations, realize NLOS reconstruction at any resolution, and can also deal with self-occlusion and non-uniform reflection phenomena.

NeTF consists of two parts. Firstly, according to the known illumination point and detection point position on the intermediate wall, sampling is performed in the space represented by the spherical coordinate system, and then the sampling coordinates are converted to the Cartesian coordinate system to better describe the geometry and viewing angle characteristics of the object. Secondly, we input the sampling points represented by these rectangular coordinate systems into the fully connected neural network and single-photon non-view imaging model. Following the proposed imaging model, we calculate the predicted transient data, and minimize the difference between the predicted and measured transient data to optimize the neural network to obtain the density distribution and reflectivity of the NLOS field scene.

![c](/assets/NeTF_images/3.png "Pipeline of NeTF"){:height="100%" width="100%"}
<center style="font-size:14px;color:#B0B0B0;text-decoration:underline">Pipeline of NeTF</center> 

# Two-stage Training and Hierarchical Sampling

We have found that the data is imbalanced in the neural network training process, which leads to poor reconstruction of self-occluded NLOS scenes. To address the problem, we have proposed a two-stage training strategy, that is, the importance of each sample is analyzed from the training results of the first stage, and the transient data is resampled in the second stage to achieve balanced data. Besides, a Hierarchical sampling method is also proposed, which allocates more sampling points to the space with higher probability of NLOS scenes in order to improve the sampling efficiency and reconstruction accuracy. The NeTF method is based on deep learning, which can not only obtain better reconstruction effects than existing methods, but also deal with self-occlusion and non-uniform reflections, and realize NLOS 3D reconstruction with any resolution in confocal or non-confocal setting.

![d](/assets/NeTF_images/4.png "Performance of NeTF vs. SOTA methods on syhthetic data and real data"){:height="100%" width="100%"}
<center style="font-size:14px;color:#B0B0B0;text-decoration:underline">Performance of NeTF vs. SOTA methods on syhthetic data and real data</center> 

<!-- ![setting](/_posts/image16_setting.png "Magic Gardens") -->
<!-- ![a](/images/1.png){:height="70%" width="70%"} -->
<!-- ![b](/images/image16_setting.png){:height="100%" width="100%"} -->
<!-- ![b](_posts/image16_setting.png "RUNOOBb")
![c](/image16_setting.png "RUNOOBc")
![d](image16_setting.png "RUNOOBd") -->

Check out the [arXiv Page][arXiv] for more information. The code is available at [Code Release][code].

[arXiv]: https://arxiv.org/abs/2101.00373
[code]: https://github.com/zeromakerplus/NeTF_public
