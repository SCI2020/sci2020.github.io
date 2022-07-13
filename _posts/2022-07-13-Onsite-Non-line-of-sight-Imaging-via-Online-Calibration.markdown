---
layout: post
title:  "Onsite Non-line-of-sight Imaging via Online Calibration"
date:   2022-07-13
categories: paper
---

## Abstract:
There has been increasing interest in deploying non-line-of-sight (NLOS) imaging systems for recovering objects hidden behind corners. Existing solutions need to calibrate the imaging system using auxiliary apparatus and additional detectors. We present an online calibration technique that directly decouples the transients, which are acquired by onsite scanning on a relay surface, into line-of-sight (LOS) and hidden components. We use the former to directly (re-)calibrate the system upon changes of scene--surface configurations, scannable regions, and sampling patterns, and the latter for hidden object recovery via spatial-, frequency-, or learning-based techniques. We also calculate a *Gamma* map from the LOS component to preview calibration effects for accurate transient measurements. Our technique avoids using auxiliary calibration tools such as mirrors or checkerboards and supports both uniform and non-uniform sampling in our onsite NLOS imaging system. Comprehensive experiments via calibration evaluation and NLOS reconstruction demonstrate the efficiency and effectiveness of our solution.
Besides, we have made our data and code open-source on Github to the research community.

# Non-line-of-sight Imaging
Non-line-of-sight (NLOS) imaging aims at recovering objects outside the direct line of sight of a sensor Most active NLOS imaging systems exploit an ultra-fast pulsed laser beam that can be controlled to direct light toward a relay surface (e.g., a wall). A companion time-resolved detector then collects the arrival time and number of photons that return after the first and third of three bounces: off the relay surface, off the hidden objects, and back off the relay surface. The first bounce corresponds to direct reflection in the line-of-sight (LOS) scene. By removing or gating the photons from the first bounce, photons from the third bounce are employed to reconstruct or to localize the hidden objects. Potential applications are numerous, including autonomous driving, remote sensing, and biomedical imaging.

![tt](/NeTF_images/1.png "A top-viewed scenario of the NLOS imaging system"){:height="100%" width="100%"}
<center style="font-size:14px;color:#B0B0B0;text-decoration:underline">A top-viewed scenario of the NLOS imaging system</center>

# New Calibration Scheme for Non-line-of-sight Imaging
we present an online calibration technique for a SPAD-based NLOS imaging system. Our technique needs no additional tools such as mirrors or a checkerboard. We decouple a transient acquired at onsite sampling into LOS and hidden components. We then exploit the LOS component to calibrate the relay surface and calculate a \textit{Gamma} map. By introducing the *Gamma* map, our calibration technique can preview the calibration effects when readjusting the hardware devices. Many fast Fourier transform (FFT)-based algorithms  require transients measured in a regular grid as input whereas learning-based methods allow flexible sampling patterns. Our online calibration technique enables our NLOS imaging system to support arbitrary sampling. Thus, we can uniformly sample detection points in, e.g., an evenly spaced regular grid and a ring and radius pattern (i.e., a concentric-circle pattern), and non-uniformly detect points on the relay surface.


<!-- <img src="/NeTF_images/2.png" height="100%" width="100%"/>
</div> -->
<div align=center>
<img src="/NeTF_images/1.png" height="70%" width="70%"/>
</div>
<center style="font-size:14px;color:#B0B0B0;text-decoration:underline">Detection points in different sampling patterns</center>

# NLOS Reconstruction validation
We validate the transients measured from our NLOS imaging system, which is calibrated with our online calibration technique. Using the measured transients, we reconstruct the hidden objects using SOTA methods, including LCT, FK, PF, and NeTF.

![cc](/OIvOC_images/resultsGalleryWithBar.pdf "Reconstruction evaluation using transients measured from our calibrated NLOS imaging system"){:height="100%" width="100%"}
<center style="font-size:14px;color:#B0B0B0;text-decoration:underline">Reconstruction evaluation using transients measured from our calibrated NLOS imaging system</center>

<!--Check out the [arXiv Page][arXiv] for more information. --> The code is available at [Code Release][code].

<!-- [arXiv]: https://arxiv.org/abs/2101.00373 -->
[code]: https://github.com/SCI2020/Inphomatool_public
