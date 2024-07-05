---
title: "BSCCS Final Year Project 2023-2024, Deep-learning model for camouflaged object detection"
collection: teaching
type: "CS4514 Project"
permalink: /teaching/FYP
venue: "City University of Hong Kong, Department of Computer Science"
date: 2024-04-01
location: "Hong Kong, China"
---

Abstract
======
* We propose a novel two-branch VCOD model that utilizes both RGB frames and motion estimations as inputs to give dense predictions of targets in a video.

* Different from other methods using implicit motion handling, we continue to use explicit optical flows in spite of acceptable estimation errors, for the purpose of saving computational cost. 
To this end, we introduce inter-branch feature fusion module to fuse feature maps obtained from two modalities, i.e., RGB frames and optical flow estimations. Besides, we also introduce intra-branch feature fusion module to fuse feature maps at multiple scales in order to get fine-grained features.

* Our proposed framework is non-trivial, which achieves 39 FPS (> 20 FPS) inference speed with a competitive performance among state-of-the-art methods on VCOD tasks. 
Our model outperforms the best method in the evaluation by 9.5% on MAE (mean absolute error) with 55.86 MB (67.82%) less parameters. However, we also observe that the state-of-the-art method outperforms our model on all other metrics.

![alt text](http://AharenDaisuki.github.io/images/qualitative_results.png)

Proposed Model
======
<p align="left">
    <img src="http://AharenDaisuki.github.io/images/proposed_framework.png" width='1400' height='300' /> <br />
    <em>
    Illustration of our model. First, the transformer-based backbone extracts
    features from two consecutive input frames and the corresponding motion estimation.
    Then, the proposed Inter-branch Feature Fusion module and Intra-branch Feature Fusion
    module fuse features from both appearance branch and motion branch.
    </em>
</p>

Our model is implemented in [PyTorch](https://github.com/pytorch/pytorch) framework and trained on a single NVIDIA GeForce RTX 3080 GPU of 10240 MiB memory.

Repository
======
[Repo](https://github.com/AharenDaisuki/Deep-learning-model-for-camouflaged-object-detection)

Final Report
=====
[Deep learning model for camouflaged object detection](https://drive.google.com/file/d/1hTAkfLB3w7eAXHaP47lbP5EZrpRNHKWT/view?usp=sharing)