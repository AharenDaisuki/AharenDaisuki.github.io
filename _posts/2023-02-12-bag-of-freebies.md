---
title: 'Bag-of-freebies in YOLOv4'
date: 2023-02-12
permalink: /posts/2023/02/BagOfFreebies/
tags:
- Computer Vision
---

Normally referred to as data augmentation, Bag-of-freebies means a collection of tricks used in YOLO that enhance detection precision 
with higher training cost but without increasing induction cost. Part of Bag-of-freebies will be covered in the following discussions.

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


