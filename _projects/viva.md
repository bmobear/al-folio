---
layout: default
title: viva
description: Visual Variation Learning for Object Recognition
img: /assets/img/2019_pami_viva_6.png
---

<h2 class="page-title">Visual Variation Learning for Object Recognition</h2>

<div class="pub_img center" width="100%">
    <img width="15%" src="{{ site.baseurl }}/assets/img/2019_pami_viva_0.png"/>
    <img width="30%" src="{{ site.baseurl }}/assets/img/2019_pami_viva_6.png"/>
    <img width="20%" src="{{ site.baseurl }}/assets/img/2019_pami_viva_7.png"/>
</div>

### Overview
+ We propose visual variation learning to improve object recognition with convolutional neural networks (CNN). While a typical CNN regards visual variations as nuisances and marginalizes them from the data, we speculate that some variations are informative. 
+ We study the impact of visual variation as an auxiliary task, during training only, on classification and similarity embedding problems. 
+ Our key contribution is that, at the cost of visual variation annotation during training only, CNN enhanced with visual variation learning learns better object representations.

<div class="citation">
    Visual Variation Learning for Object Recognition. Jatuporn Toy Leksut, Jiaping Zhang, Laurent Itti; Under Review, 2019 <br><br>


    [<a href="" target="_blank">PDF</a>]
</div>

---

### Data

#### iLab-20M
The iLab-20M dataset is a large-scale controlled, parametric dataset of toy vehicle objects under variations of viewpoint, lighting, and background. The dataset is produced by placing a physical object on a turntable and using multiple cameras located on a semicircular arc over the table. 

+ 15 categories: boat, bus, car, equipment, f1car, helicopter, military, monster truck, pickup truck, plane, semi truck, tank, train, UFO, and van 
+ 718 object instances
+ 88 different viewpoints (11 elevations x 8 azimuths)
+ 5 lighting conditions
+ 3 camera focus settings
+ 14 -- 40 background images
+ 22 million images total

<div class="pub_img center" width="100%">
    <img width="80%" src="{{ site.baseurl }}/assets/img/page_viva_ilab2m.png"/>
    <p class="caption">
    The iLab dataset provides toy vehicle images from 15 categories in various viewpoints, lighting conditions, and backgrounds.
    </p>
</div>

<div class="citation">
    iLab-20M: A Large-Scale Controlled Object Dataset to Investigate Deep Learning. Ali Borji, Saeed Izadi, Laurent Itti; The IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2016 <br><br>


    [DOI: <a href="https://doi.org/10.1109/CVPR.2016.244" target="_blank">10.1109/CVPR.2016.244</a>]
    [<a href="http://openaccess.thecvf.com/content_cvpr_2016/html/Borji_iLab-20M_A_Large-Scale_CVPR_2016_paper.html" target="_blank">Open Access</a>]
</div>

#### iLab-80M
The iLab-80M is an augmented set of the iLab-20M adding random crops and scales. The augmentation ensures that the number of images per category is well balanced, resulting in 5.5 million images per category and a total of 82.7 million images for the whole set. 

In addition, the original `960x720` images are cropped around each object and rescaled to `256x256`.

#### iLab-2M
From iLab-80M, we generate our own subsets for experiments conducted in this work. Our    variation is pose, therefore we select data that vary in pose variation and keep other visual variations constant.
+ 30 poses (5 elevations x 6 azimuths)
+ 1.2M training images, 270K validation images, 270K test images

<div class="link-button"><a href="">Download iLab-2M</a></div>


---

### Results

<div class="pub_img center" width="100%">
    <img width="45%" src="{{ site.baseurl }}/assets/img/alexinet.png"/>
    <img width="50%" src="{{ site.baseurl }}/assets/img/boxplot_multilayer.png"/>
    <p class="caption">
    Multi-layer injection results on iLab-2M
    </p>
</div>

<div class="pub_img center" width="100%">
    <img width="45%" src="{{ site.baseurl }}/assets/img/alexinet.png"/>
    <img width="50%" src="{{ site.baseurl }}/assets/img/boxplot_multilayer.png"/>
    <p class="caption">
    Multi-layer injection results on iLab-2M
    </p>
</div>

---
