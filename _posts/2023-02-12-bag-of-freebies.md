---
title: 'Bag-of-freebies in YOLOv4'
date: 2023-02-12
permalink: /posts/2023/02/BagOfFreebies/
tags:
- Computer Vision
---

You can think of 'Bag of freebies' as a collection of strategies for improving the overall precision without increasing the inference cost.
What is often adopted and meets the definition of BoF is data augmentation. Part of Bag-of-freebies will be covered in the following discussions.

Roadmap
======
* BBox regression
  * IOU
  * GIOU
  * DIOU
  * CIOU

* blocking
  * random erase
  * cutout
  * hide-and-seek
  * grid mask

* regularization
  * drop block

* multi-graph
  * mixup
  * cutmix
  * **Mosaic**

Bound box regression
======

IOU
------ 

![iou](https://aharendaisuki.github.io/images/iou.png "reference: https://zhuanlan.zhihu.com/p/104236411")

Reference: [https://zhuanlan.zhihu.com/p/104236411](https://zhuanlan.zhihu.com/p/104236411)


$ ground truth: x = (x_{top}, x_{bottom}, x_{left}, x_{right}) $

$ prediction: \widetilde{x} = (\widetilde{x}_{top}, \widetilde{x}_{bottom}, \widetilde{x}_{left}, \widetilde{x}_{right}) $


