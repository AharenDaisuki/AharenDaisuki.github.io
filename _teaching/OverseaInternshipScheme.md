---
title: "Oversea Internship Scheme"
collection: teaching
type: "FS4005 Oversea Internship Scheme"
permalink: /teaching/OIS
venue: "University of Tennessee, Knoxville"
date: 2023-05-29
location: "Tennessee, United States"
---

Abstract
======
MagmaDNN is a neural network library in C++ aiming at optimizing towards heterogeneous architectures, i.e., multi-core CPUs
and GPUs. Currently, no implementation of the multi-head attention layer, which is a core component of transformer models, is provided
by MagmaDNN library, despite the popularity and significance of transformer models in various tasks including vision tasks such as medical
segmentation, image recognition, semantic segmentation, and natural language processing tasks such as machine translation.

To bridge the gap, we present an implementation of the multi-head attention layer in MagmaDNN framework. Our implementation improves
the prediction loss by 20.41% compared with Tensorflow implementation, despite consuming extra training time (epoch = 1000, learning rate
= 0.001, batch size = 8, input size = (3 × 8 × 8)). Compared with Pytorch implementation, our method also outperforms it by a clear margin in
terms of prediction loss.

We conclude our contributions in this paper in two aspects:
* We present an implementation of the multi-head attention layer in MagmaDNN framework, 
making the development of transformer architectures possible for MagmaDNN library.

* We compare the performance among our multi-head layer with PyTorch and TensorFlow implementations.
Compared with competitors, our layer outperforms them by a clear margin in terms of the best-epoch prediction loss,
despite a reasonable extra training time for large-scale data.

Oral Presentation
======
[Final Presentation](http://AharenDaisuki.github.io/files/RECSEM_Transformer_Presentation_copy.pdf)

Poster Presentation
======
[Poster Presentation](http://AharenDaisuki.github.io/files/RECSEM_Poster_copy.pdf)

Assets
======
[Assets](http://AharenDaisuki.github.io/files/RECSEM2023_Transformer.pdf)

Certification
======
[OIS certification](http://AharenDaisuki.github.io/files/OIS_certification.pdf)