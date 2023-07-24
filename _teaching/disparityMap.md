---
title: "Stereo disparity estimation"
collection: teaching
type: "CS4186 Computer vision and image process"
permalink: /teaching/DisparityMap
venue: "City University of Hong Kong, Department of Computer Science"
date: 2023-04-20
location: "Hong Kong, China"
---

Abstract
======
In this project, semi-global block matching (SGBM) is adopted to compute disparity map for stereo
matching task. Moreover, weighted least square (WLS) filtering is used for image filtering. OpenCV
library is utilized in the implementation of SGBM and WLS. In terms of evaluation metrics, peak signal-to-noise ratio
(PSNR) is selected to evaluate the difference between the ground truth disparity maps and results. In
my trial and error, the highest PSNR for three test cases, Art, Dolls and Reindeer is 17.00, 17.27
and 15.51 respectively. In comparison, empirical PSNR value in image compression ranges from 20 to 40.

Pdf files
======
[Instance_Search.pdf](http://AharenDaisuki.github.io/files/disparity_map.pdf)

Disparity map
======
![Art](http://AharenDaisuki.github.io/images/Art.png)
![Dolls](http://AharenDaisuki.github.io/images/Dolls.png)
![Reindeer](http://AharenDaisuki.github.io/images/Reindeer.png)

Code
======
[Disparity Map](https://github.com/AharenDaisuki/InstanceSearch)